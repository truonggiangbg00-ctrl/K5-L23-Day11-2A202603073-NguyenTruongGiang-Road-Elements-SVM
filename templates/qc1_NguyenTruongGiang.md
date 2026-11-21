# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Trường Giang        Người kiểm (học viên):  Nguyễn Viết Quang
Ngày:  21/11/2026                        Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest):  NguyenTruongGiang_1
Số ảnh kiểm: 6 (+ 22 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag):  308

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 28 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 28 | 6 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 28 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 28 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 28 | 5 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 28 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 28 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 28 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 28 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 28 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 28 | 0 | chính |
| QC1-12 file | lỗi file | 28 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 nặng | A14 | A14 lane | nặng | chưa có R1 (bỏ qua vì thật sự không thấy vạch) |
| 2 | QC1-05 chính | A14 | id 26 và 27 | chính | 2 polyline cùng position L1: vạch đứt có bị tách (do là đường đôi) |
| 3 | QC1-05 chính | A04 | id 78 và 82 | chính | 2 polyline cùng position R2: vạch đứt có bị tách (do là đường đôi) |
| 4 | QC1-05 chính | A04 | id 83 và 84 | chính | 2 polyline cùng position L1: vạch đứt có bị tách (do là đường đôi) |
| 5 | QC1-02 nặng | A05 | A05 lane | nặng | chưa có L1 (bỏ qua vì thật sự không thấy vạch) |
| 6 | QC1-02 nặng | A05 | A05 lane | nặng | chưa có R1 (bỏ qua vì thật sự không thấy vạch) |
| 7 | QC1-02 nặng | A06 | A06 lane | nặng | chưa có R1 (bỏ qua vì thật sự không thấy vạch) |
| 8 | QC1-02 nặng | A07 | A07 lane | nặng | chưa có L1 (bỏ qua vì thật sự không thấy vạch) |
| 9 | QC1-02 nặng | A09 | A09 lane | nặng | chưa có R1 (bỏ qua vì thật sự không thấy vạch) |
| 10 | QC1-05 chính | A09 | id 128 và 130 | chính | 2 polyline cùng position L2: vạch đứt có bị tách (do là đường đôi) |
| 11 | QC1-05 chính | A011 | id 141 và 142 | chính | 2 polyline cùng position L2: vạch đứt có bị tách (do là đường đôi) |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Ảnh này không có vạch kẻ L1 R1 và chờ lead xác nhận đúng hay không |  |
| A06 | Ảnh này không có vạch kẻ L1 R1 và chờ lead xác nhận đúng hay không |  |
| A07 | Ảnh này không có vạch kẻ L1 và chờ lead xác nhận đúng hay không |  |
| A09 | Ảnh này không có vạch kẻ R1 và chờ lead xác nhận đúng hay không |  |
| A14 | Ảnh này không có vạch kẻ R1 và chờ lead xác nhận đúng hay không |  |

## Quyết định
Lỗi nặng: 6   Lỗi chính: 5 / 196 nhãn = 2.5 %   Lỗi nhẹ: 0   Ca chờ lead: 6  
Quyết định (Release / Hold / Rework): Hold
Lý do (theo luật của phiếu): Còn câu hỏi chưa được quyết định

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
