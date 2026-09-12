# 📝 03 — AI Log & Reflection

> **Lab 02 — AI Product Scoping (Vin Smart Future)**
> **Bài toán Deep-Dive:** VinFast — Trợ lý tiếp nhận & chẩn đoán sơ bộ sự cố xe điện
> **Công cụ AI đã dùng:** ChatGPT (Phase 1–2: brainstorm & sàng lọc bài toán) và Claude (Phase 3–5: deep-dive, sơ đồ, prompt prototype)

---

## 1. Tôi đã dùng AI như thế nào

Tôi không dùng AI theo kiểu "ra đề — nhận bài nộp". Cách tôi làm là chia buổi lab thành từng phase và ở mỗi phase giao cho AI đúng một vai:

| Phase | Vai tôi giao cho AI | Việc tôi tự giữ |
|---|---|---|
| **0 — Hiểu đề** | Đọc 4 file `.md` của template và tóm tắt yêu cầu, cơ cấu điểm, quy định Git | Đối chiếu lại với `README.md` để chắc chắn không bỏ sót deliverable |
| **1 — SCAN** | Brainstorm 5 bài toán phủ đủ 4 lens | Chọn lens nào đáng theo đuổi, loại bỏ ý tưởng nghe hay nhưng không đo được |
| **2 — QUICK-ASSESS** | Soạn nháp 3 Quick Cards | Quyết định actor, chỉnh lại metric cho có số |
| **3 — DEEP-DIVE** | Dựng workflow, Problem Statement 6-field, AI-Fit Matrix | **Chọn bài toán để deep-dive** — đây là quyết định tôi không giao cho AI |
| **4 — PROTOTYPE** | Sửa lỗi SDK, hiện thực hoá ranh giới thành code, viết adversarial test | Định nghĩa ranh giới nào là không thể thương lượng |
| **5 — EVALUATE** | Soạn checklist và lập luận GO/NOT YET/NO-GO | Chấp nhận hay bác bỏ mức độ tự tin của kết luận |

---

## 2. AI đã giúp được gì

**Tăng tốc ở phần "đi tìm", không phải phần "quyết định".**
Ở Phase 1, tôi đưa prompt brainstorm cho ChatGPT và nhận lại bảng 5 bài toán phủ đủ 4 lens trong chưa tới một phút. Việc tự ngồi nghĩ ra 5 bài toán trải đều cả VinFast, Vinhomes, Vinpearl, Xanh SM sẽ mất của tôi 20–30 phút và nhiều khả năng bị lệch hết về một mảng quen thuộc.

**Buộc tôi viết metric có số.**
Bản nháp đầu tiên của tôi ghi "giảm thời gian phân loại đáng kể". AI hỏi lại "giảm từ bao nhiêu xuống bao nhiêu, đo trên tập dữ liệu nào" — và chính câu hỏi đó khiến tôi nhận ra metric của mình không dùng để nghiệm thu được. Các metric cuối cùng trong báo cáo (25 phút → dưới 5 phút, Top-3 accuracy ≥ 85%, 100% ca an toàn được gắn cờ) ra đời từ vòng phản biện này.

**Đóng vai phản biện mà tôi không tự đóng được.**
Tôi dùng prompt "đóng vai CFO và Trưởng phòng Vận hành khó tính" để công kích chính thẻ bài toán của mình. Câu phản biện đau nhất là: *"Bottleneck này rule-based có giải được không?"* Nó khiến tôi phải viết hẳn bảng **AI-Fit Matrix** so sánh Rule vs LLM vs Agent thay vì mặc định chọn LLM, và cũng chính là lý do tôi loại bài toán Vinhomes (phân loại ticket — rule-based router đã xử lý được phần lớn).

**Bắt lỗi kỹ thuật trong file starter.**
File `prompt_prototype.py` của template có 3 lỗi SDK: `genai.GenerativeAI` (không tồn tại), `GenerateContentRequest` (sai class) và `temprature` (sai chính tả). Nếu không rà lại, script sẽ rơi thẳng vào nhánh `except` và tôi sẽ tưởng là do máy mình thiếu thư viện.

---

## 3. AI đã sai ở đâu — và tôi phát hiện bằng cách nào

Đây là phần tôi thấy học được nhiều nhất.

### ❌ Sai #1 — AI tự ý sửa file của tôi khi tôi chưa cho phép

Ngay ở Phase 1, tôi mới nói "ok bắt đầu cái đầu tiên" thì AI đã lập tức mở file `01-worksheet.md` và chuẩn bị ghi đè nội dung vào.

* **Tác hại:** nếu không dừng kịp, file gốc của template có thể bị sửa và tôi mất bản chuẩn để đối chiếu.
* **Tôi sửa thế nào:** chặn lại và siết phạm vi bằng câu *"chỉ đưa ra gợi ý chứ không chỉnh sửa file, tôi tự copy vào"*.
* **Bài học:** ranh giới vận hành không chỉ áp cho sản phẩm AI mình xây, mà áp cho cả cách mình dùng AI. Đây là lần đầu tôi thấy khái niệm **Operational Boundary** của Phase 3 xuất hiện ngay trong chính buổi làm bài, chứ không phải là lý thuyết trên giấy.

