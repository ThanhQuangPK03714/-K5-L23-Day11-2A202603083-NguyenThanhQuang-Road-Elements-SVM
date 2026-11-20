# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Mạnh Đức (`nguyenmanhduc`), MSSV 2A202603153  
Người kiểm (học viên): Nguyễn Thanh Quang  
Ngày: 2026-11-20  
Phiên bản guideline: Road v1.0  
File được kiểm: `nguyenmanhduc-front.zip`, `nguyenmanhduc-fisheye.zip`; không có manifest nên revision chưa xác minh.  
Số ảnh kiểm: 6 (A01, A03, A08, B03, B05, B07)  
Số nhãn đã kiểm (shape + 4 tag slots/ảnh): 131 (107 shape + 24 tag slots).

Mẫu gồm ba ảnh front và ba ảnh fisheye, bao gồm front, fisheye rear và camera bên. Đã kiểm XML và đối chiếu hình vẽ với ảnh gốc trong `data/`. Hai ZIP mở được, mỗi ZIP có `annotations.xml` và không kèm ảnh. Ảnh đối chiếu: [montage sáu ảnh QC](./docs/images/submission-evidence/nguyenmanhduc-qc-sample.png).

Lint toàn bộ hai ZIP báo 56 cảnh báo; phiếu này chỉ kết luận trên mẫu sáu ảnh đã chọn. Các cảnh báo ở ảnh ngoài mẫu chưa được xác minh trực quan và không được tính vào bảng mẫu dưới đây.

## Ảnh đối chứng cho coach

**A01: 0 lỗi đã xác nhận trong phạm vi kiểm của phiếu.** Ảnh có một câu hỏi chưa kết luận về hai polyline L2 song song và `kind=double` (xem mục Ca mơ hồ); câu hỏi này chưa được tính là lỗi. Coach cần kiểm tra A01 cùng câu hỏi đang mở trước khi xác nhận đây là ảnh không lỗi.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 4 | 1 nặng, 3 nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 2 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 7 | 7 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 13 | 2 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 25 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 25 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 7 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 18 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 48 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 30 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 45 | 4 | chính |
| QC1-12 file | lỗi file | 2 ZIP | 1 | nhẹ |

## Danh sách lỗi

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-01 | B05 | tag:camera | Nặng | Thiếu tag camera; tên ảnh `B05_05780_MVL.png` yêu cầu `fisheye_left`. |
| 2 | QC1-01 | B05 | tag:timeofday | Nhẹ | Thiếu tag. |
| 3 | QC1-01 | B05 | tag:weather | Nhẹ | Thiếu tag. |
| 4 | QC1-01 | B05 | tag:source | Nhẹ | Thiếu tag. |
| 5 | QC1-02 | A03 | lane | Nặng | Thiếu R1; vạch sát bên phải làn xe nhìn thấy trong ảnh. |
| 6 | QC1-02 | A08 | lane | Nặng | Thiếu L1; vạch làn sát phía trái nhìn thấy trong ảnh. |
| 7 | QC1-03 | B05 | lane#3@(1123,443) | Nặng | Camera fisheye bên trái nhưng `position=L1`; phải là `other`. |
| 8 | QC1-03 | B05 | lane#4@(1121,402) | Nặng | Camera fisheye bên trái nhưng `position=L2`; phải là `other`. |
| 9 | QC1-03 | B05 | lane#5@(1196,603) | Nặng | Camera fisheye bên trái nhưng `position=L1`; phải là `other`. |
| 10 | QC1-03 | B07 | lane#2@(1121,244) | Nặng | Camera fisheye bên phải nhưng `position=R1`; phải là `other`. |
| 11 | QC1-03 | B07 | lane#3@(1079,200) | Nặng | Camera fisheye bên phải nhưng `position=R2`; phải là `other`. |
| 12 | QC1-03 | B07 | lane#4@(137,695) | Nặng | Camera fisheye bên phải nhưng `position=R1`; phải là `other`. |
| 13 | QC1-03 | B07 | lane#5@(126,513) | Nặng | Camera fisheye bên phải nhưng `position=R2`; phải là `other`. |
| 14 | QC1-04 | A08 | lane#7@(518,302) | Chính | Điểm đầu ở xa hơn điểm cuối; polyline đi ngược quy tắc gần ra xa. |
| 15 | QC1-04 | A08 | lane#8@(2,361) | Chính | Điểm đầu ở xa hơn điểm cuối; polyline đi ngược quy tắc gần ra xa. |
| 16 | QC1-11 | B03 | traffic_sign#0@(102,347) | Chính | Box ở vùng ngoài bán kính 80% nhưng `edge_zone=false`; cần bật. |
| 17 | QC1-11 | B03 | traffic_sign#16@(1129,362) | Chính | Box ở vùng ngoài bán kính 80% nhưng `edge_zone=false`; cần bật. |
| 18 | QC1-11 | B05 | traffic_sign#0@(353,39) | Chính | Box ở vùng ngoài bán kính 80% nhưng `edge_zone=false`; cần bật. |
| 19 | QC1-11 | B05 | traffic_sign#10@(417,5) | Chính | Box ở vùng ngoài bán kính 80% nhưng `edge_zone=false`; cần bật. |
| 20 | QC1-12 | B05 | road_curb#15@(576,55) | Nhẹ | Có một điểm polyline lặp liền nhau; xóa điểm thừa. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A01 | Hai polyline L2 song song biểu diễn vạch đôi nhìn thấy trong ảnh và đều có `kind=double`. Với vạch đôi, guideline muốn giữ hai polyline hay chỉ một polyline đại diện cho vạch? | Chưa có |

## Quyết định

Lỗi nặng: **10**  
Lỗi chính: **6 / 131 nhãn đã kiểm = 4.58%**  
Lỗi nhẹ: **4**  
Ca chờ lead: **1**

Quyết định: **Rework**  
Lý do: Có lỗi nặng ở QC1-01, QC1-02 và QC1-03; theo quy tắc chỉ cần một lỗi nặng là Rework. Tỷ lệ lỗi chính riêng lẻ chưa vượt 5%, nhưng không làm thay đổi quyết định. Cần hỏi lead về cách biểu diễn vạch đôi A01 trước khi đóng QC.
