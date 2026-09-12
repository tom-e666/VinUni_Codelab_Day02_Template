# 📄 02 — Deep-Dive Report: Trợ lý chẩn đoán sơ bộ sự cố xe điện VinFast

> **Vin Smart Future — Lab 02: AI Product Scoping**
> **Mảng kinh doanh lựa chọn:** 🚗 **VinFast — Khối Dịch vụ hậu mãi (Xưởng dịch vụ uỷ quyền)**
> **Bài toán Deep-Dive:** Quick Problem Card #2 — *Hỗ trợ tiếp nhận & chẩn đoán sơ bộ sự cố xe điện VinFast*
>
> ⚠️ **Ghi chú về số liệu:** Toàn bộ con số trong báo cáo là **ước tính vận hành cần kiểm chứng** bằng log DMS (Dealer Management System) và lịch sử phiếu dịch vụ (Repair Order) thực tế của xưởng trước khi đưa vào KPI chính thức.

---

## 🗳️ Quyết định lựa chọn bài toán của nhóm

Nhóm chọn **Card #2 (VinFast — Chẩn đoán sơ bộ)** để Deep-Dive, loại 2 thẻ còn lại vì:

| Thẻ | Quyết định | Lý do |
|---|---|---|
| **#1 Vinhomes — Phân loại phản ánh cư dân** | ❌ Loại | Bài toán phân loại văn bản thuần tuý, một **rule-based router + từ khoá** đã giải quyết được ~70% lượng ticket với chi phí gần bằng 0. Giá trị gia tăng của LLM thấp so với rủi ro. |
| **#2 VinFast — Chẩn đoán sơ bộ** | ✅ **CHỌN** | Bottleneck là **tra cứu tri thức kỹ thuật phi cấu trúc** (sổ tay, service bulletin, lịch sử RO) — đúng thế mạnh của LLM + RAG mà rule-based không làm được. Tổn thất/lượt lớn (20–30 phút), tần suất cao, và ranh giới an toàn có thể kiểm soát bằng HITL. |
| **#3 Vinpearl — Trích xuất email đặt phòng đoàn** | ❌ Loại | Là bài toán extraction tốt nhưng **tác động kinh doanh phân tán** (theo mùa vụ), và phần lớn email đoàn đã có template sẵn → regex/parser truyền thống xử lý được phần lớn. |

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

                    KHÁCH HÀNG
                        │
                        ▼
             🔄 Báo lỗi / gửi hình ảnh
                        │
                        ▼
             🔄 Cố vấn dịch vụ tiếp nhận
                        │
                        ▼
             🔴 Đọc mô tả + hình ảnh
                        │
                        ▼
             🔴 Tra cứu sổ tay kỹ thuật
                / tài liệu sửa chữa
                        │
                        ▼
             🔴 Đối chiếu mã lỗi /
                triệu chứng / linh kiện
                        │
                        ▼
             Kỹ thuật viên xác nhận
                        │
                        ▼
             Ước tính thời gian +
             lập báo giá sơ bộ

Thời gian ước tính
| Bước     | Công việc                      |            Thời gian |
| -------- | ------------------------------ | -------------------: |
| 1        | Tiếp nhận thông tin + hình ảnh |            ~2–3 phút |
| 2        | Đọc mô tả triệu chứng          |            ~3–5 phút |
| 3        | 🔴 Tra cứu tài liệu kỹ thuật   |      **~10–15 phút** |
| 4        | 🔴 Đối chiếu mã lỗi/linh kiện  |       **~5–10 phút** |
| 5        | Ước tính + báo giá sơ bộ       |              ~5 phút |
| **Tổng** |                                | **~25–35 phút/lượt** |

🔄 Handoff

Có 3 điểm handoff đáng chú ý:

Khách hàng
    ↓ 🔄
Cố vấn dịch vụ
    ↓ 🔄
Hệ thống tài liệu / lịch sử xe / dữ liệu lỗi
    ↓ 🔄
