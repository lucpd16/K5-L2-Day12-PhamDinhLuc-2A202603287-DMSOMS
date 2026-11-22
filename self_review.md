# Tự đánh giá — Phạm Đình Lực · G07

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S07_rgb.png | child_seat | seat_flip | Ghế ở giữa ban đầu để mặc định là driver | Đã sửa sang rear_middle |
| D01.png | face13 | ok | 13 điểm skeleton gắn chuẩn mép mắt, mũi, miệng | Đã chuẩn |
| D03.png | glasses / face | ok | Kính râm nhìn xuyên được trên NIR, đánh dấu đúng open và sun | Đã chuẩn |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Set giá trị `day` cho thuộc tính `light` của ảnh IR (ảnh S), mặc định ảnh IR phải để `light` là `unknown`.

Vì sao mình mắc: Do thói quen gán nhanh trên giao diện CVAT và chưa đọc kỹ lưu ý cho các giá trị thuộc tính.

Lần sau tránh bằng cách: Dùng lệnh kiểm tra tự động `cabin_check.py` ngay sau mỗi checkpoint để phát hiện sớm các trường thuộc tính đặc biệt.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: Ở cảnh S04 (`infant_seat`), thuộc tính `facing` nên là `rear` (nôi em bé hướng quay về phía sau xe) theo đúng quy chuẩn lắp đặt an toàn trên ô tô thực tế. Ngoài ra, việc so sánh diff cho thấy bạn của mình bị thiếu hoàn toàn skeleton 13 điểm `face13` trên các ảnh DMS, giúp mình củng cố tầm quan trọng của việc đối chiếu chéo để không sót các nhãn quan trọng.
