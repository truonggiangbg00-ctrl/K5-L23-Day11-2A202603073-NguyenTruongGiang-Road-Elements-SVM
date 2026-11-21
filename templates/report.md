# Báo cáo cá nhân — Ngày 11
Họ tên:   Nguyễn Trường Giang            Mã học viên:  2A202603073
Phiên bản CVAT (Help → About):  CVAT 2.16 (CVAT for images 1.1)
Guideline: Road v1.0    Lần nộp (`revision` trong manifest):  1
Thời điểm export (ngày giờ trên CVAT):  21/11/2026 11:39:04 (04:39:04 UTC)    Số lần nộp lại sau Rework:  0

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đã dùng đủ `lane`, `road_curb`, `crosswalk`, `drivable`, `traffic_light`, `traffic_sign`. | Đúng kiểu polyline/polygon/rectangle theo đặc tả |
| Thuộc tính và giá trị | Các giá trị đã có thuộc tính theo nhãn: `position/style/color/kind`, `area_type`, `color/type/facing`, `group/facing`, `edge_zone`. | Đầy đủ giá trị định sẵn, không dùng nhãn tự chế |
| 4 tag ảnh | Đủ tag ở 28 ảnh, có đủ các tag camera , timeofday, weather, source. | Gán camera đầu tiên trên từng ảnh |

- Cách kết thúc polyline trên bản CVAT này: Chọn công cụ Polyline, label lane, rồi bấm Shape. Click lần lượt các điểm trên tâm vệt sơn. Bắt đầu từ phía gần xe (đáy ảnh) và đi ra xa, xong thì bấm phím N (hoặc click đúp chuột) để kết thúc.
- Cách đặt tag ảnh trên bản CVAT này: Dùng công cụ Tag ở thanh bên trái. Đặt camera trước, sau đó timeofday, weather, source. Trong bảng Objects, mở Details của từng tag để kiểm tra và sửa giá trị select `value`.

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
| A04 | `lane` | Vẽ 1 polyline có `kind=double` hay vẽ 2 polyline riêng cho vạch đôi | Vẽ 2 polyline cùng vị trí L1/R2 | Nhìn thấy 2 vệt sơn thực tế chạy song song nên vẽ 2 polyline; theo guideline Road v1.0 chuẩn thì nên vẽ 1 polyline ở trục tâm với thuộc tính `kind=double`. |
| A05 | `lane` / `road_curb` | Có vẽ L1/R1 không hay chỉ vẽ `road_curb` | Không vẽ L1/R1, chỉ vẽ `road_curb` | Mặt đường khu vực giao cắt/nội khu hoàn toàn không có vạch kẻ sơn L1/R1 còn nhìn thấy được; tuân thủ nguyên tắc không tạo nhãn ảo và đã báo lead xin miễn trừ (waive) QC1-02. |
| A06 | `lane` / `crosswalk` | Vẽ lane xuyên qua vạch đi bộ hay ngắt trước vạch | Vẽ `crosswalk` bao kín các sọc, lane dừng trước giao lộ | Vạch sang đường chiếm toàn bộ phần đường giao lộ, không còn vạch phân làn kéo dài qua ngã tư. |
| A07 | `traffic_light` | Chọn color `red` hay `off` | Chọn `red` cho đèn đang sáng, đèn tắt chọn `off` | Thuộc tính color là màu của bóng đèn tín hiệu đang phát sáng tại thời điểm chụp, không gán theo màu vỏ. |
| A09 | `lane` / `road_curb` | Vẽ lane R1 hay vẽ `road_curb` sát mép đường | Không vẽ R1, vẽ `road_curb` | Mép đường bên phải là dải lề đất/bụi không có vệt sơn, do đó mép ngoài được gán là `road_curb`. |
| B05 | `lane` (fisheye MVL) | Chọn position L1/R1 hay `other` | Chọn `position = other` | Theo Guideline Road v1.0 mục 4: Đối với camera fisheye hai bên sườn xe (`fisheye_left`, `fisheye_right`), toàn bộ vạch lane bắt buộc gán `position = other`. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi:  Nguyễn Viết Quang            Quyết định nhận được:  Hold  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | --- | --- | --- |
| QC1-05 | 5 | Đã nhận | Không cần sửa vì thực tế hiện trường là vạch đôi (A04, A09, A11, A14), người gán vẽ 2 polyline để bám chi tiết hai vệt sơn. Đã giải trình trong bảng ca khó. |
| QC1-02 | 6 | Đã nhận | Không cần sửa vì các ảnh A05, A06, A07, A09, A14 mặt đường thực tế bị mòn mờ hoàn toàn hoặc không có vạch kẻ L1/R1, đã báo lead xác nhận miễn trừ. |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `NguyenTruongGiang-front.zip` | Có | 9 | 8 | Có (`camera=front`) |
| `NguyenTruongGiang-front-extra.zip` | Có | 7 | 8 | Có (`camera=front`) |
| `NguyenTruongGiang-fisheye.zip` | Có | 2 | 6 | Có (`camera=fisheye_front`) |
| `NguyenTruongGiang-fisheye-extra.zip` | Có | 2 | 3 | Có (`camera=fisheye_front`) |
| `NguyenTruongGiang-manifest.json` | Có | N/A (JSON manifest) | N/A | Có trong manifest (`CVAT for images 1.1`) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project (hiển thị đủ 6 nhãn và 4 nhãn Tag kèm danh sách thuộc tính).
2. Một ảnh camera trước đã gán đủ (làn đường L1/R1, vùng lái direct/alternative, đèn tín hiệu/biển báo).
3. Một ảnh fisheye đã gán (hiển thị polyline bám theo cung cong của thấu kính fisheye, không gán thân xe).
4. Một đoạn XML annotations.xml có thẻ `<polyline label="lane">` kèm đầy đủ thuộc tính `position`, `style`, `color`, `kind`.

