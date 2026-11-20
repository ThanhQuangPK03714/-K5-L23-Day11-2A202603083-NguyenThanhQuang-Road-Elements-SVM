# Báo cáo cá nhân — Ngày 11

Họ tên: Nguyễn Thanh Quang  
Mã học viên: 2A202603083  
Phiên bản CVAT: 2.74.1 (API local `/api/server/about`)  
Guideline: Road v1.0  
Lần nộp (`revision` trong manifest): 3
Thời điểm tạo manifest revision 3: 20/11/2026 23:50:05 (UTC+7; từ `created_at` trong manifest).
Số lần nộp lại sau Rework: 2 (revision 2 và revision 3; chưa có xác nhận cuối cùng của coach).

> Trạng thái: chưa thể xác nhận hồ sơ đã hoàn tất hoặc đạt điểm tối đa. Revision 3 ưu tiên xác nhận coach rằng A09 không có R1; position của lane này đã trở về `L1`, còn `style=dashed` và chỉnh sửa vạch đôi theo nhận xét QC1. LINT vẫn cảnh báo hai lane `L1` ở A09; cần người kiểm/coach xác nhận cách diễn giải. Còn sáu cảnh báo chính chưa xác minh và ảnh Project settings hợp lệ còn thiếu.

## 1. Kiểm project

| Mục | Trạng thái | Ghi chú |
| --- | --- | --- |
| Schema 6 label và 4 tag | Đã xác minh trong metadata của cả hai ZIP | Đây là bằng chứng schema được export, không thay thế ảnh chụp trang cấu hình Project. |
| Cấu hình trực tiếp trên Project | Đã kiểm tra Project #2 trong CVAT | `d11_road_NguyenThanhQuang` có sáu label và bốn tag; tab Constructor xác nhận danh sách, tab Raw xác nhận kiểu và thuộc tính như bảng dưới. Ảnh chụp màn hình rõ làm minh chứng vẫn còn thiếu. |
| Bốn tag trên ảnh | Đủ trên cả 20 ảnh | Đã đối chiếu XML export: mỗi ảnh có camera, timeofday, weather và source cùng giá trị. |

| Label/tag | Kiểu và cấu hình theo metadata export |
| --- | --- |
| `lane` | Polyline; `position` = L1/R1/L2/R2/other; `style` = solid/dashed; `color` = white/yellow/other; `kind` = single/double |
| `road_curb` | Polyline; không có thuộc tính |
| `crosswalk` | Polygon; không có thuộc tính |
| `drivable` | Polygon; `area_type` = direct/alternative |
| `traffic_light` | Rectangle; `color` = red/yellow/green/off/unknown; `type` = vehicle/pedestrian/beacon; `facing` = front/side/back; `edge_zone` = checkbox |
| `traffic_sign` | Rectangle; `group` = prohibitory/mandatory/warning/information/supplementary/other; `facing` = front/side/back; `edge_zone` = checkbox |
| `camera` | Tag; `value` = front/fisheye_front/fisheye_rear/fisheye_left/fisheye_right |
| `timeofday` | Tag; `value` = day/dusk/night |
| `weather` | Tag; `value` = clear/overcast/rain/fog/other |
| `source` | Tag; `value` = real/simulated |

Cách kết thúc polyline mà người gán thực tế đã dùng: Người gán không nhớ thao tác/phím tắt; không ghi suy đoán thành trải nghiệm thực tế.
Cách chọn giá trị tag trong giao diện: Chưa xác nhận thao tác đã dùng; XML và Project Raw xác nhận cấu hình `value` và các giá trị đã lưu.

## 2. Số lượng đã gán

