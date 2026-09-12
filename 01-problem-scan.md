# 01-problem-scan.md — Ý tưởng cá nhân (SCAN & QUICK-ASSESS)

**Họ và tên:** Nguyễn Văn A  
**MSSV:** 20210000  
**Vai trò:** AI Product Engineer — Vin Smart Future  
**Ngày thực hiện:** 12/09/2026  

---

## 🔍 Phase 1 — SCAN: Bảng quét cơ hội tối ưu hóa bằng AI (Vingroup)

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Stakeholder Pain) để tìm kiếm các bottleneck vận hành trong hệ sinh thái Vingroup:

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| **1** | **Xanh SM (GSM)** | Repetitive / Time-consuming | **Xử lý và phân loại khiếu nại tài xế/khách hàng qua kênh Chat/Callbot.** Hằng ngày tiếp nhận hàng chục ngàn yêu cầu phản hồi về cuốc xe, sai lệch cước phí, thái độ phục vụ. Nhân viên CSKH phải đọc transcript, phân loại ticket thủ công và gán nhãn ưu tiên. |
| **2** | **VinFast** | Stakeholder Pain / Time-consuming | **Tổng hợp & Phân tích lỗi kỹ thuật xe điện (EV Diagnostic Log & Field Issues) từ Showroom/Xưởng dịch vụ.** Kỹ thuật viên mất nhiều thời gian đọc log lỗi dài, tổng hợp phản ánh của khách hàng để đưa ra gợi ý sửa chữa chính xác theo tiêu chuẩn nhà máy. |
| **3** | **Vinhomes** | Time-consuming / AI-upgrade | **Tự động hóa tiếp nhận & Soạn thảo phản hồi góp ý/khiếu nại cư dân trên App Vinhomes Resident.** BQL mất 15-30 phút để đọc phản ánh, kiểm tra quy định đô thị và soạn văn bản phản hồi vừa chuẩn mực vừa xoa dịu cư dân. |
| **4** | **Vinmec** | Time-consuming / Repetitive | **Tóm tắt bệnh án y tế & Hỗ trợ chuẩn hóa dữ liệu hồ sơ bệnh án điện tử (EMR).** Bác sĩ mất nhiều thời gian tổng hợp lịch sử khám, xét nghiệm và đơn thuốc cũ từ file PDF/ảnh quét để đưa ra tóm tắt lâm sàng nhanh trước khi nhập viện. |
| **5** | **Vinpearl / VinWonders** | AI-upgrade / Repetitive | **Trợ lý AI tư vấn lịch trình vui chơi & Quản lý đặt phòng linh hoạt.** Khách hàng thường hỏi lặp đi lặp lại về giờ mở cửa, điều kiện chiều cao trò chơi, gợi ý lịch trình theo thời tiết và số lượng trẻ em đi kèm. |

---

## 🃏 Phase 2 — QUICK-ASSESS: Top 3 Quick Problem Cards

---

### ┌─────────────────────────────────────────────────────────────┐
### │ QUICK PROBLEM CARD #1: Xanh SM Complaint & Ticket Triage   │
### └─────────────────────────────────────────────────────────────┘

* **Bài toán (1 câu):** Tự động hóa quá trình đọc, trích xuất thông tin, phân loại mức độ khẩn cấp và đề xuất hướng xử lý cho các ticket khiếu nại của tài xế và khách hàng Xanh SM.
* **Công ty thành viên:** `[X]` Xanh SM `[ ]` VinFast `[ ]` Vinhomes `[ ]` Vinmec `[ ]` Khác
* **Ai đang đau (Actor)?** Nhân viên Vận hành CSKH Tier-1 (Xanh SM Operation Team) và Chuyên viên giải quyết khiếu nại.
* **Workflow thủ công hiện tại (4 bước):**
  1. *Khách hàng/Tài xế gửi khiếu nại (App/Call Center)* ──>
  2. *CSKH đọc thủ công transcript/tin nhắn và tra cứu thông tin chuyến đi* ──>
  3. *Gán nhãn loại sự cố (Cước phí, Tài xế, Xe hỏng, Tai nạn) và chuyển Ticket cho bộ phận liên quan* ──>
  4. *Soạn phản hồi mẫu hoặc gọi lại cho khách hàng*
* **Bước nào tốn thời gian/lỗi nhất?** Bước 2 & 3 (Phân loại, đọc hiểu ngữ cảnh khiếu nại và tra cứu quy trình xử lý). ⏱ **7 - 12 phút/ticket**.
* **AI có thể nhảy vào hỗ trợ ở bước nào?** Đọc transcript/text khiếu nại ──> Trích xuất thực thể (Loại sự cố, Mã chuyến xe, Số tiền tranh chấp) ──> Đánh giá Sentiment & Mức độ khẩn cấp ──> Tự động phân loại Ticket & Soạn sẵn bản thảo phản hồi cho CSKH duyệt (HITL).
* **Đo thành công bằng gì (Metric có số)?**
  * Giảm thời gian xử lý ticket (TTR - Time to Resolve) từ **10 phút ──> dưới 2.5 phút/ticket**.
  * Độ chính xác phân loại sự cố (Triage Accuracy) đạt **> 92%**.
  * Tăng năng suất xử lý ticket của 1 nhân viên CSKH lên **300%**.