## 7. Tự đánh giá
- **Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:**  
  Lỗi mắc phải và bị cảnh báo nhiều nhất là **QC1-05** (cảnh báo 2 polyline trùng position do vẽ 2 đường song song cho vạch đôi) và **QC1-02** (cảnh báo thiếu L1/R1 ở những ảnh thực tế không có vạch).  
  *Cách tránh ở Ngày 20:* Đối với vạch đôi, tuân thủ đúng quy ước taxonomy: chỉ vẽ 1 đường polyline ở trục tâm dải sơn và chọn thuộc tính `kind = double`, tránh vẽ 2 polyline cùng position gây cảnh báo conflict. Đối với các ảnh đường không có vạch, ghi chép và gắn cờ ngay vào bảng ca khó kèm ảnh minh chứng để xin xác nhận của lead trước phiên QC.

- **Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:**  
  Dữ liệu nhãn này là ground truth huấn luyện các mô hình thị giác máy tính cho xe tự hành (ADAS), cụ thể:
  - Nhãn `lane` đi vào mô hình phát hiện làn đường (Lane Detection) phục vụ chức năng Hỗ trợ giữ làn đường (Lane Keeping Assist - LKA) và Cảnh báo lệch làn (LDW).
  - Nhãn `drivable` đi vào mô hình phân vùng di chuyển (Drivable Area Segmentation) phục vụ lập quỹ đạo chuyển động (Trajectory Planning).
  - *Phân tích tác động sai lệch:* Nếu mắc lỗi **QC1-05 (vẽ 2 polyline trùng position L1)**, khi huấn luyện mô hình dự đoán vị trí làn đường (như cấu trúc Row-Anchor), hàm loss sẽ bị phạt nặng do có hai target tọa độ x khác nhau trên cùng một slot L1 tại cùng một hàng y. Điều này khiến mô hình hội tụ kém, đầu ra dự đoán bị dao động (chập chờn giữa 2 vạch) làm hệ thống điều khiển LKA tính toán sai tâm làn xe, gây hiện tượng rung lắc vô-lăng hoặc giật lái nguy hiểm trong thực tế.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi (A01 - L1: `lane#4@(109,720)`) | 109.2 | 156.0 | 202.8 | 249.6 | 296.7 |
| x của bạn kia (hoặc A01 - R1: `lane#7@(657,680)`) | không có làn | không có làn | 600.8 | 543.8 | 486.8 |

Trả lời 3 câu:

1. **Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?**  
   - Nếu dừng polyline sớm 40 px ở phía xa (ví dụ điểm cuối dừng ở $y = 600$ thay vì kéo dài tới $y = 560$), thì hàng **$y = 560$** sẽ nằm ngoài phạm vi bao của polyline và chuyển trạng thái thành **"không có làn"**.  
   - Tương tự, nếu bắt đầu polyline muộn 40 px ở phía gần xe (tại $y = 680$ thay vì sát đáy $y = 720$), thì hàng **$y = 720$** sẽ biến thành "không có làn".

2. **So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?**  
   - Ở hàng $y = 720$ (ngay trước đầu xe), độ lệch tọa độ thường nhỏ ($\approx 1 - 3\text{ px}$); ở hàng $y = 560$ (phía xa tầm nhìn), độ lệch có thể lớn hơn ($\approx 5 - 10\text{ px}$) do phối cảnh xa vạch bị mờ và khó định vị tâm vạch chính xác.  
   - **Lệch ở hàng $y = 720$ ảnh hưởng đến LKA nhiều hơn:** Hàng $y = 720$ thể hiện vị trí thực tế tức thời của xe so với làn đường để tính sai số vị trí ngang (lateral offset error). Nếu sai số ở hàng gần xe lớn, bộ điều khiển phản hồi của xe sẽ phản ứng lập tức bằng cách đánh lái mạnh/giật cục. Trong khi đó, hàng xa $y = 560$ chủ yếu cung cấp thông tin góc nhìn trước (look-ahead curvature heading) và được lọc làm mịn qua thời gian.

3. **Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?**  
   - Về mặt hình học tĩnh (tìm giao điểm của các đoạn thẳng với đường thẳng ngang $y = \text{const}$), các giá trị tọa độ giao điểm $x$ về bản chất toán học không thay đổi.  
   - Tuy nhiên, các script tiền xử lý dữ liệu và trích xuất đặc trưng (như script nội suy `rowanchor.py` hay pipeline nạp dữ liệu huấn luyện của mô hình row-anchor như UFLD) thường mặc định mảng tọa độ có thứ tự $y$ giảm dần đơn điệu từ gần ra xa xe ($y_{\text{gần}} > y_{\text{xa}}$). Nếu vẽ ngược từ xa về gần, script sẽ gặp lỗi logic duyệt mảng, nhầm lẫn điểm bắt đầu/kết thúc (start/end anchor), hoặc phải tốn thêm chi phí đảo ngược mảng; mô hình học chuỗi điểm cũng bị đảo lộn gradient định hướng.
