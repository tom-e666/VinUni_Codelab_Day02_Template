> * **Họ và tên:** Nguyễn Đức Long
> * **MSSV:** 2A202602917  
---

# 02-deep-dive-report.md (Báo cáo Phân tích sâu)

> **Mục tiêu:** Định hình chi tiết (scoping) bài toán ứng dụng AI cho Khối Vận Hành Dịch vụ Xưởng VinFast, thiết lập ranh giới an toàn và đánh giá độ khả thi của dự án.
> **Dự án:** Hỗ trợ tiếp nhận & chẩn đoán sơ bộ sự cố xe điện VinFast.

---

## 🏗️ Phase 3 — DEEP-DIVE

### 3.1. Current-State Workflow (Quy trình hiện tại)

Quy trình tiếp nhận và chẩn đoán sơ bộ khi khách hàng đưa xe điện VinFast gặp sự cố vào xưởng dịch vụ:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Khách báo lỗi│     │ Cố vấn dịch  │     │ Tra cứu sổ   │     │ Ước tính TG &│
│ hoặc gửi ảnh │ ──→ │ vụ thu thập  │ ──→ │ tay kỹ thuật │ ──→ │ lập báo giá  │
│ màn hình xe  │     │ triệu chứng  │     │ chẩn đoán    │     │ sơ bộ        │
│ Ai: Khách/Cố │     │ Ai: Cố vấn   │     │ Ai: Kỹ thuật │     │ Ai: Cố vấn   │
│ vấn          │     │              │     │ viên/Cố vấn  │     │              │
│ ⏱ 5 phút     │     │ ⏱ 5 phút     │     │ ⏱ 20-30 phút 🔴│     │ ⏱ 5 phút     │
│ In: Lời nói/ │     │ In: Text/Log │     │ In: Triệu chứng│     │ In: Mã vật tư│
│ Hình ảnh     │     │ Out: Note    │     │ Out: Mã lỗi  │     │ Out: Báo giá │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
🔴 = Bottlenecks (Điểm tắc nghẽn)
⏱ Tổng thời gian xử lý thủ công ban đầu: ~35-45 phút/lượt.

```

### 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung chi tiết |
| --- | --- |
| **1. Actor / Operator** | Kỹ thuật viên (Technician) & Cố vấn dịch vụ (Service Advisor) tại các xưởng dịch vụ VinFast. |
| **2. Current Workflow** | Khi nhận xe lỗi, cố vấn ghi nhận tình trạng hoặc hình ảnh lỗi từ màn hình. Kỹ thuật viên phải đối chiếu thủ công triệu chứng với hàng ngàn trang tài liệu (Sổ tay sửa chữa, Cẩm nang mã lỗi) theo từng dòng xe và phiên bản phần mềm để tìm ra nguyên nhân và danh sách linh kiện cần kiểm tra. |
| **3. Bottleneck** | **Bước 3:** Việc tra cứu thông tin trong các tài liệu kỹ thuật phân mảnh và phức tạp của xe điện (EV) mất quá nhiều thời gian, đặc biệt với các ca bệnh khó hoặc mã lỗi mới (mất trung bình 20-30 phút). |
| **4. Business Impact** | Khách hàng phải chờ đợi lâu tại phòng chờ chỉ để biết xe bị lỗi gì. Giờ cao điểm gây ùn ứ tại khu vực tiếp nhận. Khó tối ưu hóa năng suất của kỹ thuật viên do thời gian "chết" ở khâu tra cứu tài liệu quá cao. |
| **5. Success Metric** | 1. Giảm thời gian chẩn đoán và tra cứu mã lỗi sơ bộ từ 25-30 phút xuống **< 5 phút/ca**.<br>

<br>2. Độ chính xác của top 3 nguyên nhân và mã vật tư được hệ thống gợi ý đạt **> 90%**. |
| **6. Operational Boundary** | **Được phép:** AI (Vision + RAG) được phép đọc hình ảnh màn hình lỗi, truy xuất kho dữ liệu sổ tay kỹ thuật nội bộ, tóm tắt quy trình xử lý và gợi ý mã vật tư thay thế.<br>

<br>**CẤM:** Tuyệt đối không được tự động xuất báo giá chính thức cho khách hàng. Không được tự động ra quyết định thay thế các cụm linh kiện giá trị cao (Pin, Động cơ) mà bỏ qua bước xác nhận của Kỹ sư trưởng. |

### 3.3. Future-State Flow & AI Fit

* **Mức AI Fit:** **LLM Feature** (Cụ thể: Ứng dụng mô hình LLM Multimodal để trích xuất text từ ảnh chụp màn hình xe và kiến trúc RAG - Retrieval-Augmented Generation để truy vấn sổ tay kỹ thuật).
* **Quy trình tương lai (Future-State):**

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Upload ảnh / │     │ 🔵 AI OCR &  │     │ 🟢 Cố vấn /  │     │ 🟢 Hệ thống  │
│ Text mô tả   │ ──→ │ RAG tra cứu  │ ──→ │ KTV click    │ ──→ │ ERP xuất báo │
│ sự cố vào App│     │ Sổ tay -> Gợi│     │ duyệt nguyên │     │ giá sơ bộ    │
│ nội bộ       │     │ ý nguyên nhân│     │ nhân hợp lý  │     │ cho khách    │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ↩️ Fallback:
                                                               Nếu ảnh quá mờ, lỗi 
                                                               không có trong DB 
                                                               (Confidence score 
                                                               < 70%), LLM thông báo 
                                                               KTV tự tra cứu thủ công.

```

---

## 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist:

1. [x] **Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?**
*(VinFast đã có hệ thống tài liệu số hóa: Owner's Manual, Repair Manual, CSDL mã lỗi DTC).*
2. [x] **Rủi ro khi AI sai có nằm trong tầm kiểm soát?**
*(Có, vì hệ thống chỉ đóng vai trò "Trợ lý gợi ý" (Copilot). Cố vấn dịch vụ và Kỹ thuật viên vẫn là người review và chốt phương án cuối cùng - HITL).*
3. [x] **Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?**
*(Có, các kỹ thuật viên luôn mong muốn có công cụ tra cứu nhanh để giảm tải áp lực KPI thời gian xử lý xe trong ca làm việc).*

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

**[x] GO (Bắt đầu xây dựng Prototype)**
[ ] NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline)
[ ] NO-GO (Không khả thi / Rule-based tốt hơn)

**Justification (Lý giải quyết định):**
Bài toán này giải quyết trực tiếp một "nút thắt cổ chai" (bottleneck) cực kỳ rõ ràng trong vận hành xưởng dịch vụ. Không giống như các nghiệp vụ có thể giải quyết bằng hệ thống Rule-based thông thường, việc chẩn đoán sự cố xe điện dựa trên mô tả văn bản tự do của khách hàng hoặc hình ảnh chụp màn hình không có cấu trúc là thế mạnh tuyệt đối của LLM (Vision & Text processing).

Việc tích hợp RAG vào quy trình này có tính khả thi kỹ thuật cao vì dữ liệu nội bộ (tài liệu kỹ thuật) đã có sẵn. Hơn nữa, việc áp dụng mô hình Human-in-the-loop (HITL) đảm bảo rủi ro chẩn đoán sai lệch (hallucination) ảnh hưởng đến an toàn xe được triệt tiêu hoàn toàn. Chi phí đầu tư cho một hệ thống AI nội bộ rẻ hơn rất nhiều so với tổn thất do giảm năng suất tiếp nhận và trải nghiệm tồi tệ của khách hàng khi phải chờ đợi. Dự án đủ điều kiện để tiến hành làm bản mẫu (Prototype).