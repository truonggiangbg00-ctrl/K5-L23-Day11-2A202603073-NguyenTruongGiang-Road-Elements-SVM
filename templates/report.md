# Báo cáo cá nhân — Ngày 11
Họ tên:   Nguyễn Trường Giang            Mã học viên:  2A202603073
Phiên bản CVAT (Help → About):  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest):  1
Thời điểm export (ngày giờ trên CVAT):    Số lần nộp lại sau Rework:  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đã dùng đủ `lane`, `road_curb`, `crosswalk`, `drivable`, `traffic_light`, `traffic_sign`. |  |
| Thuộc tính và giá trị | Các giá trị đã có thuộc tính theo nhãn: `position/style/color/kind`, `area_type`, `color/type/facing`, `group/facing`, `edge_zone`. |  |
| 4 tag ảnh | Đủ tag ở 28 ảnh, có đủ các tag camera , timeofday, weather, source. |  |



- Cách kết thúc polyline trên bản CVAT này: Chọn công cụ Polyline, label lane, rồi bấm Shape. Click lần lượt các điểm trên tâm vệt sơn. Bắt đầu từ phía gần xe (đáy ảnh) và đi ra xa, xong thì bấm phím N để kết thúc.
- Cách đặt tag ảnh trên bản CVAT này: Dùng công cụ Tag ở thanh bên trái. Đặt camera trước, sau đó timeofday, weather, source. Trong bảng Objects, mở Details của từng tag để kiểm giá trị.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 35 | 9 | 4 | 24 | 20 | 16 |
| front-extra (đã làm 4 / 4) | 4 | 12 | 4 | 2 | 8 | 2 | 10 |
| fisheye | 8 | 8 | 11 | 8 | 8 | 2 | 1 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 2 | 5 | 4 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi:  Quyết định nhận được:  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | --- | --- | --- |
| QC1-05 | 5 | Đã nhận | Không cần sửa vì đó là đường kẻ đôi |
| QC1-02 | 6 | Đã nhận | Không cần sửa vì thật sự không có vạch L1 và R1 |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |

## 6. Ảnh chụp màn hình
1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.
4. Một đoạn XML có <polyline label="lane">.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi |  |  |  |  |  |
| x của bạn kia |  |  |  |  |  |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?
