# 01 — Problem Scan (Cá nhân)

>

---

## 🔍 Phase 1 — SCAN

### 📝 List bài toán của tôi:

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | VinFast | Lặp lại | Kỹ thuật viên xưởng dịch vụ đọc thủ công mã lỗi (DTC) và log pin/BMS rồi tra cứu tài liệu sửa chữa để chẩn đoán, tốn thời gian và phụ thuộc kinh nghiệm từng người, làm kéo dài thời gian xe nằm xưởng. |
| 2 | Xanh SM | Pain từ người khác | Tài xế chạy xe rỗng và chờ cuốc lâu ở khu vực dư xe, trong khi giờ cao điểm hoặc sự kiện lớn thiếu xe do điều phối viên cân đối thủ công, làm giảm thu nhập tài xế và tăng tỷ lệ khách bị bỏ lỡ. |
| 3 | Vinhomes | AI-upgrade | AI hỗ trợ ban quản lý tòa nhà tiếp nhận và phân loại yêu cầu của cư dân (sự cố kỹ thuật, phí dịch vụ, đặt tiện ích) qua hotline/app, hiện nhân viên phải đọc và chuyển bộ phận xử lý thủ công nên phản hồi chậm và không đồng đều. |
| 4 | Vinmec | Lặp lại | Nhân viên mã hóa đọc toàn bộ hồ sơ bệnh án để gán mã ICD-10 và dịch vụ kỹ thuật, đối chiếu chứng từ trước khi nộp bảo hiểm, gây chậm thanh toán và nhiều claim bị từ chối do sai hoặc thiếu mã. |
| 5 | Vinpearl | AI-upgrade | Phân công buồng phòng và vệ sinh theo giờ check-out/check-in dự kiến đang do quản lý ca sắp xếp thủ công, dẫn đến phòng sẵn sàng chậm, khách phải chờ nhận phòng và nhân sự phân bổ không đều. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Top 3 lựa chọn từ danh sách SCAN: **#1 (VinFast - chẩn đoán lỗi tại xưởng), #3 (Vinhomes - phân loại yêu cầu cư dân), #4 (Vinmec - mã hóa bệnh án và claim).**

### Quick Problem Card #1 — VinFast: Phân loại phản hồi lỗi xe

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                        │
│                                                               │
│ Bài toán: Kỹ thuật viên đọc thủ công mã lỗi (DTC) và log     │
│ pin/BMS rồi tra cứu tài liệu sửa chữa để tìm nguyên nhân.    │
│ Công ty thành viên: [x] VinFast                              │
│                                                               │
│ Ai đang đau (Actor)? Kỹ thuật viên xưởng dịch vụ; Khách hàng │
│ phải chờ xe nằm xưởng lâu, cố vấn dịch vụ khó báo thời gian  │
│ hoàn thành chính xác.                                        │
│                                                               │
│ Workflow thủ công hiện tại (4 bước):                         │
│   1. Xe vào xưởng, đọc mã lỗi và log qua thiết bị chẩn đoán  │
│   --> 2. KTV tra cứu tài liệu sửa chữa và lịch sử xe -->     │
│   3. Suy luận nguyên nhân gốc, chọn phương án sửa --> 4. Đặt │
│   phụ tùng, thực hiện sửa và ghi phiếu                       │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ ~25 phút/xe,    │
│ phụ thuộc kinh nghiệm cá nhân, dễ chẩn đoán sai phải quay    │
│ lại xưởng)                                                   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3 (tự động tóm  │
│ tắt log, tra cứu tài liệu và các ca tương tự, đề xuất nguyên │
│ nhân khả dĩ kèm bước kiểm tra)                               │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                        │
│   Giảm thời gian chẩn đoán từ 25 phút -> dưới 10 phút/xe,   │
│   tăng tỉ lệ sửa đúng ngay lần đầu (first-time-fix) ≥ 85%    │
│                                                               │
│ Quick Architecture: [ ] No AI  [x] LLM  [ ] Rule  [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #2 — Xanh SM: Phát hiện gian lận cuốc xe ảo (fake trip)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                        │
│                                                               │
│ Bài toán: Ban quản lý tòa nhà đọc và chuyển thủ công từng    │
│ yêu cầu của cư dân (sự cố kỹ thuật, phí dịch vụ, tiện ích)   │
│ tới đúng bộ phận xử lý.                                      │
│ Công ty thành viên: [x] Vinhomes                             │
│                                                               │
│ Ai đang đau (Actor)? Nhân viên tiếp nhận của ban quản lý;    │
│ Cư dân chờ phản hồi lâu, yêu cầu khẩn (rò nước, mất điện)    │
│ có thể bị xếp lẫn với yêu cầu thông thường.                  │
│                                                               │
│ Workflow thủ công hiện tại (4 bước):                         │
│   1. Cư dân gửi yêu cầu qua hotline/app --> 2. Nhân viên đọc │
│   và hiểu nội dung --> 3. Xác định loại việc và mức khẩn --> │
│   4. Chuyển bộ phận phù hợp (kỹ thuật/an ninh/kế toán) và    │
│   phản hồi cư dân                                            │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ ~4 phút/yêu     │
│ cầu, phản hồi đầu tiên thường 30-60 phút vào giờ cao điểm,   │
│ dễ chuyển nhầm bộ phận)                                      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4 (tự động phân │
│ loại loại việc và mức khẩn, đề xuất bộ phận nhận, soạn sẵn   │
│ phản hồi xác nhận cho cư dân)                                │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                        │
│   Giảm thời gian phân loại từ 4 phút --> dưới 30 giây,       │
│   độ chính xác chuyển đúng bộ phận ≥ 90%, phản hồi đầu tiên  │
│   dưới 10 phút                                               │
│                                                               │
│ Quick Architecture: [ ] No AI  [x] LLM  [ ] Rule  [ ] Agent  |
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #3 — Xanh SM: AI hỗ trợ tổng đài tài xế (2 nhóm case: Khẩn cấp & Huỷ cuốc)

