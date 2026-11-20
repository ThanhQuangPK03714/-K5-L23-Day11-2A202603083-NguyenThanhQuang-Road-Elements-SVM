# Báo cáo cá nhân — Ngày 11

Họ tên: Nguyễn Thanh Quang  
Mã học viên: 2A202603083  
Phiên bản CVAT: 2.74.1 (API local `/api/server/about`)  
Guideline: Road v1.0  
Lần nộp (`revision` trong manifest): 1  
Thời điểm export: 20/11/2026 22:27 (giờ máy, UTC+7); export qua CVAT API 2.74.1.  
Số lần nộp lại sau Rework: 0 theo `revision=1`.  

> Trạng thái: bộ hồ sơ đáp ứng các điều kiện nộp bắt buộc trong checklist sau khi ghi nhận ngoại lệ QC1-02 đã được coach xác nhận ở mục 4. Cả 20 ảnh có đủ 4 tag và hai ZIP đã export lại. Manifest vẫn đếm 6 cảnh báo nặng này; còn 6 cảnh báo chính chưa được xác minh trực quan, nên không khẳng định chúng đã được sửa hay bảo đảm kết quả chấm.

## 1. Kiểm project

| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| Tên 6 label và 4 tag | Đã thấy trong sidebar job #21 | Danh sách tên hiện trong CVAT; kiểu hình và cấu hình thuộc tính cần xác nhận trong project settings. Xem ảnh minh chứng ở mục 6. |
| Thuộc tính và giá trị | Chưa xác minh | Cần đối chiếu với taxonomy Road v1.0 trên project. |
| 4 tag ảnh | Đủ trên cả 20 ảnh | Đã đối chiếu từng frame trong XML export với tên camera, timeofday, weather và source. |

Cách kết thúc polyline trên bản CVAT này: Chưa xác minh.  
Cách đặt tag ảnh trên bản CVAT này: Chưa xác minh.

## 2. Số lượng đã gán

Số liệu shape lấy từ `thanhquang-manifest.json`; ZIP hiện tại gồm 12 ảnh front và 8 ảnh fisheye, không có ảnh nhúng.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 32 | 20 | 4 | 25 | 19 | 14 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 7 | 17 | 8 | 6 | 2 | 9 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó

Các dòng dưới đây là cảnh báo lint cần đối chiếu với ảnh/CVAT, không phải xác nhận rằng chúng là lỗi hoặc là các ca khó tôi đã gặp.

| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do / việc cần xác minh |
| --- | --- | --- | --- | --- |
| A05 | lane | Thiếu L1/R1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy L1/R1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A06 | lane | Thiếu R1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy R1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A07 | lane | Thiếu L1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy L1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A09 | lane | Thiếu R1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy R1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A12 | lane | Thiếu L1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy L1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A08 | lane | Chiều polyline gần-ra-xa hay xa-ra-gần | Chưa xác minh | Còn cảnh báo QC1-04; hướng của đường gần ngang cần người kiểm xác nhận. |
| A09 | lane | Hai polyline L2 có phải vạch đôi hay bị tách | Chưa xác minh | Còn cảnh báo QC1-05; cần đối chiếu ảnh với quy tắc `kind=double`. |
| B06, B07 | lane | `position=other` cho camera fisheye bên | Đã sửa | Mọi lane trong hai ảnh đã đặt `other` theo guideline. |
| B02–B05 | traffic_light / traffic_sign | `edge_zone` bật hay tắt | Đã bật theo gợi ý lint | Đã bật cho các box được cảnh báo và kiểm tra lại trong XML export. |
| B03, B06, B07 | lane / road_curb | Polyline fisheye có đủ điểm theo cung | Chưa xác minh | Còn 4 cảnh báo QC1-11 về đường 3 điểm; cần kiểm tra độ cong trên ảnh trước khi thêm điểm. |

## 4. Phiếu QC 1 nhận được

Bạn kiểm lô của tôi: Chưa có phiếu QC1 thực tế được cung cấp.  
Quyết định nhận được: Chưa có.

Chưa điền bảng lỗi vì chưa có phiếu của người kiểm. Không tạo kết quả QC giả.

### Xác nhận ngoại lệ QC1-02 cho lô của tôi

Ngày 20/11/2026, coach xác nhận các vạch L1/R1 còn thiếu dưới đây không nhìn thấy trong ảnh. Không tự vẽ thêm; ghi nhận theo ngoại lệ tại [đặc tả bàn giao](./docs/delivery_road_v1.0.md). `road_check lint` vẫn đếm 6 cảnh báo nặng này trong manifest.

