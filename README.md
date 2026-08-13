# DUC_TinhTienTro — Máy Tính Tiền Trọ

> Web app tính & chia tiền trọ cho phòng ở ghép, chạy 100% client-side trong **một file HTML duy nhất**. Kết quả xuất ra dạng **hóa đơn** tối ưu để chụp màn hình và gửi qua Zalo/Messenger.

**Trạng thái:** `[~]` ĐANG tinh chỉnh · **Ngôn ngữ:** HTML/JS · **Cập nhật:** 10/08/2026

---

## Tính năng chính

- **Nhập liệu linh hoạt:** đơn giá điện/nước, tiền phòng, rác, phụ thu, chỉ số công tơ cũ–mới — tất cả là input, không hardcode.
- **Chia cho 2 người** (tên sửa được): tính theo điện riêng + tỉ lệ số ngày ở + trả trước.
- **Hóa đơn nổi bật:** header gradient, tổng tiền `PHẢI TRẢ` cỡ lớn, phong cách fintech xanh dương.
- **Tự lưu localStorage:** nhập 1 lần, mở lại không mất dữ liệu.
- **Tải ảnh hóa đơn** (`html2canvas`) → file PNG đặt tên theo tháng.

## Công thức

```
Tổng nước        = nước mới − nước cũ;   Tiền nước = tổng nước × đơn giá nước
Tổng điện        = điện mới − điện cũ
Điện chung       = tổng điện − (điện riêng người 1 + điện riêng người 2)
Tổng chi phí chung = phòng + rác + tiền nước + phụ thu + (điện chung × đơn giá điện)
Tỉ lệ (mỗi người)  = số ngày ở / tổng số ngày ở   (chia 0 → 0.5/người)
Phải trả (mỗi người) = (tổng chi phí chung × tỉ lệ) + (điện riêng × đơn giá điện) − trả trước
```

## Tech stack

- HTML5 + Vanilla JavaScript + Tailwind CSS (CDN)
- `html2canvas@1.4.1` (CDN) — xuất ảnh hóa đơn
- Không backend, không database, không build step.

## Cách chạy

1. Mở `DUC_TinhTienTro.html` bằng trình duyệt (Chrome/Edge) — cần mạng để tải CDN.
2. Nhập số liệu → bấm **XUẤT HÓA ĐƠN**.
3. Bấm **📸 Tải ảnh hóa đơn** để lưu PNG.

## Cấu trúc thư mục

```
DUC_TinhTienTro/
├── DUC_TinhTienTro.html      # toàn bộ app (HTML + CSS + JS)
├── GiaoDien-TienTro.svg      # minh họa giao diện (vector, số liệu mẫu)
└── _BAN-GIAO_2026-08-10.md   # tài liệu bàn giao chi tiết + rủi ro
```

## Screenshot

> ⚠️ Chưa có ảnh chụp thực tế — cần tự chụp trên trình duyệt/điện thoại rồi thêm vào đây.
>
> `![Giao diện](screenshot-giao-dien.png)`
> `![Hóa đơn](screenshot-hoa-don.png)`

## ⚠️ Trạng thái nghiệm thu & rủi ro (đọc kỹ)

- **Logic tính:** ✅ đã nghiệm thu bằng bộ số mẫu (tổng 2 người khớp chính xác).
- **UI + tải ảnh:** ❌ **CHƯA nghiệm thu** trên trình duyệt/mobile thật.
- **Phụ thuộc mạng:** Tailwind + html2canvas load từ CDN → không có mạng là hỏng giao diện + không tải được ảnh.
- **Giới hạn:** cứng đúng 2 người; chưa validate input (điện mới < cũ ra số âm không cảnh báo); localStorage chỉ theo 1 trình duyệt.

Chi tiết đầy đủ xem `_BAN-GIAO_2026-08-10.md` (mục B — Rủi ro / Technical debt).

## Checklist tinh chỉnh (chuẩn 00_DANG-TINH-CHINH)

- [x] Đổi tên chương trình + file theo chuẩn `DUC_` (ASCII, không dấu)
- [x] README
- [x] File bàn giao (`_BAN-GIAO_2026-08-10.md`)
- [x] Không chứa secret / IP nội bộ / thông tin Chervon
- [ ] Screenshot (tự chụp)
- [ ] Nghiệm thu UI + tải ảnh trên trình duyệt thật
