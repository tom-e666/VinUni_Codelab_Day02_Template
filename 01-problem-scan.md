# 🔍 Phase 1 — SCAN & QUICK-ASSESS (Vin Smart Future)

> **Bản tổng hợp chọn lọc từ ý tưởng của Nhóm (Tiến & Duy)**

---

## 📝 1. Danh sách 5 Bài toán Vận hành Chọn lọc (Problem List)

| # | Subsidiary (Công ty) | Lens (Ống kính) | Mô tả ngắn bài toán & Bottleneck | Nguồn đóng góp |
|---|---|---|---|---|
| 1 | **Xanh SM (GSM)** | 😣 **Stakeholder Pain** + ⏱ **Time-consuming** | **Điều phối & xử lý sự cố hết pin thực địa:** Điều phối viên phải tra cứu vị trí GPS, tìm trạm sạc VinFast còn trụ trống phù hợp và soạn SMS chỉ dẫn thủ công cho tài xế (mất **15 phút/lượt**). | *Duy & Tiến* |
| 2 | **VinFast – After-sales** | ⏱ **Time-consuming** (Tốn thời gian) | **Tiếp nhận & chẩn đoán xe trước sửa chữa:** Khách hàng mô tả lỗi + gửi hình ảnh; xưởng phải tiếp nhận, đánh giá tình trạng, tra cứu tài liệu chẩn đoán ca khó và lập báo giá thủ công (**20–30 phút/ca**). | *Tiến* |
| 3 | **Vinhomes** | 😣 **Stakeholder Pain** + ⏱ **Time-consuming** | **Đồng bộ hồ sơ cư dân & thẻ ra vào/thẻ xe:** Quá trình đối chiếu giấy tờ và đồng bộ app kéo dài cả tuần (7 ngày), khiến cư dân chưa làm được thẻ ra vào/xe và phải chịu phí gửi xe vãng lai hàng ngày. | *Tiến* |
| 4 | **Vinmec** | 😣 **Stakeholder Pain** (Nỗi đau bác sĩ) | **Tóm tắt hồ sơ bệnh án & phiếu xuất viện:** Bác sĩ mất **20–30 phút** cho mỗi bệnh nhân để đọc lại toàn bộ lịch sử khám, thay đổi đơn thuốc và viết tay bản tóm tắt xuất viện, gây quá tải khối lượng công việc. | *Duy* |
| 5 | **Vinpearl** | 🤖 **AI-upgrade** + ⏱ **Time-consuming** | **Xử lý yêu cầu đặt phòng đoàn (Group Booking):** Nhân viên booking phải đọc thủ công các email/yêu cầu đặt phòng phức tạp theo đoàn và đối chiếu danh sách phòng trống trên nhiều hệ thống. | *Duy* |

---

## 🃏 2. Top 3 Quick Problem Cards (Phase 2)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 (XANH SM)                                            │
│                                                                             │
│ Bài toán (1 câu): Điều phối & hỗ trợ khẩn cấp tài xế Xanh SM báo sự cố hết pin│
│ Công ty thành viên: [x] Xanh SM (GSM)                                       │
│                                                                             │
│ Ai đang đau (Actor): Tài xế Xanh SM & Điều phối viên tổng đài.              │
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Nhận điện thoại sự cố ──> 2. Định vị GPS xe ──> 3. Tra trạm sạc trống  │
│   ──> 4. Soạn SMS hướng dẫn ──> 5. Điều xe cứu hộ nếu pin < 5%.              │
│                                                                             │
│ Bước tốn thời gian/lỗi nhất: Tra trạm sạc trống & Soạn SMS (⏱ 10/15 min).   │
│ AI nhảy vào ở bước nào: AI auto-pull GPS ──> Tra trụ trống ──> Draft SMS.   │
│                                                                             │
│ Đo thành công bằng gì: Giảm thời gian xử lý từ 15 min ──> < 3 min.         │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM Feature  [ ] Agent         │
└─────────────────────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2 (VINFAST)                                             │
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
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM Feature  [ ] Agent         │
└─────────────────────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3 (VINMEC)                                              │
│                                                                             │
│ Bài toán: Tự động tổng hợp & soạn thảo bản nháp tóm tắt xuất viện Vinmec    │
│ Công ty thành viên: [x] Vinmec                                              │
│                                                                             │
│ Ai đang đau (Actor): Bác sĩ điều trị & Đội ngũ quản lý hồ sơ bệnh án.       │
│                                                                             │
│ Workflow thủ công hiện tại:                                                 │
│   1. Xem lại lịch sử khám ──> 2. Tổng hợp thay đổi thuốc ──>                │
│   3. Viết văn bản tóm tắt xuất viện ──> 4. Bác sĩ kiểm tra & ký duyệt.      │
│                                                                             │
│ Bước tốn thời gian/lỗi nhất: Đọc trích xuất dữ liệu & viết tóm tắt (⏱ 20 min).│
│ AI nhảy vào ở bước nào: AI trích xuất dữ liệu ──> Draft bản nháp tóm tắt.   │
│                                                                             │
│ Đo thành công bằng gì: Giảm 50% thời gian soạn thảo (từ 20 min ──> 8 min). │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM Feature (HITL)  [ ] Agent  │
└─────────────────────────────────────────────────────────────────────────────┘
```