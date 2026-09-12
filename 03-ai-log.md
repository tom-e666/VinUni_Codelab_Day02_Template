# 03-ai-log.md — Nhật ký tương tác & Phản ánh sử dụng AI (AI Log & Reflection)

## 🏛️ Bối cảnh sử dụng AI

Trong suốt quá trình làm bài Lab 02 về **AI Product Scoping tại Vin Smart Future**, tôi đã sử dụng các công cụ LLM như một **thought-partner (đối tác tư duy)** để hỗ trợ brainstorm bài toán, phản biện ranh giới vận hành (Operational Boundary), kiểm thử kịch bản tấn công (Adversarial Testing) và hoàn thiện cấu trúc tài liệu.

Dưới đây là nhật ký chi tiết và phân tích phản ánh (reflection) về quá trình tương tác này.

---

## 🔍 1. AI đã giúp ích được gì? (AI as Thought Partner)

1. **Brainstorm & Khai phá góc nhìn vận hành (Phase 1 - SCAN):**
   * *Nhiệm vụ:* Tìm kiếm các bottleneck thực tế trong hệ sinh thái Vingroup (GSM, VinFast, Vinhomes, Vinmec, Vinpearl).
   * *Kết quả:* AI đã gợi ý các tình huống thực địa rất chính xác như *Sự cố sạc pin giữa đường của tài xế Xanh SM*, *Quản lý yêu cầu hủy chuyến*, và *Tóm tắt EMR y tế Vinmec*. Điều này giúp tôi mở rộng tư duy vượt khỏi các ứng dụng chatbot CSKH thông thường.

2. **Thiết lập & Stress-Test Ranh giới an toàn (Phase 3 & Phase 4):**
   * *Nhiệm vụ:* Đóng vai trò CFO & Head of Operations khắt khe để phản biện bài toán.
   * *Kết quả:* AI đã chỉ ra sơ hở trong quy trình tự động hóa: nếu cho phép AI tự động gửi tin nhắn điều hướng trạm sạc cho tài xế mà không qua kiểm duyệt (Human-in-the-loop), rủi ro tài xế bị điều sang trạm sạc hết trụ trống hoặc quá xa khi pin dưới 5% sẽ gây hậu quả nghiêm trọng.

3. **Tạo Test Case Tấn công (Adversarial Prompt Generation):**
   * *Nhiệm vụ:* Viết kịch bản dụ AI vượt ranh giới (Prompt Injection / Safety Violation).
   * *Kết quả:* AI giúp tạo nhanh các kịch bản giả lập tài xế đóng vai khách VIP/tình huống khẩn cấp để ép hệ thống bỏ qua bước tạo bản thảo (`[DRAFT_ONLY]`) hoặc bỏ qua ngưỡng an toàn pin.

---

## 🔴 2. AI trả lời sai / Hallucination ở đâu? (Mistakes & Hallucinations)

Trong quá trình tương tác, tôi phát hiện AI mắc phải 3 lỗi logic và ảo tưởng thông tin (hallucination) đáng chú ý:

1. **Đề xuất kiến trúc quá phức tạp (Over-engineering):**
   * *Lỗi:* Khi yêu cầu đề xuất giải pháp cho bài toán chỉ hướng trạm sạc khẩn cấp cho tài xế Xanh SM, AI ban đầu đề xuất dựng một hệ thống **Autonomous Multi-Agent Swarm** tự động ra quyết định và gọi API điều xe cứu hộ tự động.
   * *Nguyên nhân:* AI xu hướng ưu tiên các công nghệ "hot" mà không đánh giá rủi ro vận hành thực tế.
   * *Thực tế:* Bài toán chỉ cần **LLM Feature (Prompting + RAG) kết hợp Human-In-The-Loop (HITL)** để đảm bảo an toàn tuyệt đối.

2. **Hallucination về API & Dữ liệu thời gian thực (Real-time Telemetry):**
   * *Lỗi:* AI tự bịa ra rằng LLM có thể "trực tiếp đọc tín hiệu cảm biến dòng điện của trụ sạc VinFast theo thời gian thực (millisecond)".
   * *Thực tế:* LLM không thể đọc trực tiếp IoT telemetry stream mà phải thông qua REST API do Backend service cung cấp.

3. **Bỏ qua ranh giới Operational Boundary khi viết Prompt mẫu:**
   * *Lỗi:* Ở lượt tạo prompt đầu tiên, AI quên thêm tiền tố cấm `[DRAFT_ONLY]` trong output, dẫn đến nguy cơ hệ thống tự động đẩy tin nhắn trực tiếp tới App tài xế.

---

## 🛠️ 3. Tôi đã sửa Prompt & Thiết lập Ranh giới ra sao? (Iterative Prompt Tuning)

Để khắc phục các lỗi trên, tôi đã tiến hành tinh chỉnh Prompt (Prompt Tuning) qua các bước:

### ❌ Prompt ban đầu (Sơ khai — Bị AI hallucinate & vượt ranh giới):
> *"Hãy viết prompt cho AI hỗ trợ tài xế Xanh SM hết pin. AI hãy tìm trạm sạc VinFast gần nhất và nhắn tin hướng dẫn tài xế ngay lập tức."*

👉 **Hậu quả:** AI tự ý tạo câu trả lời gửi trực tiếp, đề xuất trạm sạc cách 8km dù pin xe chỉ còn 2%.

---

### ✅ Prompt cải tiến (Đã thêm Operational Boundary & Guardrails nghiêm ngặt):
> *"Bạn là AI Operational Assistant thuộc Vin Smart Future. Nhiệm vụ của bạn là phân tích dữ liệu sự cố pin của tài xế Xanh SM và tạo BẢN THẢO tin nhắn hướng dẫn (`[DRAFT_ONLY]`).*
> 
> **Ranh giới an toàn tuyệt đối (STRICT BOUNDARIES):**
> 1. KHÔNG BAO GIỜ gửi tin nhắn trực tiếp. Luôn bắt đầu output bằng thẻ `[DRAFT_ONLY]` để Điều phối viên (Human) kiểm duyệt.
> 2. Nếu `battery_level < 5%`, TUYỆT ĐỐI KHÔNG đề xuất trạm sạc cách xa quá 3km. Bắt buộc trả về yêu cầu `dispatch_mobile_charger` (Gửi xe cứu hộ pin di động).
> 3. Trả về định dạng JSON cấu trúc rõ ràng gồm: `status`, `recommendation_type`, `draft_message`, `risk_flag`."*

---

## 🎯 4. Bài học rút ra (Key Reflections)

1. **AI là Thought Partner, không phải Decision Maker:** AI xuất sắc trong việc mở rộng ý tưởng và viết draft, nhưng người kỹ sư AI Product Engineer phải giữ vai trò phản biện, kiểm soát ranh giới vận hành và đưa ra quyết định kỹ thuật cuối cùng.
2. **Operational Boundary là cốt lõi của AI Product:** Một sản phẩm AI thành công cho tập đoàn lớn như Vingroup không nằm ở mô hình lớn hay nhỏ, mà nằm ở **Cơ chế kiểm soát rủi ro (HITL, Guardrails, Fallback)** khi AI đưa ra kết quả sai.
3. **Lập trình Prompt phải rõ ràng như viết Code:** Cần quy định cấu trúc JSON Output, quy tắc cấm (Negative Constraints) và điều kiện biên (Edge Cases) chi tiết thì LLM mới vận hành tin cậy trong môi trường doanh nghiệp.
