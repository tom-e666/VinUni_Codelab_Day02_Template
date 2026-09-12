# 🔍 Phase 1 — SCAN & QUICK-ASSESS (Vin Smart Future)

---

## 📝 1. Danh sách 5 Bài toán Vận hành (Problem List)

| # | Subsidiary (Công ty) | Lens (Ống kính) | Mô tả ngắn bài toán & Bottleneck |
|---|---|---|---|
| 1 | **VinFast – Xưởng dịch vụ** | 🔁 **Repetitive** (Lặp lại) | **Gọi điện chăm sóc sau sửa chữa/bảo dưỡng cho từng khách hàng:** Quy trình VinFast quy định khách làm dịch vụ được liên hệ để ghi nhận phản hồi sau khi xe ra xưởng; khi mạng lưới đạt 350 xưởng dịch vụ (11/2025), đây là một workflow lặp lại quy mô lớn. |
| 2 | **VinFast – After-sales** | ⏱ **Time-consuming** (Tốn thời gian) | **Tiếp nhận và chẩn đoán xe trước sửa chữa:** Khách mô tả lỗi + gửi hình ảnh; xưởng phải tiếp nhận, đánh giá tình trạng, xác định hạng mục, thời gian sửa chữa và báo giá. Các ca "chẩn đoán khó" gây tốn nhiều thời gian của kỹ thuật viên. |
| 3 | **Xanh SM** | 😣 **Stakeholder Pain** (Nỗi đau) | **ETA và điểm đón chưa chính xác làm khách chờ/tài xế tìm khách:** Review App Store 17/12/2025 ghi nhận ETA 5 phút biến thành 30 phút. Phản ánh khác cho thấy app xác định sai vị trí đón 3 lần liên tiếp tại cùng địa điểm. |
| 4 | **Vinhomes** | 😣 **Stakeholder Pain** + ⏱ **Time-consuming** | **Đồng bộ thông tin cư dân/thẻ ra vào/thẻ gửi xe kéo dài:** Review Vinhomes Resident 25/8/2026 phản ánh quá trình đồng bộ app mất 1 tuần, cư dân chưa làm được thẻ gửi xe và phải trả 32.000đ/tối tiền gửi xe vãng lai. |
| 5 | **Vinhomes** | 🤖 **AI-upgrade** (AI làm tốt hơn) | **Luồng đặt tiện ích trên app còn friction:** Review 4/8/2026 phản ánh trải nghiệm "đặt lịch tiện ích trên app" rất bất tiện. Cư dân gặp khó khăn khi thao tác hoặc phải chờ BQL hỗ trợ thủ công. |

---

## 🃏 2. Top 3 Quick Problem Cards (Phase 2)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                       │
│                                                                             │
│ Bài toán (1 câu): Đặt vị trí đón thực tế & tính toán ETA chính xác cho Xanh SM│
│ Công ty thành viên: [x] Xanh SM (GSM)                                       │
│                                                                             │
│ Ai đang đau (Actor): Khách hàng đi taxi/xe máy điện và Tài xế Xanh SM.       │
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Khách đặt xe ──> 2. App ghim GPS thô ──> 3. Tài xế đi theo map ──>    │
│   4. Gọi điện tìm nhau tại điểm đón (cổng TTTM/chung cư).                  │
│                                                                             │
│ Bước tốn thời gian/lỗi nhất: Tài xế dò tìm điểm đón thực tế (⏱ 10-15 min).   │
│ AI nhảy vào ở bước nào: AI đọc GPS + lịch sử đón ──> Chuẩn hóa điểm đón thực│
│                                                                             │
│ Đo thành công bằng gì: Giảm thời gian chờ/tìm điểm đón từ 10 min ──> < 2 min. │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                       │
│                                                                             │
│ Bài toán: Hỗ trợ tiếp nhận & chẩn đoán sơ bộ sự cố xe điện VinFast           │
│ Công ty thành viên: [x] VinFast                                             │
│                                                                             │
│ Ai đang đau (Actor): Kỹ thuật viên & Cố vấn dịch vụ xưởng VinFast.           │
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Khách báo lỗi/gửi ảnh ──> 2. Cố vấn đọc mô tả ──> 3. Tra sổ tay kỹ thuật │
│   ──> 4. Ước tính thời gian & lập báo giá sơ bộ.                            │
│                                                                             │
│ Bước tốn thời gian/lỗi nhất: Tra cứu tài liệu chẩn đoán ca khó (⏱ 20-30 min).│
│ AI nhảy vào ở bước nào: AI phân tích hình ảnh/mô tả ──> Gợi ý mã lỗi & vật tư│
│                                                                             │
│ Đo thành công bằng gì: Giảm thời gian chẩn đoán ban đầu từ 25 min ──> < 5 min.│
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                       │
│                                                                             │
│ Bài toán: Tự động hóa kiểm tra & đồng bộ hồ sơ thẻ cư dân Vinhomes           │
│ Công ty thành viên: [x] Vinhomes                                            │
│                                                                             │
│ Ai đang đau (Actor): Cư dân Vinhomes & Nhân viên Ban quản lý khu đô thị.    │
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Cư dân nộp hồ sơ trên app ──> 2. BQL kiểm tra giấy tờ ──>              │
│   3. Đối chiếu dữ liệu căn hộ ──> 4. Kích hoạt thẻ ra vào/xe.               │
│                                                                             │
│ Bước tốn thời gian/lỗi nhất: Nhân viên BQL đối chiếu giấy tờ thủ công (7 ngày)│
│ AI nhảy vào ở bước nào: OCR đọc giấy tờ ──> AI xác minh dữ liệu ──> Duyệt tự động│
│                                                                             │
│ Đo thành công bằng gì: Rút ngắn thời gian duyệt thẻ từ 7 ngày ──> < 24 giờ. │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent                 │
└─────────────────────────────────────────────────────────────────────────────┘
```