# Danh sách lớp v0 — Phạm Đình Lực · G07

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state | open / closed / unknown | Phát hiện buồn ngủ, ngủ gật (nhắm mắt liên tục > 1.5s) | Có, trừ khi bị đốm lóa phản xạ LED |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung (nhìn đùi/điện thoại, nhìn màn hình quá lâu) | Có (ước lượng qua hướng tròng mắt và xoay đầu) |
| 3 | hand_on_wheel | yes / no / unknown | Cảnh báo rời tay lái (Hands-off warning) phục vụ tính năng tự lái L2/L2+ | Có |
| 4 | phone_interaction | held / mounted / lap / none | Cảnh báo vi phạm dùng điện thoại cầm tay khi đang điều khiển phương tiện | Có (thấy hình dáng viền máy hoặc ánh sáng màn hình) |
| 5 | head_pose | yaw, pitch, roll | Phát hiện tài xế ngất xỉu, gục đầu hoặc quay đầu nói chuyện bỏ quên làn đường | Có |
| 6 | driver_seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Cảnh báo thắt dây an toàn và điều chỉnh thuật toán nổ túi khí thông minh | Khó thấy nếu mặc áo tối màu trùng màu dây |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | seat_occupancy | person / empty | Nhắc nhở hành khách thắt dây an toàn cho từng vị trí ghế cụ thể | Có |
| 2 | child_seat_status | rear_facing / front_facing / none | Tự động tắt túi khí ghế trước nếu lắp ghế trẻ em quay ngược (tránh chấn thương tử vong) | Có (dựa vào hình dáng ghế) |
| 3 | forgotten_object | bag / box / cup / phone / other | Cảnh báo đồ vật hoặc hành lý bị bỏ quên khi chủ xe tắt máy khóa cửa xe | Có |
| 4 | passenger_seatbelt | worn_correct / not_worn / unknown | Cảnh báo hành khách ngồi sau chưa thắt dây an toàn theo luật định | Có, dựa vào đường chéo từ vai xuống hông |
| 5 | passenger_posture | normal / leaning / out_of_position | Nhận biết tư thế ngồi bất thường (gác chân lên táp-lô, cúi gập người) để hãm lực túi khí | Có |
| 6 | pet_detection | dog / cat / none | Cảnh báo để quên thú cưng trong xe dưới thời tiết nắng nóng (chống sốc nhiệt) | Có |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. **Câu hỏi:** Khi tài xế đeo kính râm sẫm màu nhưng camera NIR nhìn xuyên qua thấy rõ đồng tử và viền mắt đang mở, thì thuộc tính `glasses` nên gán là `sun` (theo bản chất kính ngoài đời thực) hay `clear` (theo đặc tính quang học thu được trên ảnh NIR)?
   - **Khung ví dụ:** D02
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán `sun` vì gọng kính dày đặc trưng kính râm và để model học nhận diện vật thể thực tế, nhưng thuộc tính mắt `eye_*` vẫn gán `open` theo những gì camera thấy được.

2. **Câu hỏi:** Trong trường hợp ghế trẻ em `child_seat` có một đồ vật (ví dụ balo `object`) đặt bên trong, thuộc tính `occupied` của `child_seat` nên gán là `no` (ghế trống không có trẻ em ngồi) hay `unknown` (vì ghế không hoàn toàn trống, đang chịu tải trọng vật thể)?
   - **Khung ví dụ:** S03_rgb
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán `occupied = no` kèm vẽ 1 box `object` riêng đè lên, theo logic `occupied` ở đây chỉ đo lường sự hiện diện của trẻ nhỏ (Child Presence Detection) chứ không tính đồ vật.