Số liệu shape lấy từ `thanhquang-manifest.json`; ZIP hiện tại gồm 12 ảnh front và 8 ảnh fisheye, không có ảnh nhúng.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 31 | 20 | 4 | 25 | 19 | 14 |
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
| A09 | lane | Coach xác nhận R1 không nhìn thấy; QC1 nhận định có vạch R1 và hai nét vạch đôi | Revision 3 không gán R1; lane này là `L1/dashed`, vạch đôi là `L1/double` | Đã ưu tiên xác nhận coach về việc không có R1; LINT vẫn báo hai lane cùng `L1`, cần xác nhận vạch đứt có phải lane riêng hay không. |
| A12 | lane | Thiếu L1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy L1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A08 | lane | Chiều polyline gần-ra-xa hay xa-ra-gần | Chưa xác minh | Còn cảnh báo QC1-04; hướng của đường gần ngang cần người kiểm xác nhận. |
| A09 | lane | Hai polyline L2 có phải vạch đôi hay bị tách | Đã gộp thành một `L1/kind=double` theo QC1 | Sau khi khôi phục position của lane còn lại theo xác nhận coach, LINT báo hai lane `L1`; cần người kiểm xác nhận cấu hình cuối. |
| B06, B07 | lane | `position=other` cho camera fisheye bên | Đã kiểm tra | ZIP revision 1 đã có `other`; QC1 ghi khác nhưng không kèm hash để đối chiếu. |
| B02–B05 | traffic_light / traffic_sign | `edge_zone` bật hay tắt | Đã bật theo gợi ý lint | Đã bật cho các box được cảnh báo và kiểm tra lại trong XML export. |
| B03 | lane#1 | Có đủ điểm theo cung fisheye không | Chưa xác minh | LINT: chỉ 3 điểm; cần nhìn ảnh trước khi quyết định thêm điểm. |
| B06 | road_curb#4 | Có đủ điểm theo cung fisheye không | Chưa xác minh | LINT: chỉ 3 điểm; cần nhìn ảnh trước khi quyết định thêm điểm. |
| B07 | lane#4, lane#5 | Có đủ điểm theo cung fisheye không | Chưa xác minh | LINT: mỗi polyline chỉ 3 điểm; cần nhìn ảnh trước khi quyết định thêm điểm. |

## 4. Phiếu QC 1 nhận được

Đã nhận phiếu QC1 do Nguyễn Mạnh Đức lập cho `thanhquang-front.zip` và `thanhquang-fisheye.zip`. Phiếu không kèm manifest hoặc hash nên không xác định được chính xác revision đã kiểm.

| Kết quả trên bộ file người kiểm đã nhận | Giá trị trong phiếu |
| --- | ---: |
| Lỗi nặng | 17 |
| Lỗi chính | 2 / 65 nhãn = 3,08% |
| Lỗi nhẹ | 18 |
| Quyết định | Rework |

Phiếu liệt kê 24 ô tag thiếu trong sáu ảnh mẫu, năm lỗi `position`, sáu màu đèn giao thông và hai lỗi cấu hình lane ở A09. Có bốn nhóm câu hỏi chờ lead: A05, A06, A08, B06/B07. Đây là số liệu của phiếu; chúng không tự động chứng minh trạng thái của ZIP revision 1.

### Đối chiếu từng mã QC1 với revision 3

| Mã | Số lỗi theo phiếu Đức | Đồng ý / đối chiếu với bộ hiện tại | Hành động và trạng thái |
| --- | ---: | --- | --- |
| QC1-01 | 24 | Chưa thể quy kết cho revision 1 vì phiếu không có hash; revision 1 và 3 có đủ bốn tag trên mỗi ảnh. | Không sửa tag; cần hash của bộ Đức đã kiểm để đối chiếu phần mâu thuẫn. |
| QC1-02 | 0 xác nhận riêng | Coach xác nhận các vạch thiếu trong A05/A06/A07/A09/A12 không nhìn thấy. | Giữ ngoại lệ; không tự vẽ thêm. |
| QC1-03 | 5 | B06/B07 đã có `position=other` từ revision 1; yêu cầu gán R1 ở A09 mâu thuẫn với xác nhận coach. | Không đổi B06/B07; A09 không có R1 theo coach. |
| QC1-04 | 0 xác nhận riêng | Chưa xác minh chiều lane A08; LINT vẫn cảnh báo. | Chưa sửa; cần đối chiếu ảnh. |
| QC1-05 | 0 xác nhận | A09 còn cảnh báo hai lane `L1`; cách biểu diễn chưa được chốt. | Đã gộp cặp vạch đôi theo QC1; còn chờ kiểm tra lane đứt riêng. |
| QC1-06 | 2 | Đồng ý với hai nhận xét cấu hình lane A09 trong phiếu. | Đã đặt vạch đôi thành `kind=double`, giữ lane còn lại `style=dashed`; position A09 theo xác nhận coach. |
| QC1-07 | 0 xác nhận | Không có lỗi được xác nhận trong mẫu. | Không có chỉnh sửa theo mã này. |
| QC1-08 | 6 | Đồng ý; sáu đèn A06/A08 đã được đối chiếu và đổi sang xanh. | Đã sửa trong revision 2 và giữ ở revision 3. |
| QC1-09 | 0 xác nhận | Không có lỗi được xác nhận trong mẫu. | Không có chỉnh sửa theo mã này. |
| QC1-10 | 0 xác nhận | Không có lỗi được xác nhận trong mẫu. | Không có chỉnh sửa theo mã này. |
| QC1-11 | 0 xác nhận riêng | Không có lỗi fisheye được kết luận trong mẫu; cảnh báo hình học LINT là các mục riêng chưa xác minh. | Chưa sửa các đường cong chỉ dựa trên cảnh báo tự động. |
| QC1-12 | 0 trong phạm vi mở file | Hai ZIP hiện tại mở được; phiếu không có manifest/hash để kiểm tra revision. | Không có lỗi mở file được ghi nhận; cần kèm manifest khi QC lại. |

