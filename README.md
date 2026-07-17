# Gym Tracker — Kế hoạch tập giảm mỡ (Full Body A/B)

Ứng dụng web tĩnh (1 file `index.html`) theo dõi lịch tập gym 3 buổi/tuần luân phiên A/B.

## Tính năng
- Tự hiện buổi hiện tại (Tuần X · Buổi A/B) với checklist đầy đủ: Khởi động → Bài chính → Thư giãn.
- Tick từng bài, tick hết → kết thúc buổi, tự chuyển sang buổi tiếp theo (A↔B).
- Hết 3 buổi → báo "Tuần X hoàn thành" và bắt đầu tuần mới (đảo A/B).
- Ghi mức tạ mỗi bài + nhắc mức tạ lần trước để theo dõi tăng tiến.
- Timer nghỉ giữa hiệp 60/90s (kêu bíp + rung khi hết giờ).
- Tiến độ lưu ngay trên trình duyệt (localStorage) — không cần tài khoản, không cần mạng.

## Chạy
Mở `index.html` bằng trình duyệt, hoặc dùng bản GitHub Pages. Trên điện thoại: **Chia sẻ → Thêm vào Màn hình chính** để dùng như app.

*Lưu ý: Đây là plan tham khảo, không thay thế chỉ định của bác sĩ/vật lý trị liệu.*