Kỹ thuật viên

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Field	Nội dung chi tiết
1. Actor / Operator	Cố vấn dịch vụ và kỹ thuật viên VinFast – tiếp nhận thông tin, xác định triệu chứng, tra cứu tài liệu và chuẩn bị chẩn đoán ban đầu.
2. Current Workflow	Khách báo lỗi/gửi ảnh → cố vấn đọc mô tả → tra cứu manual/tài liệu kỹ thuật → đối chiếu mã lỗi, triệu chứng và linh kiện → kỹ thuật viên xác nhận → ước tính thời gian và chi phí. Công cụ có thể gồm hệ thống dịch vụ, tài liệu kỹ thuật và lịch sử sửa chữa.
3. Bottleneck	🔴 Tra cứu tài liệu và đối chiếu triệu chứng/mã lỗi là bước tốn thời gian nhất, đặc biệt với các ca hiếm hoặc mô tả lỗi không chuẩn hóa.
4. Business Impact	Giả định một case mất ~25–35 phút để chẩn đoán sơ bộ, trong đó ~15–25 phút dành cho tra cứu/đối chiếu. Nếu có hàng trăm case/ngày, thời gian này tạo ra đáng kể chi phí nhân sự và có thể kéo dài thời gian tiếp nhận xe. Cần validate bằng dữ liệu vận hành thực tế.
5. Success Metric	Giảm thời gian chẩn đoán sơ bộ từ ~25 phút → <5 phút; ≥85% case được AI đưa ra top-3 nguyên nhân/mã lỗi phù hợp để kỹ thuật viên review; giảm ≥60% thời gian tra cứu tài liệu.
6. Operational Boundary	AI được phép phân tích mô tả/hình ảnh, tìm kiếm tài liệu liên quan, tóm tắt triệu chứng và đề xuất mã lỗi/nguyên nhân/linh kiện. AI không được tự xác nhận chẩn đoán cuối cùng, tự quyết định thay thế linh kiện, tự hướng dẫn thao tác sửa chữa nguy hiểm hoặc tự phê duyệt báo giá. Kỹ thuật viên phải xác nhận trước khi thực hiện.

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [X] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

                     KHÁCH HÀNG
                         │
                         ▼
                Báo lỗi + hình ảnh
                         │
                         ▼
              🔄 Chuẩn hóa thông tin
                         │
                         ▼
                 🔵 AI / LLM
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       Symptoms       Image         Error codes
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                   🔵 RAG Search
                         │
                         ▼
              Tài liệu kỹ thuật liên quan
                         │
                         ▼
                 🔵 AI Recommendation
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       Top-3 causes   Error code    Parts/docs
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                  🔵 Confidence Check
                         │
                ┌────────┴────────┐
                │                 │
          Confidence ≥ 0.85   Confidence < 0.85
                │                 │
                ▼                 ▼
        🟢 Technician       ↩️ Fallback
           Review                 │
                │                 ▼
                │          Manual document search
                │                 │
                └────────┬────────┘
                         ▼
                 🟢 Technician
                 confirms diagnosis
                         │
                         ▼
                 Repair / Quotation

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
AI Readiness Checklist
Checklist	Đánh giá	Lý do
1. Có dữ liệu mẫu/logs sạch để test?	☑ Có, nhưng cần chuẩn hóa	Prototype có thể dùng mô tả lỗi mẫu, hình ảnh dashboard và tài liệu kỹ thuật đã được phê duyệt. Tuy nhiên cần chuẩn hóa dataset và tạo bộ test case có ground truth.
2. Rủi ro AI sai có kiểm soát được?	☑ Có	AI chỉ đưa ra gợi ý Top-3 nguyên nhân/mã lỗi, không tự quyết định sửa chữa. Case confidence thấp hoặc có nguy cơ an toàn → Human Review.
3. Stakeholders sẵn sàng thay đổi workflow?	☑ Có điều kiện	Cố vấn/kỹ thuật viên vẫn giữ quyền quyết định cuối cùng; AI chỉ giảm thời gian tra cứu và tổng hợp nên mức thay đổi quy trình không quá lớn. Cần pilot với một nhóm kỹ thuật viên trước.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[X] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp. Chỉ xây dựng AI hỗ trợ phân tích mô tả lỗi + hình ảnh dashboard + truy xuất tài liệu kỹ thuật + đề xuất Top-3 nguyên nhân/mã lỗi cho một nhóm lỗi xe điện giới hạn.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> GO vì bài toán có bottleneck vận hành rõ ràng: kỹ thuật viên/cố vấn mất khoảng 25–35 phút/case, trong đó khoảng 15–25 phút dành cho tra cứu và đối chiếu tài liệu. Đây là công việc có khả năng giảm đáng kể bằng AI khi đầu vào gồm ngôn ngữ tự nhiên và hình ảnh, những dạng dữ liệu mà rule-based thuần túy khó bao phủ toàn bộ.

Về mặt kỹ thuật, prototype có thể sử dụng Multimodal LLM + RAG để hiểu triệu chứng và tìm kiếm trong tài liệu kỹ thuật, sau đó trả về Top-3 nguyên nhân/mã lỗi kèm bằng chứng. Rule-based validation được dùng cho các mã lỗi và business rule đã biết.

Về mặt chi phí và rủi ro, AI không được tự đưa ra quyết định sửa chữa, thay linh kiện hay phê duyệt báo giá. Kỹ thuật viên luôn là người xác nhận cuối cùng; các trường hợp confidence thấp sẽ fallback về tra cứu thủ công. Vì vậy rủi ro có thể kiểm soát bằng HITL + confidence threshold + fallback.

Prototype được xem là thành công nếu giảm thời gian chẩn đoán sơ bộ từ ~25 phút xuống dưới 5 phút, Top-3 diagnostic recall ≥85%, thời gian tra cứu tài liệu <2 phút và technician acceptance rate ≥80%.

Không nên triển khai production ngay cho đến khi có baseline thực tế, dataset có ground truth và đánh giá riêng đối với các case liên quan đến an toàn pin/điện áp cao.

---