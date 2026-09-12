# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---:|---|---|---|
| 1 | Vinhomes | Lặp lại | Nhân viên CSKH phải đọc từng phản ánh của cư dân, xác định loại sự cố và chuyển tới bộ phận phụ trách. Nội dung thiếu thông tin hoặc có nhiều vấn đề dễ khiến việc phân loại và chuyển tiếp bị sai. |
| 2 | Vinpearl | Tốn thời gian | Nhân viên đặt phòng phải đọc email yêu cầu đặt phòng đoàn, trích xuất ngày đến/đi, số khách, loại phòng và yêu cầu đặc biệt để nhập vào biểu mẫu. Email dài và thông tin phân tán khiến việc xử lý chậm. |
| 3 | VinFast | AI có thể tốt hơn | Khách hàng mô tả lỗi xe bằng ngôn ngữ đời thường, còn nhân viên tiếp nhận phải hỏi lại nhiều lần để ghi nhận triệu chứng và chuyển đúng nhóm kỹ thuật. AI có thể hỗ trợ chuẩn hóa mô tả và soạn câu hỏi bổ sung. |
| 4 | Xanh SM | Pain từ người khác | Tài xế và khách mất thời gian gọi lại khi điểm đón trên bản đồ không khớp với mô tả như “cổng sau” hoặc “bên kia đường”. Nhân viên hỗ trợ phải đọc trao đổi để xác định thông tin cần làm rõ. |
| 5 | Vinpearl | Lặp lại | Nhân viên vận hành phải đọc nhiều đánh giá khách sạn, phân loại phàn nàn và tổng hợp vấn đề theo bộ phận. Các phản ánh nghiêm trọng dễ bị bỏ sót trong số lượng lớn review. |
---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

┌──────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                        │
│                                                                              │
│ Bài toán: Nhân viên CSKH Vinhomes phải đọc, phân loại và chuyển phản ánh     │
│ của cư dân đến đúng bộ phận xử lý.                                           │
│                                                                              │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [X] Vinhomes                  │
│                     [ ] Vinmec   [ ] Khác                                   │
│                                                                              │
│ Ai đang đau (Actor)?                                                         │
│ - Nhân viên CSKH                                                             │
│ - Ban quản lý tòa nhà                                                        │
│ - Cư dân gửi phản ánh                                                        │
│                                                                              │
│ Workflow thủ công hiện tại:                                                 │
│ 1. Cư dân gửi phản ánh qua ứng dụng/tổng đài                                 │
│ ──> 2. Nhân viên đọc và tóm tắt nội dung                                    │
│ ──> 3. Xác định loại sự cố và mức độ ưu tiên                                │
│ ──> 4. Chuyển đến bộ phận phù hợp                                           │
│ ──> 5. Bộ phận xử lý cập nhật trạng thái                                    │
│                                                                              │
│ Bước tốn thời gian/lỗi nhất: Bước 2 và 3 (⏱ khoảng 7 phút/phản ánh)          │
│ AI hỗ trợ: Tóm tắt, phân loại, phát hiện khẩn cấp, đề xuất bộ phận           │
│ và tạo bản nháp để nhân viên duyệt.                                         │
│                                                                              │
│ Metric: Giảm 7 phút ──> dưới 2 phút/phản ánh; macro-F1 ≥ 90%;                │
│ 100% phản ánh khẩn cấp được gắn cờ để nhân viên kiểm tra.                    │
│                                                                              │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM Feature + Rule  [ ] Agent  │
└──────────────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                        │
│                                                                              │
│ Bài toán: Nhân viên đặt phòng Vinpearl phải đọc email đặt phòng đoàn,        │
│ trích xuất thông tin và nhập thủ công vào biểu mẫu.                          │
│                                                                              │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes                  │
│                     [ ] Vinmec   [X] Khác: Vinpearl                         │
│                                                                              │
│ Ai đang đau (Actor)?                                                         │
│ - Nhân viên đặt phòng                                                        │
│ - Nhân viên kinh doanh                                                       │
│ - Công ty lữ hành                                                            │
│                                                                              │
│ Workflow thủ công hiện tại:                                                 │
│ 1. Nhận email đặt phòng đoàn                                                 │
│ ──> 2. Đọc email và tệp đính kèm                                            │
│ ──> 3. Trích xuất ngày, số khách, loại phòng và yêu cầu đặc biệt             │
│ ──> 4. Kiểm tra thông tin thiếu/mâu thuẫn                                   │
│ ──> 5. Nhập hệ thống và gửi email xác nhận                                  │
│                                                                              │
│ Bước tốn thời gian/lỗi nhất: Bước 2 và 3 (⏱ khoảng 15 phút/email)            │
│ AI hỗ trợ: Trích xuất dữ liệu, đánh dấu thông tin thiếu/mâu thuẫn             │
│ và tạo bản nháp email yêu cầu bổ sung.                                      │
│                                                                              │
│ Metric: Giảm 15 phút ──> dưới 5 phút/email; độ chính xác trường bắt buộc     │
│ ≥ 95%; 100% trường thiếu hoặc mâu thuẫn được đánh dấu.                      │
│                                                                              │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM Feature + Rule  [ ] Agent  │
└──────────────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                        │
│                                                                              │
│ Bài toán: Nhân viên tiếp nhận VinFast phải chuẩn hóa mô tả lỗi xe và         │
│ chuyển thông tin đến đúng nhóm kỹ thuật.                                     │
│                                                                              │
│ Công ty thành viên: [X] VinFast  [ ] Xanh SM  [ ] Vinhomes                  │
│                     [ ] Vinmec   [ ] Khác                                   │
│                                                                              │
│ Ai đang đau (Actor)?                                                         │
│ - Khách hàng                                                                 │
│ - Nhân viên tổng đài/dịch vụ                                                 │
│ - Kỹ thuật viên                                                              │
│                                                                              │
│ Workflow thủ công hiện tại:                                                 │
│ 1. Khách hàng gọi hoặc gửi mô tả lỗi                                        │
│ ──> 2. Nhân viên đọc và hỏi thêm triệu chứng                                │
│ ──> 3. Ghi nhận thông tin vào phiếu dịch vụ                                 │
│ ──> 4. Phân loại và chuyển nhóm kỹ thuật                                    │
│ ──> 5. Kỹ thuật viên kiểm tra và xác nhận nguyên nhân                       │
│                                                                              │
│ Bước tốn thời gian/lỗi nhất: Bước 2 và 4 (⏱ khoảng 12 phút/trường hợp)      │
│ AI hỗ trợ: Tóm tắt triệu chứng, chuẩn hóa thuật ngữ, đề xuất câu hỏi,        │
│ gợi ý nhóm kỹ thuật và gắn cờ trường hợp nguy hiểm.                         │
│                                                                              │
│ Metric: Giảm 12 phút ──> dưới 5 phút/trường hợp; độ chính xác phân loại      │
│ ≥ 85%; 100% trường hợp liên quan đến phanh, pin hoặc va chạm được gắn cờ.   │
│                                                                              │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM Feature + Rule  [ ] Agent  │
└──────────────────────────────────────────────────────────────────────────────┘
> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---