* **Quick Architecture:** `[ ]` No AI `[ ]` Rule `[ ]` LLM `[X]` Agent

---

### ┌─────────────────────────────────────────────────────────────┐
### │ QUICK PROBLEM CARD #2: Vinhomes Resident Issue Responder  │
### └─────────────────────────────────────────────────────────────┘

* **Bài toán (1 câu):** Phân tích phản ánh/khiếu nại của cư dân trên App Vinhomes Resident và tự động soạn thảo văn bản phản hồi chuẩn mực, đúng quy định đô thị để Ban Quản Lý (BQL) duyệt nhanh.
* **Công ty thành viên:** `[ ]` Xanh SM `[ ]` VinFast `[X]` Vinhomes `[ ]` Vinmec `[ ]` Khác
* **Ai đang đau (Actor)?** Nhân viên Ban Quản Lý Vinhomes (Resident Care Specialist).
* **Workflow thủ công hiện tại (4 bước):**
  1. *Cư dân gửi ý kiến/khiếu nại qua ứng dụng Vinhomes Resident* ──>
  2. *Nhân viên BQL đọc phản ánh, phân loại nội dung (Tiếng ồn, An ninh, Tiện ích, Vệ sinh)* ──>
  3. *Tra cứu Sổ tay Cư dân/Quy định KĐT tương ứng để tìm hướng giải quyết* ──>
  4. *Soạn email/thông báo trả lời cư dân và trình Trưởng BQL ký duyệt*
* **Bước nào tốn thời gian/lỗi nhất?** Bước 3 & 4 (Tra cứu nội quy và viết phản hồi sao cho đúng chuẩn mực, lịch sự, tránh leo thang căng thẳng). ⏱ **15 - 20 phút/phản ánh**.
* **AI có thể nhảy vào hỗ trợ ở bước nào?** Đọc nội dung phản ánh ──> Tra cứu RAG trên cơ sở dữ liệu Quy định/Sổ tay cư dân Vinhomes ──> Phân tích thái độ cư dân ──> Tự động tạo bản thảo trả lời chứa đầy đủ quy định và giải pháp xử lý ──> BQL chỉ cần review & ấn Gửi.
* **Đo thành công bằng gì (Metric có số)?**
  * Giảm thời gian phản hồi cư dân ban đầu từ **24 giờ ──> dưới 30 phút**.
  * Giảm tỷ lệ phản hồi lại do không hài lòng với cách trả lời từ **18% ──> dưới 5%**.
  * Tỷ lệ bản thảo AI được BQL giữ nguyên không cần sửa đổi đạt **> 80%**.
* **Quick Architecture:** `[ ]` No AI `[ ]` Rule `[X]` LLM `[ ]` Agent

---

### ┌─────────────────────────────────────────────────────────────┐
### │ QUICK PROBLEM CARD #3: VinFast EV Diagnostic Summarizer    │
### └─────────────────────────────────────────────────────────────┘

* **Bài toán (1 câu):** Tóm tắt log lỗi kỹ thuật xe điện VinFast kết hợp phản ánh của khách hàng để gợi ý quy trình chẩn đoán & khắc phục nhanh cho kỹ thuật viên tại Showroom/Xưởng dịch vụ.
* **Công ty thành viên:** `[ ]` Xanh SM `[X]` VinFast `[ ]` Vinhomes `[ ]` Vinmec `[ ]` Khác
* **Ai đang đau (Actor)?** Kỹ thuật viên Dịch vụ VinFast (Service Technician / Service Advisor).
* **Workflow thủ công hiện tại (4 bước):**
  1. *Tiếp nhận xe VinFast vào xưởng dịch vụ kèm mô tả lỗi từ chủ xe* ──>
  2. *Cắm máy đọc lỗi OBD-II, xuất file diagnostic log dài hàng ngàn dòng code/mã DTC* ──>
  3. *Kỹ thuật viên đọc log, đối chiếu tay với Manual hướng dẫn sửa chữa của VinFast* ──>
  4. *Lập danh sách phụ tùng cần thay thế / các bước kiểm tra phần mềm/pin*
* **Bước nào tốn thời gian/lỗi nhất?** Bước 3 (Đọc hiểu log lỗi phức tạp kết hợp mã DTC và tra cứu tài liệu kỹ thuật). ⏱ **25 - 40 phút/xe**.
* **AI có thể nhảy vào hỗ trợ ở bước nào?** Phân tích file log DTC ──> Trích xuất các lỗi trọng tâm ──> Tổng hợp cùng mô tả hiện tượng của khách ──> Đối chiếu Service Manual ──> Đưa ra Báo cáo chẩn đoán sơ bộ & Check-list 5 bước kiểm tra đề xuất cho KTV.
* **Đo thành công bằng gì (Metric có số)?**
  * Rút ngắn thời gian chẩn đoán ban đầu từ **30 phút ──> dưới 5 phút/xe**.
  * Tăng tỷ lệ chẩn đoán đúng ngay lần đầu (First-Time Right) từ **78% ──> trên 92%**.
* **Quick Architecture:** `[ ]` No AI `[ ]` Rule `[X]` LLM `[ ]` Agent