### Đối chiếu revision được kiểm với ZIP hiện tại

Phiếu không có manifest/hash; các ZIP người kiểm dùng không có trong workspace. Hash của bản sao revision 1 khớp với hash ghi trong manifest revision 1. LINT/XML revision 1 xác nhận đủ bốn tag trên mỗi ảnh và mọi lane B06/B07 có `position=other`, khác với các nhận xét tag/position trong phiếu. Tuy nhiên, revision 1 có sáu đèn giao thông ở A06/A08 mang màu `red` và các vấn đề lane A09 được nêu trong phiếu. Do đó, chỉ một phần nhận xét QC có thể đối chiếu với revision 1; chưa thể xác định vì sao các nhận xét còn lại khác.

SHA-256 revision 1 (bản sao lưu), revision 2 (bản sao lưu) và revision 3:

- Revision 1 front: `04994b6b9e605289464d2415d138b2f34c403902b495223362037ece1779d214`
- Revision 2 front: `91f84f0ed0f9c7adfecdd3b2fa2a793d717fe146862aaabc363241c610dacd7f`
- Revision 3 front: `a8874c2f94c2f87a61fe139d65c307c91cbc4688d93e47a496cb5d7c55082f64`
- Fisheye (không đổi giữa hai revision): `8bea2df53a59e7efa65d024dcfec3b7444023e2a48ac618e33f2ee3a43e5d25a`

Revision 2 đổi sáu đèn được QC1 xác định là xanh tại A06/A08; gộp hai nét vạch đôi A09 thành một lane `position=L1`, `kind=double`, và đổi lane còn lại thành `position=R1`, `style=dashed`. Theo lựa chọn của người nộp, revision 3 khôi phục `position=L1` cho lane đứt theo xác nhận coach rằng A09 không có R1, đồng thời giữ `style=dashed` và vạch đôi đã gộp. Revision 3 cần được đồng bộ lại lên CVAT task front #20. LINT vẫn cảnh báo hai lane cùng `L1`; không tự điền lời đáp cho lead.

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

Ca mơ hồ A01 trong phiếu của Đức (hai polyline L2 song song, cùng `kind=double`) chưa có lời đáp từ lead. Câu hỏi này vẫn mở; chưa ghi nhận câu trả lời hoặc gửi xác nhận thay người dùng.

## 5. Kiểm file export

Hai ZIP mở được bằng bộ đọc CVAT for images 1.1 của repository. `contains_images=false` cho cả hai. Các số shape dưới đây là số shape trong hai ảnh đầu mỗi bộ; lint đọc được XML nhưng không xác nhận chất lượng nhãn so với ảnh gốc. Manifest revision 3 ghi front 12 ảnh/113 shapes và fisheye 8 ảnh/49 shapes.

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `thanhquang-front.zip` | Có | A01: 9 | A02: 7 | Có |
| `thanhquang-fisheye.zip` | Có | B01: 4 | B02: 8 | Có |

