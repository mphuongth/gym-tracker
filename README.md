# Gym Tracker — Kế hoạch tập gym

Ứng dụng web tĩnh (1 file `index.html`) theo dõi lịch tập gym. Hỗ trợ **nhiều kế hoạch**: dùng plan mặc định (giảm mỡ Full Body A/B) hoặc **upload plan riêng** dưới dạng JSON.

## Tính năng
- Tự hiện buổi hiện tại (Tuần X · buổi nào) với checklist đầy đủ: Khởi động → Bài chính → Thư giãn.
- Tick từng bài, tick hết → kết thúc buổi, tự chuyển sang buổi tiếp theo theo `sessionOrder`.
- Hết một tuần → báo "Tuần X hoàn thành" và bắt đầu tuần mới.
- Ghi tạ + reps (hoặc giây cho bài giữ như Plank) từng set + nhắc lần trước để theo dõi tăng tiến.
- Cân nặng theo tuần + biểu đồ đường.
- Timer nghỉ giữa hiệp 60/90s (bíp + rung khi hết giờ).
- **Nhiều kế hoạch**: thư viện plan dạng card, upload JSON, plan mới thành mặc định, chọn plan khác bất cứ lúc nào. Tiến độ lưu riêng theo từng plan; cân nặng dùng chung.
- Xuất / nhập backup toàn bộ dữ liệu (.json).
- Tiến độ lưu ngay trên trình duyệt (localStorage) — không cần tài khoản, không cần mạng.

## Chạy
Mở `index.html` bằng trình duyệt, hoặc dùng bản GitHub Pages. Trên điện thoại: **Chia sẻ → Thêm vào Màn hình chính** để dùng như app.

## Format kế hoạch (upload) — `gym-plan/v1`

Trong app: chip tên plan ở đầu trang → **Thêm kế hoạch mới** → dán JSON hoặc chọn file `.json`. Bấm **Tải mẫu** để lấy plan hiện tại làm khuôn. Xem ví dụ đầy đủ ở [`examples/plan-example-ppl.json`](examples/plan-example-ppl.json).

```json
{
  "schema": "gym-plan/v1",
  "name": "Tên kế hoạch",           // bắt buộc
  "goal": "Mục tiêu (mô tả ngắn)",   // tuỳ chọn
  "daysPerWeek": 3,                  // số buổi/tuần; mặc định = độ dài sessionOrder
  "dayLabels": ["Thứ 2", "Thứ 4", "Thứ 6"],  // nhãn từng ngày; tuỳ chọn
  "sessionOrder": ["A", "B"],        // bắt buộc: thứ tự buổi, xoay vòng theo từng buổi tập
  "warmup":  [ { "name": "...", "detail": "..." } ],   // tuỳ chọn, dùng chung mọi buổi
  "cooldown":[ { "name": "...", "detail": "..." } ],   // tuỳ chọn
  "sessions": {                      // bắt buộc: map key → buổi tập
    "A": { "title": "Buổi A", "exercises": [
      { "name": "Squat", "detail": "3 × 10–12", "alt": "Leg Press", "note": "Giữ lưng thẳng" }
    ]},
    "B": { "title": "Buổi B", "exercises": [ { "name": "Hip Thrust", "detail": "3 × 10–12" } ] }
  }
}
```

**Quy tắc:**
- Buổi tập thứ `n` (đếm từ 0) = `sessionOrder[n % sessionOrder.length]`; cứ `daysPerWeek` buổi gom thành 1 tuần. A/B luân phiên chỉ là `["A","B"]` với `daysPerWeek: 3`. Plan 4 buổi: `sessionOrder` 4 key + `daysPerWeek: 4`.
- Mỗi bài `exercise`: `name` (bắt buộc), `detail`, `alt` (bài thay thế), `note` (lưu ý).
- Cách ghi định lượng suy ra từ `detail`:
  - `"3 × 10–12"` → ghi **kg + reps** từng set.
  - `"3 × 30–45s"` (reps là thời gian) → ghi **giây** từng set.
  - `"15–20 phút · ..."` (không mở đầu bằng `N ×`) → chỉ tick, **không** ghi định lượng (cardio/finisher).

*Lưu ý: Đây là plan tham khảo, không thay thế chỉ định của bác sĩ/vật lý trị liệu.*