| Ảnh | Vạch không nhìn thấy theo xác nhận của coach |
| --- | --- |
| A05 | L1, R1 |
| A06 | R1 |
| A07 | L1 |
| A09 | R1 |
| A12 | L1 |

Phiếu QC1 tôi lập cho bạn được ghép: [Nguyễn Mạnh Đức (2A202603153)](./thanhquang-qc1-for-nguyenmanhduc.md). Kết quả kiểm mẫu 6 ảnh: Rework; 10 lỗi nặng, 6 lỗi chính và 4 lỗi nhẹ. Đây là QC bộ dữ liệu của bạn ấy, không phải phiếu QC nhận về cho bộ của tôi.

## 5. Kiểm file export

Hai ZIP mở được bằng bộ đọc CVAT for images 1.1 của repository. `contains_images=false` cho cả hai. Các số shape dưới đây là số shape trong hai ảnh đầu mỗi bộ; lint đọc được XML nhưng không xác nhận chất lượng nhãn so với ảnh gốc.

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `thanhquang-front.zip` | Có | A01: 9 | A02: 7 | Có |
| `thanhquang-fisheye.zip` | Có | B01: 4 | B02: 8 | Có |

Kết quả lint sau export: 20 ảnh; 12 cảnh báo gồm 6 nặng (đều là QC1-02 thiếu L1/R1 đã được coach xác nhận ngoại lệ) và 6 chính. Không còn cảnh báo nhẹ. Theo đặc tả bàn giao, QC1-02 này được miễn sau khi coach xác nhận; các cảnh báo chính còn lại cần tự-QC nhưng không phải điều kiện chặn nộp trong checklist.

## 6. Ảnh chụp màn hình

Ảnh chụp CVAT có chứa khung hình BDD100K/WoodScape được giữ cục bộ để dùng trong bộ nộp theo kênh coach chỉ định; không commit lên repository công khai theo [quy định nguồn dữ liệu](./ATTRIBUTION.md). Các đường dẫn dưới đây tồn tại trên máy làm bài, không được đồng bộ lên GitHub.

1. Danh sách label/tag trong sidebar job #21: `docs/images/submission-evidence/labels-tags-task21.png` và `docs/images/submission-evidence/labels-tags-task21-lower.png`. Đây là danh sách ở job, không phải trang cấu hình project.
2. Ảnh canvas front A01 trong task #20: `docs/images/submission-evidence/front-task20.png`.
3. Ảnh canvas fisheye B01 trong task #21: `docs/images/submission-evidence/fisheye-task21.png`. Giá trị tag được xác minh trong XML.
4. XML A01 trích từ ZIP front hiện tại: [annotations-front-A01.xml](./docs/images/submission-evidence/annotations-front-A01.xml), cùng [ảnh chụp XML](./docs/images/submission-evidence/xml-front-A01.png). XML có đủ 4 tag cùng các shape của ảnh; hai file XML minh chứng không chứa ảnh gốc.

## 7. Tự đánh giá

Trong các vấn đề lặp lại được phát hiện khi tự-QC, lỗi thuộc tính `position` trên camera fisheye bên xuất hiện ở bốn lane tại B06/B07; các lane này đã được đặt về `other`. Nếu giữ L1/R1 cho camera bên, mô hình học thuộc tính vị trí làn sai theo góc camera. Cách tránh là kiểm tra ánh xạ camera → `position` cho từng ảnh trước export. Cả 20 ảnh hiện đủ bốn tag; lint còn 12 gợi ý (6 nặng QC1-02 được coach xác nhận ngoại lệ, 6 chính chưa được xác minh). Các cảnh báo chính không chặn nộp theo checklist nhưng chưa được xác nhận là đúng.

Nhãn là Ground Truth dùng để huấn luyện/đánh giá mô hình. Nếu thiếu tag, pixel và shape không đổi nhưng dữ liệu sẽ mất khả năng phân nhóm theo camera, thời điểm và thời tiết; điều đó có thể che khuất chênh lệch hiệu năng giữa các điều kiện. Ở lần export hiện tại, cả 20 ảnh đã có đủ tag; chưa xác nhận các cảnh báo hình học còn lại đã được sửa.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

Chưa thực hiện; đây là phần tùy chọn.
