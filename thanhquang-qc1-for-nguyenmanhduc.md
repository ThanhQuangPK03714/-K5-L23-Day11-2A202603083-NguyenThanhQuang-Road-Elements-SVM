# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Mạnh Đức (`nguyenmanhduc`), MSSV 2A202603153  
Người kiểm (học viên): Nguyễn Thanh Quang  
Ngày: 2026-11-20  
Phiên bản guideline: Road v1.0  
File được kiểm: `nguyenmanhduc-front.zip`, `nguyenmanhduc-fisheye.zip`; phiếu không kèm manifest nên không gắn được kết quả với một revision cụ thể.
Số ảnh mẫu: 6 (A01, A03, A08, B03, B05, B07); ảnh đối chứng bổ sung ngoài mẫu: A02.
Số nhãn đã kiểm (shape + 4 tag slots/ảnh): 131 (107 shape + 24 tag slots).

Mẫu gồm ba ảnh front và ba ảnh fisheye, bao gồm front, fisheye rear và camera bên. Đã kiểm XML và đối chiếu hình vẽ với ảnh gốc trong `data/`. Hai ZIP mở được, mỗi ZIP có `annotations.xml` và không kèm ảnh. Ảnh đối chiếu: [montage sáu ảnh QC](./docs/images/submission-evidence/nguyenmanhduc-qc-sample.png).

Lint toàn bộ hai ZIP báo 56 cảnh báo; kết luận QC thống kê chỉ tính mẫu sáu ảnh đã chọn. Các cảnh báo ở ảnh ngoài mẫu không được tính vào bảng mẫu dưới đây.

Hai ZIP của Đức được tìm thấy trong thư mục dự án và được chạy LINT ngày 21/11/2026. SHA-256 của các bản dùng cho rà soát bổ sung:

- Front: `049aeff6049e94b87dc902aa6a5c9040e8c820da48ad9442cfb364ec82153be3`
- Fisheye: `221ba3ee68874fc228e4a6e7f28568dda6f7cc87b9f30e297b8c8f46e482f3d1`

Phiếu QC gốc không ghi hash/manifest nên các hash trên nhận diện bản ZIP hiện có, không chứng minh đây chính xác là byte-for-byte các file Đức đã mở lúc kiểm.

## Ảnh đối chứng cho coach

**A02: không phát hiện lỗi trong phạm vi rà soát bổ sung.** Ảnh có 7 shape và 4 tag; đủ tag `camera=front`, `timeofday=day`, `weather=clear`, `source=real`. LINT không báo lỗi trên A02; overlay được dựng từ ZIP và ảnh gốc rồi đối chiếu trực quan, các lane và vùng drivable bám theo mặt đường. A02 nằm ngoài mẫu 6 ảnh nên không cộng 11 mục của ảnh này vào mẫu số 131 hoặc tỉ lệ lỗi. Overlay để coach kiểm tra: [nguyenmanhduc-A02-control.png](./docs/images/submission-evidence/nguyenmanhduc-A02-control.png).

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 4 | 1 nặng, 3 nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 2 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 7 | 7 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 13 | 2 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 25 | 1 | chính |
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
| 21 | QC1-05 | A01 | lane (2 polyline L2) | Chính | Cùng một vạch đôi được biểu diễn bằng hai polyline `L2`, đều `kind=double`; guideline yêu cầu một polyline theo tâm cụm và gán `kind=double`. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A01 | Hai polyline L2 song song đều gán `kind=double`; biểu diễn thế nào theo guideline? | Đã đối chiếu [hướng dẫn CVAT của bài](./docs/huong_dan_cvat_bang_hinh.md): vạch đôi trên ảnh thật được biểu diễn bằng một polyline theo tâm cụm, `kind=double`. Đã phân loại hai polyline cho cùng cụm là lỗi QC1-05; đây là kết luận theo guideline, không phải lời đáp thay coach. |

## Quyết định

Lỗi nặng: **10**

Lỗi chính: **7 / 131 nhãn đã kiểm = 5.34%**

Lỗi nhẹ: **4**

Ca chờ lead: **0**

Quyết định: **Rework**  
Lý do: Có lỗi nặng ở QC1-01, QC1-02 và QC1-03; theo quy tắc chỉ cần một lỗi nặng là Rework. Tỉ lệ lỗi chính 5.34% cũng vượt ngưỡng 5%. A01 được phân loại theo hướng dẫn bài; ảnh đối chứng A02 nằm ngoài mẫu thống kê.
