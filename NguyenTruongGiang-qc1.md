# Phiếu QC 1 — Road v1.0 (bản rà soát A01–A06)

**Lô được rà soát:** Nguyễn Trường Giang — 2A202603073  
**Người kiểm:** Nguyễn Ngọc Đông — 2A202603291  
**Ngày rà soát:** 21/11/2026  
**Tệp đã kiểm:** `NguyenTruongGiang-front.zip` · SHA-256 `f6e2b2ed35d025a38f8c35cd88975a24722822892b90d0c9f27eaff64f845a89`

## Phạm vi và cách kiểm

Chỉ kiểm sáu ảnh front A01–A06 theo yêu cầu: **52 shape** và **24 tag**. Đã đọc lại XML, chạy `road_check lint` và đối chiếu trực quan với ảnh nguồn/ảnh CVAT được cung cấp. Lint không có golden truth; mọi dòng “cần xác nhận” dưới đây không được tính là lỗi đã xác định.

## Kết quả theo nhóm QC

| Mã | Phạm vi đã rà | Kết quả |
| --- | --- | --- |
| QC1-01 | 4 tag mỗi ảnh | A01–A06 có camera `front`, timeofday/weather/source hợp lệ. Không thấy lỗi cấu trúc. |
| QC1-02 | L1/R1 | A01–A04 có L1/R1. A05 không thấy vạch làn trên ảnh; giữ ngoại lệ, **không tự vẽ L1/R1**. A06 thiếu R1 theo lint nhưng ảnh giao cắt/qua vạch ngựa vằn không cho thấy R1 rõ ràng; ghi ngoại lệ cần người kiểm xác nhận. |
| QC1-03 | `position` lane | Không có lane camera bên; các giá trị trong tập `L1/R1/L2/R2` hợp lệ. |
| QC1-04 | Chiều gần → xa | Điểm đầu/cuối của 17 lane A01–A06 theo hướng gần xe ra xa; không thấy cảnh báo chiều vẽ. |
| QC1-05 | Lane đứt/tách | A04 có hai polyline cùng `L1` và hai cùng `R2`, cùng `kind=double`; cần đối chiếu xem là vạch đôi thật hay một vạch bị vẽ lặp. |
| QC1-06 | style/color/kind | Giá trị XML hợp lệ; A04 cần xác nhận lại `kind=double` cùng với QC1-05. |
| QC1-07 | drivable/curb/crosswalk | Đã rà trực quan A01–A06; không chốt lỗi khi không có GT. |
| QC1-08 | traffic light | A06 có 6 box, thuộc tính có mặt; chưa có GT để kết luận sai/missing đèn. |
| QC1-09 | sign/light attributes | Các thuộc tính bắt buộc có mặt ở shape đã kiểm; chưa đối chiếu GT. |
| QC1-10 | sign/crosswalk | Không kết luận thiếu/thừa khi không có GT. |
| QC1-11 | fisheye | Không áp dụng cho sáu ảnh front. |
| QC1-12 | XML/file | ZIP đọc được; parser không báo lỗi cấu trúc. |

## Ngoại lệ có ảnh chứng minh

| Ảnh | Cảnh báo lint | Nhận định trực quan | Xử lý |
| --- | --- | --- | --- |
| A05 | QC1-02: thiếu L1, R1 | Ảnh đường phố không có vạch làn nhận biết được. | Không coi là lỗi; không thêm line. Lưu ảnh CVAT làm chứng cứ. |
| A06 | QC1-02: thiếu R1 | Bối cảnh giao cắt/crosswalk; R1 không quan sát rõ. | Ngoại lệ chờ người kiểm xác nhận, không tự thêm line. |

## Điểm cần xác nhận trước khi chốt

| Mã | Ảnh | Mức | Nội dung |
| --- | --- | --- | --- |
| QC1-05/06 | A04 | chính — cần xác nhận | Có hai `L1` và hai `R2`, tất cả `kind=double`. Nếu mỗi cặp là một nét bị vẽ lặp thì gộp thành một polyline `kind=double`; nếu là hai vạch vật lý khác nhau thì ghi rõ lý do và giữ nguyên. |

## Kết luận tạm thời

Không thấy lỗi nặng đã được xác nhận trên A01–A06. A05 không được coi là thiếu L1/R1 vì có ảnh chứng minh không có vạch; A06 là ngoại lệ cần xác nhận. Chưa chốt Release/Rework cho toàn bộ bài vì phạm vi QC chỉ gồm sáu ảnh và chưa có golden truth.
