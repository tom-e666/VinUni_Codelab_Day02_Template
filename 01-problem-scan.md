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

## QUICK PROBLEM CARD #1

**Bài toán:**  
Nhân viên CSKH Vinhomes phải đọc phản ánh của cư dân, phân loại nội dung, xác định mức độ ưu tiên và chuyển đến đúng bộ phận xử lý.

**Công ty thành viên:** [ ] VinFast  [ ] Xanh SM  [X] Vinhomes  [ ] Vinmec  [ ] Khác

**Ai đang đau (Actor)?**

- Nhân viên CSKH
- Ban quản lý tòa nhà
- Cư dân gửi phản ánh

**Workflow thủ công hiện tại:**

1. Cư dân gửi phản ánh qua ứng dụng hoặc tổng đài.
2. Nhân viên CSKH đọc và tóm tắt nội dung.
3. Nhân viên xác định loại sự cố và mức độ ưu tiên.
4. Nhân viên chuyển phản ánh đến bộ phận phù hợp.
5. Bộ phận xử lý cập nhật trạng thái cho cư dân.

**Bước tốn thời gian/lỗi nhất:**  
Bước 2 và 3: đọc, hiểu và phân loại phản ánh thủ công.  
Thời gian ước tính: khoảng **7 phút/phản ánh**, cần kiểm chứng bằng dữ liệu thực tế.

**AI có thể hỗ trợ ở đâu?**

- Tóm tắt nội dung phản ánh.
- Đề xuất nhãn phân loại.
- Phát hiện dấu hiệu khẩn cấp.
- Đề xuất bộ phận xử lý.
- Tạo bản nháp để nhân viên kiểm tra và duyệt.

**Đo thành công bằng gì?**

- Giảm thời gian phân loại từ **7 phút xuống dưới 2 phút/phản ánh**.
- Đạt **macro-F1 tối thiểu 90%** trên tập dữ liệu đã được nhân viên gán nhãn.
- **100% phản ánh có dấu hiệu khẩn cấp** được gắn cờ để nhân viên kiểm tra.
- AI không tự động loại bỏ hoặc gửi phản hồi khi chưa được duyệt.

**Quick Architecture:** [ ] No AI  [ ] Rule  [X] LLM Feature + Rule  [ ] Agent
## QUICK PROBLEM CARD #2

**Bài toán:**  
Nhân viên đặt phòng Vinpearl phải đọc email đặt phòng đoàn, trích xuất thông tin và nhập thủ công vào biểu mẫu.

**Công ty thành viên:** [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [X] Khác: Vinpearl

**Ai đang đau (Actor)?**

- Nhân viên đặt phòng
- Nhân viên kinh doanh
- Công ty lữ hành

**Workflow thủ công hiện tại:**

1. Nhân viên nhận email đặt phòng đoàn.
2. Nhân viên đọc email và tệp đính kèm.
3. Nhân viên trích xuất ngày đến, ngày đi, số khách, loại phòng và yêu cầu đặc biệt.
4. Nhân viên kiểm tra thông tin còn thiếu hoặc mâu thuẫn.
5. Nhân viên nhập dữ liệu vào hệ thống và gửi email xác nhận.

**Bước tốn thời gian/lỗi nhất:**  
Bước 2 và 3: đọc email, tìm thông tin và nhập lại dữ liệu.  
Thời gian ước tính: khoảng **15 phút/email**, cần kiểm chứng bằng log xử lý.

**AI có thể hỗ trợ ở đâu?**

- Đọc email và tệp đính kèm.
- Trích xuất các trường thông tin đặt phòng.
- Đánh dấu trường còn thiếu hoặc mâu thuẫn.
- Tạo bản nháp email yêu cầu bổ sung thông tin.

**Đo thành công bằng gì?**

- Giảm thời gian xử lý từ **15 phút xuống dưới 5 phút/email**.
- Độ chính xác trích xuất các trường bắt buộc đạt tối thiểu **95%**.
- **100% trường thiếu hoặc mâu thuẫn** được đánh dấu để nhân viên kiểm tra.
- Không tự động xác nhận hoặc giữ phòng khi chưa có nhân viên duyệt.

**Quick Architecture:** [ ] No AI  [ ] Rule  [X] LLM Feature + Rule Validation  [ ] Agent

## QUICK PROBLEM CARD #3

**Bài toán:**  
Nhân viên tiếp nhận VinFast phải chuẩn hóa mô tả lỗi xe bằng ngôn ngữ đời thường và chuyển thông tin đến đúng nhóm kỹ thuật.

**Công ty thành viên:** [X] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác

**Ai đang đau (Actor)?**

- Khách hàng
- Nhân viên tổng đài/dịch vụ
- Kỹ thuật viên

**Workflow thủ công hiện tại:**

1. Khách hàng gọi hoặc gửi mô tả lỗi xe.
2. Nhân viên đọc và hỏi thêm triệu chứng.
3. Nhân viên ghi nhận thông tin vào phiếu dịch vụ.
4. Nhân viên phân loại lỗi và chuyển đến nhóm kỹ thuật.
5. Kỹ thuật viên kiểm tra và xác nhận nguyên nhân.

**Bước tốn thời gian/lỗi nhất:**  
Bước 2 và 4: hỏi lại, chuẩn hóa mô tả và phân loại nhóm kỹ thuật.  
Thời gian ước tính: khoảng **12 phút/trường hợp**, cần kiểm chứng bằng dữ liệu thực tế.

**AI có thể hỗ trợ ở đâu?**

- Tóm tắt triệu chứng khách hàng mô tả.
- Chuẩn hóa các thuật ngữ kỹ thuật.
- Đề xuất câu hỏi bổ sung.
- Gợi ý nhóm kỹ thuật tiếp nhận.
- Gắn cờ các trường hợp có dấu hiệu nguy hiểm.

**Đo thành công bằng gì?**

- Giảm thời gian tiếp nhận từ **12 phút xuống dưới 5 phút/trường hợp**.
- Độ chính xác phân loại nhóm kỹ thuật đạt tối thiểu **85%**.
- **100% trường hợp** liên quan đến phanh, pin, nhiệt độ hoặc va chạm được gắn cờ để nhân viên kiểm tra.
- AI không tự chẩn đoán cuối cùng hoặc hướng dẫn sửa chữa nguy hiểm.

**Quick Architecture:** [ ] No AI  [ ] Rule  [X] LLM Feature + Rule Safety Check  [ ] Agent

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---
