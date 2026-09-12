# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

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
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |VinFast |🔁 Repetitive + ⏱️ Time-consuming |Phân tích cảnh báo lỗi xe: Nhân viên phải đọc và đối chiếu hàng nghìn mã lỗi, log xe và lịch sử sửa chữa để xác định nguyên nhân. Ước tính có thể gây hàng nghìn giờ công/tháng. |
| 2 |Xanh SM |⏱️ Time-consuming + 👥 Stakeholder Pain |Xử lý khiếu nại chuyến đi: CSKH phải đọc complaint, kiểm tra GPS, lịch sử chuyến và thông tin tài xế để xác minh. Ước tính ~250 giờ công/ngày nếu xử lý 3.000 complaint/ngày. |
| 3 |Vinhomes |🔁 Repetitive + 🤖 AI-upgrade |Phân loại và chuyển tiếp yêu cầu cư dân: Nhân viên phải đọc từng ticket, xác định loại sự cố, tòa nhà, mức độ ưu tiên rồi chuyển cho bộ phận phù hợp. Ước tính ~420–670 giờ công/tháng. |
| 4 |Vinmec |🔁 Repetitive + ⏱️ Time-consuming |Trích xuất thông tin từ hồ sơ bệnh án: Nhân viên phải nhập thủ công dữ liệu từ giấy/PDF vào hệ thống. Với 2.000 hồ sơ/ngày và thêm 5 phút/hồ sơ, có thể tiêu tốn ~167 giờ công/ngày. |
| 5 |Vinpearl |⏱️ Time-consuming + 🤖 AI-upgrade |Xử lý câu hỏi khách hàng: Nhân viên phải tra cứu booking, chính sách, vé, ưu đãi và thông tin dịch vụ để trả lời từng yêu cầu. Với 4.000 yêu cầu/ngày × 4 phút, có thể tiêu tốn ~267 giờ công/ngày. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Tự động phân loại và hỗ trợ xử lí khiếu   │
│ nại của khách hàng sau mỗi chuyến đi.                       │
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH và khách hàng           │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│ 1. Nhận complaint ──> 2. Đọc nội dung ──> 3. Kiểm tra       │
│ lịch sử chuyến ──> 4. Xác minh ──> 5. Phản hồi khách hàng   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Đọc + xác minh complaint (~5 phút phút/lượt)                │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2-4: đọc complaint, tóm tắt, phân loại nguyên nhân,    │
│ xác định mức độ ưu tiên và đề xuất hướng xử lý.             │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│  Giảm thời gian xử lý complaint từ ~5 phút → <2 phút;       │
│ classification accuracy ≥90%; giảm 50% workload CSKH.       │
│                                                             │                                                       
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Tự động phân loại, ưu tiên và chuyển yêu cầu/khiếu nại      │
│ của cư dân đến đúng bộ phận xử lý.                          │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [X] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên CSKH/Ban quản lý và cư dân                        │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│ 1. Nhận ticket → 2. Đọc nội dung → 3. Phân loại sự cố       │
│ → 4. Xác định bộ phận → 5. Chuyển ticket                    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Phân loại + routing ticket (~5 phút/lượt)                   │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2-4: hiểu nội dung cư dân, xác định intent, địa điểm,  │
│ mức độ ưu tiên và bộ phận phụ trách.                        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian phân loại từ ~5 phút → <30 giây;             │
│ routing accuracy ≥90%; giảm 50% workload CSKH.              │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Tự động hỗ trợ trả lời các câu hỏi của khách về booking,    │
│ dịch vụ, chính sách và ưu đãi.                              │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [X] Khác: Vinpearl         │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên CSKH và khách du lịch                             │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│ 1. Nhận câu hỏi → 2. Đọc và hiểu yêu cầu → 3. Tra cứu       │
│ booking/chính sách → 4. Soạn câu trả lời → 5. Gửi khách     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Tra cứu thông tin + soạn phản hồi (~4 phút/lượt)            │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2-4: hiểu intent, truy xuất thông tin liên quan và     │
│ tạo draft response cho nhân viên CSKH.                      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian soạn phản hồi từ ~4 phút → <1 phút;          │
│ ≥90% câu hỏi được xử lý đúng intent; giảm 50% workload.     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

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

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 3.6 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

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

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