Revision 3 đã được nhập vào CVAT job #20; API xác nhận front có 113 shapes, 48 tag slots và trạng thái `completed` (12/12 frames). A09 trên CVAT hiện có một lane `L1/double` và một lane `L1/dashed`, không còn `R1`. Fisheye job #21 vẫn `completed` (8/8 frames), có 49 shapes và 32 tag slots.

Kết quả LINT chạy trực tiếp trên hai ZIP revision 3: 20 ảnh, 12 cảnh báo, gồm 6 cảnh báo nặng QC1-02 (A05: L1/R1; A06: R1; A07: L1; A09: R1; A12: L1) đã được coach xác nhận ngoại lệ, và 6 cảnh báo chính chưa xác minh: chiều lane A08; hai lane cùng `L1` ở A09; số điểm theo cung ở B03 lane#1, B06 road_curb#4, B07 lane#4 và lane#5. Không còn cảnh báo nhẹ. LINT không kết luận chất lượng hình học; các trường hợp trên vẫn cần đối chiếu ảnh.

## 6. Ảnh chụp màn hình

Ảnh chụp CVAT có chứa khung hình BDD100K/WoodScape được giữ cục bộ để dùng trong bộ nộp theo kênh coach chỉ định; không commit lên repository công khai theo [quy định nguồn dữ liệu](./ATTRIBUTION.md). Các đường dẫn dưới đây tồn tại trên máy làm bài, không được đồng bộ lên GitHub.

1. **Còn thiếu:** ảnh trang Project > Labels có cấu hình 6 label, thuộc tính và 4 tag. `labels-tags-task21.png` và `labels-tags-task21-lower.png` chỉ chụp sidebar trong Job, không thay thế được ảnh Project settings.
2. Ảnh canvas front A01 trong task #20: `docs/images/submission-evidence/front-task20.png`.
3. Ảnh canvas fisheye B01 trong task #21: `docs/images/submission-evidence/fisheye-task21.png`. Giá trị tag được xác minh trong XML.
4. XML A01 trích từ ZIP front hiện tại: [annotations-front-A01.xml](./docs/images/submission-evidence/annotations-front-A01.xml), cùng [ảnh chụp XML](./docs/images/submission-evidence/xml-front-A01.png). XML có đủ 4 tag cùng các shape của ảnh; hai file XML minh chứng không chứa ảnh gốc.

Ba loại minh chứng (front, fisheye, XML) hiện có trên máy. Ảnh Project settings chưa có. Bốn minh chứng phải được gửi kèm riêng cùng report qua kênh coach chấp nhận; không commit ảnh chứa dữ liệu nguồn lên repository công khai theo quy định nguồn dữ liệu.

## 7. Tự đánh giá

QC1 đã phát hiện sáu màu đèn giao thông A06/A08 và các nét lane A09 cần chỉnh. Revision 3 giữ sáu màu đèn xanh, gộp vạch đôi A09, và bỏ gán `R1` theo xác nhận coach. Nếu giữ màu đèn sai hoặc tách vạch đôi thành hai lane độc lập, mô hình có thể học nhầm trạng thái đèn và cấu trúc làn. `position=other` trên các lane B06/B07 đã có từ revision 1. LINT revision 3 còn 12 cảnh báo: 6 QC1-02 có xác nhận ngoại lệ và 6 cảnh báo chính chưa xác minh. Cách kết thúc polyline và thao tác đặt tag vẫn chưa được người gán xác nhận; không suy đoán thay cho trải nghiệm thực tế. A09 còn cần người kiểm xác nhận vì LINT thấy hai lane `L1`.

Nhãn là Ground Truth dùng để huấn luyện/đánh giá mô hình. Nếu thiếu tag, pixel và shape không đổi nhưng dữ liệu sẽ mất khả năng phân nhóm theo camera, thời điểm và thời tiết; điều đó có thể che khuất chênh lệch hiệu năng giữa các điều kiện. Ở lần export hiện tại, cả 20 ảnh đã có đủ tag; chưa xác nhận các cảnh báo hình học còn lại đã được sửa.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

Chưa thực hiện; đây là phần tùy chọn.
