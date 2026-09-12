# 03 — AI Log & Reflection

## Bối cảnh

Trong bài lab, tôi sử dụng AI như một thought-partner để tìm kiếm bài toán vận hành, phản biện Quick Problem Card và kiểm tra bản mẫu prompt. Nhóm cuối cùng chọn bài toán VinFast: hỗ trợ tiếp nhận và chẩn đoán sơ bộ sự cố xe điện.

## AI đã hỗ trợ những gì?

AI giúp tôi mở rộng danh sách pain point theo bốn lens: công việc lặp lại, tốn thời gian, có thể nâng cấp bằng AI và gây khó khăn cho stakeholder. Từ đó tôi xây dựng các bài toán cho Vinhomes, Vinpearl, VinFast và Xanh SM.

AI cũng giúp chuẩn hóa Quick Problem Card theo các trường actor, workflow, bottleneck, metric và kiến trúc. Khi phản biện, AI chỉ ra rằng bài toán phân loại phản ánh Vinhomes có thể giải quyết phần lớn bằng rule-based router, trong khi bài toán VinFast phù hợp hơn với LLM Feature kết hợp RAG vì dữ liệu mô tả lỗi và tài liệu kỹ thuật có tính phi cấu trúc.

Trong phần Deep-Dive, AI hỗ trợ phân rã quy trình thành các bước, xác định handoff và bottleneck, đề xuất metric như thời gian chẩn đoán, Top-3 accuracy và tỷ lệ phát hiện ca an toàn. AI cũng gợi ý Human-in-the-loop, fallback về quy trình thủ công và giới hạn không cho mô hình tự chốt chẩn đoán, báo giá hoặc đặt phụ tùng.

## Ví dụ prompt đã sử dụng

```text
Đây là Quick Problem Card của tôi. Hãy đóng vai CFO và Trưởng phòng Vận hành
khắt khe. Chỉ ra điểm yếu về logic, metric và giải thích khi nào rule-based
phù hợp hơn LLM. Hãy đề xuất cách sửa có thể đo lường được.
```

```text
Hãy thiết kế future-state flow cho bài toán hỗ trợ tiếp nhận lỗi xe VinFast.
Phân biệt rõ AI step, Human-in-the-loop, safety escalation và fallback.
AI không được đưa ra kết luận chẩn đoán cuối cùng hoặc tự gửi báo giá.
```

## Lỗi hoặc hallucination đã phát hiện

AI ban đầu có xu hướng đưa ra các con số như thời gian xử lý, số lượng ca mỗi ngày và tỷ lệ tiết kiệm mà không có dữ liệu doanh nghiệp xác minh. Tôi không sử dụng các con số đó như sự thật; các số liệu trong báo cáo được ghi rõ là “ước tính cần kiểm chứng” và cần đối chiếu với log DMS, phiếu sửa chữa và dữ liệu thực tế của xưởng.

AI cũng từng mở rộng phạm vi bài toán quá mức, ví dụ đề xuất để mô hình tự chẩn đoán, tự gửi tin nhắn hoặc tự xác nhận kết quả. Đây là rủi ro nghiêm trọng trong lĩnh vực xe điện. Tôi đã thu hẹp nhiệm vụ thành tạo bản nháp, trích dẫn tài liệu, gắn cờ an toàn và đề xuất câu hỏi bổ sung; cố vấn dịch vụ và kỹ thuật viên vẫn là người phê duyệt.

Trong quá trình lập trình, hàm gọi Gemini ban đầu dùng sai API `genai.GenerativeAI`, `GenerateContentRequest` và tham số `temprature`. Tôi đã sửa sang `genai.Client`, `GenerateContentConfig`, `temperature` và `client.models.generate_content`. Điều này cho thấy output của AI về code phải được kiểm tra bằng tài liệu SDK và chạy thử, không nên sao chép mù quáng.

Ngoài ra, system prompt ban đầu còn trộn giữa nhiệm vụ brainstorm Phase 1 và ranh giới an toàn của prototype VinFast. Đây là lỗi về phạm vi. Prompt sản phẩm cần tập trung vào một use case, định dạng output, nguồn dữ liệu được phép sử dụng, nhãn `[DRAFT_ONLY]`, điều kiện `ESCALATE` và trạng thái `INSUFFICIENT_EVIDENCE`.

## Cách tôi kiểm soát AI

- Ghi rõ giả định và đánh dấu mọi số liệu chưa được xác minh.
- Yêu cầu AI nêu nguồn hoặc trả về `INSUFFICIENT_EVIDENCE` khi không có căn cứ.
- Tách rule an toàn khỏi phần diễn giải ngôn ngữ của LLM.
- Bắt buộc output là bản nháp và phải qua Human-in-the-loop.
- Dùng adversarial test để thử yêu cầu bỏ qua phê duyệt hoặc đề xuất trạm sạc nguy hiểm.
- Chạy code và kiểm tra lỗi SDK thay vì chỉ đánh giá câu trả lời bằng cảm nhận.

## Đánh giá cuối cùng

AI hữu ích nhất ở giai đoạn khám phá, phản biện và chuyển mô tả tự nhiên thành cấu trúc có thể kiểm tra. AI không thay thế việc xác minh dữ liệu vận hành, phê duyệt an toàn hay quyết định kinh doanh. Vì vậy, quyết định GO trong báo cáo là GO có điều kiện: phải có baseline thực tế, tập phiếu RO được gán nhãn, kho tài liệu kỹ thuật được kiểm soát và các cổng duyệt của con người trước khi triển khai.