```text
┌─────────────────────────────────────────────────────────────┐
│  QUICK PROBLEM CARD #3                                        │
│                                                               │
│ Bài toán: Nhân viên mã hóa đọc toàn bộ hồ sơ bệnh án để gán  │
│ mã ICD-10 và dịch vụ kỹ thuật, đối chiếu chứng từ trước khi  │
│ nộp bảo hiểm.                                                │
│ Công ty thành viên: [x] Vinmec                               │
│                                                               │
│ Ai đang đau (Actor)? Nhân viên mã hóa và thanh toán bảo      │
│ hiểm; Bộ phận tài chính chịu chậm dòng tiền khi claim bị từ  │
│ chối hoặc phải chỉnh sửa; Bác sĩ bị hỏi lại thông tin.       │
│                                                               │
│ Workflow thủ công hiện tại (4 bước):                         │
│   1. Hồ sơ bệnh án hoàn tất sau xuất viện/khám --> 2. Nhân   │
│   viên đọc bệnh án, kết quả cận lâm sàng --> 3. Gán mã ICD-10│
│   và dịch vụ, đối chiếu chứng từ --> 4. Nộp claim, xử lý     │
│   phản hồi từ chối của bảo hiểm                              │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ ~20 phút/hồ sơ, │
│ tỉ lệ claim bị từ chối ban đầu ~8% do sai/thiếu mã hoặc      │
│ thiếu chứng từ)                                              │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3 (tự động      │
│ trích xuất chẩn đoán và thủ thuật từ ghi chép, gợi ý mã,     │
│ cảnh báo thiếu chứng từ; nhân viên duyệt lại kết quả)        │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                        │
│   Giảm thời gian xử lý từ 20 phút --> dưới 5 phút/hồ sơ,     │
│   giảm tỉ lệ claim bị từ chối từ ~8% --> dưới 4%             │
│                                                               │
│ Quick Architecture: [ ] No AI  [x] LLM  [ ] Rule  [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```

## Kết luận lựa chọn

Trong các bài toán trên, chọn bài toán chính là:
- Vinmec - Trợ lý mã hóa bệnh án và chuẩn bị claim bảo hiểm

Lý do chọn: workflow rõ ràng, bottleneck tập trung ở bước đọc hồ sơ và gán mã, AI (LLM trích xuất + gợi ý mã, có người duyệt lại) phù hợp, và đo được ngay bằng thời gian xử lý mỗi hồ sơ và tỉ lệ claim bị từ chối.