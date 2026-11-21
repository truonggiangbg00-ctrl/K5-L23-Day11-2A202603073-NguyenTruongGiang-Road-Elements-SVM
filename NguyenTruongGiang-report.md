# Báo cáo cá nhân — Ngày 11

**Họ tên:** Nguyễn Trường Giang  
**Mã học viên:** 2A202603073  
**Guideline:** Road v1.0  
**Lần nộp (`revision`):** 1  
**Thời điểm tạo manifest:** 21/11/2026 02:39 ICT  
**Phiên bản CVAT / thời điểm export trên CVAT / số lần Rework:** Chưa có bằng chứng trong các ZIP được cung cấp.

## 1. Kiểm project

| Mục | Trạng thái từ export và ảnh chứng minh | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đã dùng đủ `lane`, `road_curb`, `crosswalk`, `drivable`, `traffic_light`, `traffic_sign`. | XML được cung cấp không có metadata label đầy đủ, nên cần mở CVAT để xác nhận kiểu khai báo gốc. |
| Thuộc tính và giá trị | Các shape đã có thuộc tính theo nhãn: `position/style/color/kind`, `area_type`, `color/type/facing`, `group/facing`, `edge_zone`. | Parser đọc được; chưa so golden truth. |
| 4 tag ảnh | Lint không báo thiếu tag ở 28 ảnh; sáu ảnh A01–A06 có camera `front`, timeofday, weather, source. | Cần giữ nguyên khi xuất bản nộp. |

Polyline được lưu trong XML bằng nhiều điểm `x,y` phân cách bởi dấu `;`. Tag ảnh được lưu bằng phần tử `<tag>` cùng thuộc tính `value`.

## 2. Số lượng đã gán

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front A01–A12 | 12 | 35 | 9 | 4 | 24 | 20 | 16 |
| front-extra A13–A16 | 4 | 12 | 4 | 2 | 8 | 2 | 10 |
| fisheye B01–B08 | 8 | 8 | 11 | 8 | 8 | 2 | 1 |
| fisheye-extra B09–B12 | 4 | 0 | 2 | 5 | 4 | 0 | 0 |

## 3. Bảng ca khó

| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane | thiếu L1/R1 hay không có vạch | Không tạo lane | Ảnh chứng minh cho thấy không có vạch làn nhận biết được. |
| A06 | lane | thiếu R1 hay giao cắt không có vạch rõ | Không tạo R1 | Bối cảnh crosswalk/giao cắt; giữ ngoại lệ chờ xác nhận người kiểm. |
| A04 | lane | hai vạch đôi thật hay nét lặp | Cần kiểm lại | Có hai L1 và hai R2, tất cả `kind=double`; chưa có GT để kết luận. |

## 4. Phiếu QC 1

Phiếu rà soát A01–A06: [NguyenTruongGiang-qc1-draft.md](NguyenTruongGiang-qc1-draft.md). Người kiểm ghi trong phiếu: **Nguyễn Ngọc Đông — 2A202603291**.

| Mã lỗi | Số lỗi đã xác nhận | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-02 | 0 | A05 là ngoại lệ có ảnh; A06 chờ xác nhận | Không thêm lane tự suy diễn |
| QC1-05/06 | 0 đã xác nhận; 1 điểm cần xem lại | Cần xác minh A04 | Chưa thay đổi XML |

Chưa có thông tin về phiếu QC nhận được cho lô của Giang hoặc quyết định peer-review; không điền thay phần này.

## 5. Kiểm file export

| File bàn giao | Mở lại được? | Ảnh | Lint hiện tại | Ghi chú |
| --- | --- | ---: | --- | --- |
| `NguyenTruongGiang-front.zip` | Có | 16 | 6 nặng + 6 chính toàn lô | Đã gộp A01–A16; XML chỉ chứa nhãn, không kèm ảnh. |
| `NguyenTruongGiang-fisheye.zip` | Có | 12 | 0 cảnh báo riêng | Đã gộp B01–B12; XML chỉ chứa nhãn, không kèm ảnh. |
| `NguyenTruongGiang-manifest.json` | Có | 28 | `nặng: 6`, `chính: 6`, `nhẹ: 0` | Revision 1; SHA-256 hai ZIP được ghi trong manifest. |

Hai ZIP cuối cùng đã gộp toàn bộ 28 ảnh. So sánh sau khi gộp xác nhận tất cả shape/tag của bốn ZIP gốc được giữ nguyên; chỉ `image id` của các ảnh extra được đánh lại để không trùng ID.

## 6. Ảnh chụp màn hình

Đã có ảnh CVAT front cho A04–A11, gồm các minh chứng A04, A05, A06. Còn cần bổ sung trước khi nộp:

1. Ảnh tab **Labels** của project.
2. Một ảnh fisheye có polyline cong, phóng to.
3. Một ảnh/đoạn XML thể hiện `<polyline label="lane">`.

## 7. Tự đánh giá

Điểm cần tránh là suy diễn L1/R1 chỉ vì lint báo thiếu. Lint chỉ phát hiện cấu trúc; ở A05 ảnh không có vạch, nên thêm lane sẽ tạo nhãn sai. Ngược lại, A04 có nhiều polyline cùng `position` và `kind=double`, cần kiểm lại thay vì cho rằng tất cả cảnh báo là false positive.

Một polyline lane sai vị trí hoặc gán sai `position` sẽ tạo mục tiêu huấn luyện sai cho mô hình; ở các hàng gần xe, sai lệch này có thể làm hệ thống hỗ trợ giữ làn nhận nhầm ranh giới làn.

## 8. (Tùy chọn) Row-anchor

Chưa thực hiện vì không có kết quả so sánh với lô peer/GT.