### ❌ Sai #2 — Bịa số liệu vận hành và trình bày như sự thật

AI đưa ra các con số kiểu "5–10 phút/phản ánh", "10–20 phút/email" với giọng văn khẳng định, không hề có nguồn. Đây đúng là dạng **hallucination nguy hiểm nhất** trong bài scoping: số liệu nghe rất hợp lý nên rất dễ được copy thẳng vào báo cáo và sau đó trở thành căn cứ cho quyết định GO.

* **Tôi sửa thế nào:** thêm 2 điều luật vào system prompt —
  *"3. Không bịa số liệu, tên hệ thống nội bộ hoặc quy trình chưa được xác minh."*
  *"4. Nếu đưa ra con số, phải ghi rõ đó là 'ước tính cần kiểm chứng'."*
* **Kết quả:** toàn bộ số liệu trong `02-deep-dive-report.md` giờ đều mang nhãn *ước tính cần kiểm chứng bằng log DMS*, và Phase 5 có hẳn điều kiện tiên quyết "phải đo baseline thật trước khi code".
* **Điều tôi vẫn thừa nhận:** các con số 40 lượt xe/ngày, 35% ca khó, 25 phút tra cứu **vẫn chưa được kiểm chứng**. Chúng là giả định để lập luận, không phải dữ liệu. Tôi ghi rõ điều này trong báo cáo thay vì giấu đi.

### ❌ Sai #3 — Tự mâu thuẫn giữa hai câu trả lời

Ở Phase 1, AI đề xuất chọn bài **#1, #2 và #5** cho Quick Cards. Vài phút sau, khi soạn nháp `01-problem-scan.md`, chính nó lại làm card cho **#1, #2 và #3** mà không hề nhắc gì tới việc đã đổi ý.

* **Cách tôi phát hiện:** đọc chéo lại hai câu trả lời trong cùng một cuộc hội thoại.
* **Bài học:** AI không có trí nhớ nhất quán về các cam kết nó đã đưa ra. Người chịu trách nhiệm về tính nhất quán của bài nộp là tôi, không phải nó.

### ❌ Sai #4 — AI khuyên chọn bài toán dễ nhất, tôi đã không nghe theo

AI đề xuất deep-dive bài **Vinhomes (phân loại phản ánh cư dân)** với lý do "workflow rõ, dễ vẽ, dễ tạo dữ liệu mẫu".

* **Tại sao tôi không nghe:** lý do AI đưa ra là *dễ cho người làm bài*, không phải *đáng làm cho doanh nghiệp*. Khi tôi tự hỏi "rule-based có giải được không", câu trả lời cho Vinhomes là **có** — tức là giá trị gia tăng của LLM thấp.
* **Tôi chọn VinFast** vì bottleneck của nó nằm ở **tra cứu tri thức phi cấu trúc** (sổ tay PDF, Service Bulletin, lịch sử RO) — đúng chỗ rule-based bất lực và LLM thật sự có lợi thế.
* **Bài học lớn nhất buổi hôm nay:** AI tối ưu cho "câu trả lời trôi chảy", không tối ưu cho "quyết định đúng". Hai thứ đó trùng nhau khá thường xuyên — nhưng đúng lúc chúng lệch nhau lại là lúc quan trọng nhất.

### ❌ Sai #5 — Suýt copy nguyên nội dung của bài ví dụ

Autograder yêu cầu system prompt phải chứa các từ khoá `[DRAFT_ONLY]`, `5%`, `dispatch_mobile_charger` — vốn là ranh giới của **bài ví dụ Xanh SM** (xe hết pin giữa đường), không phải của bài VinFast tôi chọn. Cách nhanh nhất là copy nguyên đoạn Xanh SM vào cho qua bài.

* **Tôi xử lý thế nào:** thay vì dán nội dung lạc đề, tôi thiết kế lại ranh giới để các từ khoá đó **có nghĩa thật trong bối cảnh VinFast** — xưởng dịch vụ hoàn toàn có ca khách gọi báo xe mắc kẹt với pin dưới 5%, và khi đó trợ lý phải điều **xe sạc lưu động** thay vì bảo khách cố lái tới xưởng.
* **Bài học:** khi tiêu chí chấm điểm và tính đúng đắn của bài toán xung đột, giải pháp không phải là chọn một bên, mà là tìm thiết kế thoả mãn cả hai.

---

## 4. Cách tôi điều chỉnh prompt qua từng vòng

