# 01-problem-scan.md — Ý tưởng cá nhân (SCAN & QUICK-ASSESS)

> 
> * **Họ và tên:** Nguyễn Đức Long
> * **MSSV:** 2A202602917  
> * **Mảng kinh doanh lựa chọn:** GSM (Xanh SM) / VinFast / Vinhomes / Vinmec / Vinpearl  

---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là **Nguyễn Đức Long**, AI Engineer tại **Vin Smart Future**. Tôi được giao nhiệm vụ tìm kiếm, khảo sát và scoping các cơ hội tối ưu hóa bằng trí tuệ nhân tạo (AI) cho các công ty thành viên trong tập đoàn Vingroup (GSM, VinFast, Vinhomes, Vinmec, Vinpearl) nhằm nâng cao hiệu suất vận hành và trải nghiệm khách hàng.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Pain từ người khác) quét qua hoạt động vận hành của các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Xanh SM** | Lặp lại | So khớp, phân loại và gán nhãn tự động các ticket khiếu nại của tài xế/khách hàng qua kênh Chat/Callbot. |
| 2 | **Xanh SM** | Tốn thời gian | Điều phối viên xử lý thủ công các phản hồi khẩn cấp từ tài xế về sự cố sạc pin hoặc cạn pin thực địa (mất 15-20 min/lượt). |
| 3 | **VinFast** | Stakeholder Pain | Tổng hợp log lỗi kỹ thuật xe điện (DTC Log) và đối chiếu với Manual dịch vụ để gợi ý chẩn đoán sửa chữa cho kỹ thuật viên. |
| 4 | **Vinhomes** | Time-consuming / AI-upgrade | Phân tích khiếu nại/góp ý của cư dân trên App Vinhomes Resident và tự động soạn bản thảo phản hồi chuẩn mực theo Quy định KĐT (BQL mất 15-30 phút/phản ánh). |
| 5 | **Vinmec** | Tốn thời gian | Bác sĩ mất nhiều thời gian tóm tắt hồ sơ bệnh án cũ (EMR) và lịch sử xét nghiệm của bệnh nhân trước khi nhập viện (mất 20-30 phút/bệnh nhân). |
| 6 | **Vinpearl** | AI-upgrade | Trợ lý AI tư vấn lịch trình vui chơi VinWonders và gợi ý đặt phòng theo thời tiết, số lượng trẻ em/người lớn đi kèm. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN: **#1 (Xanh SM Khiếu nại ticket), #2 (Xanh SM Sự cố sạc pin), #4 (Vinhomes Trả lời cư dân).**

---

## Card #1 — Xanh SM Xử lý & Phân loại Ticket khiếu nại CSKH

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Đọc hiểu transcript, phân loại mức độ khẩn cấp   │
│ và soạn bản thảo phản hồi ticket khiếu nại cho Xanh SM.     │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? CSKH Tier-1 (quá tải), Khách hàng (chờ lâu)    │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách hàng/Tài xế gửi khiếu nại qua App/Hotline        │
│   → 2. CSKH đọc thủ công transcript & tra cứu chuyến xe     │
│   → 3. Gán nhãn loại sự cố (Sai cước, Thái độ, Tai nạn...)   │
│   → 4. Soạn văn bản phản hồi và đề xuất mức bồi thường       │
│                                                             │
│ Bước nào tốn nhất? Bước 2 & 4 (⏱ 10 phút/ticket)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3, 4          │
│ (Trích xuất intent -> Auto tag -> Draft phản hồi)           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian xử lý ticket (TTR) từ 10 min ──> under 2.5 min.│
│                                                             │
│ Quick Architecture: [x] Agent (RAG + Function Calling)      │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #2 — Xanh SM Xử lý sự cố sạc pin thực địa

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Tài xế Xanh SM báo cáo sự cố sạc pin / hết pin    │
│ giữa đường cần điều phối cứu hộ hoặc trạm sạc gần nhất.     │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? Tài xế (chờ đợi), Điều phối viên (quá tải)     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tài xế gọi tổng đài điều vận báo hết pin               │
│   → 2. Điều phối viên tra cứu thủ công vị trí xe trên bản đồ│
│   → 3. Tra cứu thủ công các trạm sạc VinFast còn trụ trống   │
│   → 4. Viết tin nhắn chỉ dẫn/đường đi gửi qua App tài xế    │
│   → 5. Liên hệ đội xe cứu hộ nếu xe đã cạn kiệt pin         │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 12 phút/lượt)                │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│ (Tự động hóa lấy vị trí -> Tra cứu trạm trống -> Draft tin) │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian xử lý sự cố từ 15 phút ──> dưới 3 phút.      │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Tự động soạn chỉ dẫn)   │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #4 — Vinhomes Tự động hóa bản thảo phản hồi ý kiến cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
│                                                             │
│ Bài toán: Phân tích phản ánh của cư dân trên App Vinhomes   │
│ Resident và tự động soạn thảo văn bản phản hồi đúng nội quy.│
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau? Nhân viên Ban Quản Lý (BQL), Cư dân             │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi phản ánh/khiếu nại qua App Vinhomes        │
│   → 2. BQL đọc nội dung và phân loại bài toán (Ồn, Rác...)  │
│   → 3. Tra cứu Sổ tay Cư dân/Nội quy KĐT tương ứng           │
│   → 4. Soạn thảo email/thông báo trả lời chính thức          │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 15 phút/phản ánh)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│ (RAG tra cứu nội quy -> AI Draft phản hồi chuẩn mực)        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian phản hồi ban đầu từ 24 giờ ──> dưới 30 phút. │
│                                                             │
│ Quick Architecture: [x] LLM Feature (RAG + Prompting)        │
└─────────────────────────────────────────────────────────────┘
```