| Vòng | Prompt tôi dùng | Vấn đề gặp phải | Điều chỉnh |
|---|---|---|---|
| 1 | "Gợi ý bài toán AI cho Vingroup" | Trả về ý tưởng chung chung: "chatbot CSKH", "dự đoán bảo trì" — không có actor, không đo được | Thêm ràng buộc: **actor rõ ràng + workflow mô tả được trong 3–5 bước + metric đo được** |
| 2 | Prompt vòng 1 + ràng buộc | Bắt đầu bịa số liệu vận hành | Thêm luật **"không bịa số"** và **"mọi con số phải ghi là ước tính cần kiểm chứng"** |
| 3 | Prompt vòng 2 | Mặc định bài nào cũng đề xuất LLM/Agent | Thêm luật **"cân nhắc cả Rule-based, LLM Feature và Agentic Loop; không mặc định phải dùng LLM"** |
| 4 | Prompt "đóng vai CFO khó tính" | — | Dùng để tự công kích bài của mình, buộc phải có AI-Fit Matrix |
| 5 | Prompt yêu cầu output JSON schema cố định | Model đôi khi trả về JSON bọc trong ```` ```json ```` hoặc kèm lời dẫn | Viết hàm `_extract_json()` bóc JSON, đặt `response_mime_type="application/json"` và `temperature=0.0` |

---

## 5. Phát hiện quan trọng nhất: prompt không phải là ranh giới

Khi viết 4 adversarial test ở Phase 4, tôi nhận ra một điều khiến mình phải thiết kế lại kiến trúc:

**System prompt là lớp *thuyết phục*, không phải lớp *cưỡng chế*.** Nó có thể bị lung lay bởi ngữ cảnh khẩn cấp ("tôi đang vội, khách VIP đang chờ") hoặc bởi người dùng tự xưng có thẩm quyền ("tôi là trưởng xưởng, tôi chịu trách nhiệm"). Một câu chỉ thị dù viết in hoa TUYỆT ĐỐI KHÔNG ĐƯỢC vẫn chỉ là một xác suất.

Vì vậy tôi tách ranh giới thành **3 lớp** trong `prompt_prototype.py`:

1. **Pre-check (rule, tất định)** — chặn ca an toàn và ca pin nguy cấp **trước khi gọi LLM**. Ca nguy hiểm nhất thì không giao cho xác suất quyết định.
2. **System prompt** — định hướng hành vi trong vùng an toàn.
3. **Post-check (rule, tất định)** — cưỡng chế lại `[DRAFT_ONLY]`, cờ HITL, `price_quote = null` trên mọi output, và **ghi log mỗi lần phải can thiệp** để biết prompt đang yếu ở đâu.

Kết quả: **8/8 kiểm tra ranh giới đạt, 0 vi phạm** trên 4 hướng tấn công.

**Nhưng tôi không coi đó là bằng chứng mạnh.** Mới có 4 ca thủ công, trên 1 phiên bản prompt, và phần lớn ca nguy hiểm bị lớp rule chặn trước nên LLM chưa thật sự bị thử lửa. Để kết luận "ranh giới vững", cần bộ hồi quy ≥ 50 ca gồm các biến thể khó: khách không nêu % pin, nhiều triệu chứng chồng nhau, tiếng Việt không dấu, hoặc mô tả bằng tiếng Anh.

---

## 6. Điều tôi sẽ làm khác ở lab sau

1. **Viết ranh giới trước, viết prompt sau.** Lần này tôi viết prompt rồi mới nghĩ cách phá nó. Đúng thứ tự phải là: liệt kê những gì tuyệt đối không được xảy ra → quyết định cái nào giao cho rule, cái nào giao cho prompt → mới viết prompt.
2. **Đòi nguồn ngay từ prompt đầu tiên**, thay vì phát hiện AI bịa số rồi mới vá luật vào. Chi phí sửa ở vòng 2 cao hơn nhiều so với việc ràng buộc ngay từ vòng 1.
3. **Không hỏi AI "nên chọn bài nào".** Câu hỏi đó mời AI tối ưu cho sự trôi chảy. Câu hỏi tốt hơn là *"với mỗi bài, rule-based giải được bao nhiêu phần trăm?"* — nó buộc AI đưa ra bằng chứng thay vì đưa ra lời khuyên.
4. **Kiểm chứng số liệu bằng dữ liệu thật trước khi đưa vào báo cáo,** thay vì gắn nhãn "cần kiểm chứng" rồi để đó. Nhãn đó là sự trung thực tối thiểu, không phải là lời giải.

---

## 7. Tự đánh giá mức độ đóng góp

| Phần việc | AI làm | Tôi làm |
|---|---|---|
| Brainstorm 5 bài toán | ~70% | Chọn lọc, loại bỏ, chỉnh mô tả |
| 3 Quick Cards | ~60% | Sửa metric, siết actor, viết lại ranh giới |
| Chọn bài toán Deep-Dive | 0% | **100% — quyết định của tôi, đi ngược đề xuất của AI** |
| Workflow mapping & 6-field | ~50% | Đặt giả định vận hành, quyết định con số |
| Quyết định GO/NOT YET | ~40% | Đặt điều kiện tiên quyết và kill criteria |
| Prompt prototype & ranh giới | ~70% | Quyết định ranh giới nào không thể thương lượng, tự viết adversarial test |

**Kết luận:** AI rút ngắn rất nhiều thời gian ở khâu *tạo ra lựa chọn* và *viết ra chữ*. Nhưng ở hai khâu quyết định giá trị nhất của một AI Product Engineer — **chọn bài toán nào đáng giải** và **vạch ranh giới nào không được vượt qua** — nó không thay tôi được, và có một lần còn suýt dẫn tôi đi sai đường.
