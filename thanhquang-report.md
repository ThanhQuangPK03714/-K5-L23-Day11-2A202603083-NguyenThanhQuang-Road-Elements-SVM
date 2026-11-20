# Báo cáo cá nhân — Ngày 11

Họ tên: Nguyễn Thanh Quang  
Mã học viên: 2A202603083  
Phiên bản CVAT: 2.74.1 (API local `/api/server/about`)  
Guideline: Road v1.0  
Lần nộp (`revision` trong manifest): 3
Thời điểm tạo manifest revision 3: 20/11/2026 23:50:05 (UTC+7; từ `created_at` trong manifest).
Số lần nộp lại sau Rework: 2 (revision 2 và revision 3; đang chờ coach xác nhận kết quả sửa cuối).

> Trạng thái: các file đã đồng bộ revision 3. Sáu cảnh báo chính đã được rà bằng overlay; A08/A09 còn cần chốt cách diễn giải, còn B03/B06/B07 không có lệch lớn hiển nhiên nhưng chưa thể đo ngưỡng 5 px nếu thiếu GT. Ảnh Project Settings cần được lưu thành file đính kèm. Revision 3 giữ coach exception A09 không có R1; position của lane này là `L1`, cùng `style=dashed` và vạch đôi đã gộp. LINT vẫn cảnh báo hai lane `L1` ở A09.

## 1. Kiểm project

| Mục | Trạng thái | Ghi chú |
| --- | --- | --- |
| Schema 6 label và 4 tag | Đã đối chiếu output `py -3.11 -m road_lab.taxonomy`, metadata của cả hai ZIP và Project Raw | Đây là bằng chứng cấu hình, không thay thế ảnh chụp trang Project Settings. |
| Cấu hình trực tiếp trên Project | Đã kiểm tra Project #2 trong CVAT | `d11_road_NguyenThanhQuang` có sáu label và bốn tag; tab Constructor xác nhận danh sách, tab Raw xác nhận kiểu và thuộc tính như bảng dưới. Cần lưu ảnh Project Settings để đính kèm làm minh chứng. |
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

Cách hoàn tất polyline theo tài liệu CVAT: nhấn `N` lần nữa hoặc bấm `Done`; người gán không nhớ thao tác thực tế đã dùng nên đây là hướng dẫn, không phải xác nhận trải nghiệm ([CVAT docs](https://docs.cvat.ai/docs/annotation/manual-annotation/shapes/annotation-with-polylines/)).
Cách gán tag theo tài liệu CVAT: chuyển menu trên cùng sang `Tag annotation`, chọn label rồi bấm `Plus`; người gán không nhớ thao tác thực tế đã dùng ([CVAT docs](https://docs.cvat.ai/docs/annotation/manual-annotation/modes/annotation-with-tags/)). XML và Project Raw xác nhận cấu hình `value` cùng các giá trị đã lưu.

## 2. Số lượng đã gán

Số liệu shape lấy từ `thanhquang-manifest.json`; ZIP hiện tại gồm 12 ảnh front và 8 ảnh fisheye, không có ảnh nhúng.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 31 | 20 | 4 | 25 | 19 | 14 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 7 | 17 | 8 | 6 | 2 | 9 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó

Các dòng dưới đây ghi các ca đã đối chiếu bằng LINT và overlay; cảnh báo tự động không tự nó chứng minh có lỗi hoặc phản ánh trải nghiệm cá nhân.

| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do / việc cần xác minh |
| --- | --- | --- | --- | --- |
| A05 | lane | Thiếu L1/R1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy L1/R1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A06 | lane | Thiếu R1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy R1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A07 | lane | Thiếu L1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy L1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A09 | lane | Coach xác nhận R1 không nhìn thấy; QC1 nhận định có vạch R1 và hai nét vạch đôi | Revision 3 không gán R1; lane này là `L1/dashed`, vạch đôi là `L1/double` | Đã ưu tiên xác nhận coach về việc không có R1; LINT vẫn báo hai lane cùng `L1`, cần xác nhận vạch đứt có phải lane riêng hay không. |
| A12 | lane | Thiếu L1 hay ảnh thật sự không thấy vạch | Coach xác nhận không thấy L1 | Không thêm nét; ngoại lệ QC1-02 được ghi ở mục 4. |
| A08 | lane#25 | Hướng vẽ của một nét gần ngang; nét lane hay vạch dừng | Đã rà ảnh gốc và overlay | Nét gần ngang ở vùng giao lộ; LINT báo hướng, còn phiếu QC đặt câu hỏi nó có phải vạch dừng không. Không đổi nhãn khi chưa chốt loại đối tượng. |
| A09 | lane | Hai polyline L2 có phải vạch đôi hay bị tách | Đã rà ảnh gốc/overlay; revision 3 có `L1/kind=double` và `L1/dashed` | Coach xác nhận R1 không nhìn thấy, nhưng LINT vẫn báo hai lane cùng `L1`; cần người kiểm chốt cách diễn giải lane đứt. |
| B06, B07 | lane | `position=other` cho camera fisheye bên | Đã kiểm tra | ZIP revision 1 đã có `other`; QC1 ghi khác nhưng không kèm hash để đối chiếu. |
| B02–B05 | traffic_light / traffic_sign | `edge_zone` bật hay tắt | Đã bật theo gợi ý lint | Đã bật cho các box được cảnh báo và kiểm tra lại trong XML export. |
| B03 | lane#1 | Độ bám cung fisheye | Đã rà ảnh gốc và overlay; không thấy lệch lớn hiển nhiên | LINT chỉ đếm 3 điểm; không thể xác nhận sai số ≤5 px nếu thiếu GT. Không tự thêm điểm. |
| B06 | road_curb#4 | Độ bám cung fisheye | Đã rà ảnh gốc và overlay; không thấy lệch lớn hiển nhiên | LINT chỉ đếm 3 điểm; không thể xác nhận sai số ≤5 px nếu thiếu GT. Không tự thêm điểm. |
| B07 | lane#4, lane#5 | Độ bám cung fisheye | Đã rà ảnh gốc và overlay; không thấy lệch lớn hiển nhiên | Mỗi polyline có 3 điểm; LINT không đo độ lệch tới GT. Không tự thêm điểm. |

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
| QC1-01 | 24 | Phiếu không kèm hash nên không đủ căn cứ quy kết lỗi tag cho revision 1; revision 1 và 3 có đủ bốn tag trên mỗi ảnh. | Không sửa tag; cần hash của bộ Đức đã kiểm để đối chiếu phần mâu thuẫn. |
| QC1-02 | 0 xác nhận riêng | Coach xác nhận các vạch thiếu trong A05/A06/A07/A09/A12 không nhìn thấy. | Giữ ngoại lệ; không tự vẽ thêm. |
| QC1-03 | 5 | B06/B07 đã có `position=other` từ revision 1; yêu cầu gán R1 ở A09 mâu thuẫn với xác nhận coach. | Không đổi B06/B07; A09 không có R1 theo coach. |
| QC1-04 | 0 xác nhận riêng | Đang chờ đối chiếu chiều lane A08; LINT vẫn cảnh báo. | Chưa chỉnh sửa; cần đối chiếu ảnh. |
| QC1-05 | 0 xác nhận | A09 còn cảnh báo hai lane `L1`; cách biểu diễn chưa được chốt. | Đã gộp cặp vạch đôi theo QC1; còn chờ kiểm tra lane đứt riêng. |
| QC1-06 | 2 | Đồng ý với hai nhận xét cấu hình lane A09 trong phiếu. | Đã đặt vạch đôi thành `kind=double`, giữ lane còn lại `style=dashed`; position A09 theo xác nhận coach. |
| QC1-07 | 0 xác nhận | Không có lỗi được xác nhận trong mẫu. | Không có chỉnh sửa theo mã này. |
| QC1-08 | 6 | Đồng ý; sáu đèn A06/A08 đã được đối chiếu và đổi sang xanh. | Đã sửa trong revision 2 và giữ ở revision 3. |
| QC1-09 | 0 xác nhận | Không có lỗi được xác nhận trong mẫu. | Không có chỉnh sửa theo mã này. |
| QC1-10 | 0 xác nhận | Không có lỗi được xác nhận trong mẫu. | Không có chỉnh sửa theo mã này. |
| QC1-11 | 0 xác nhận riêng | Không có lỗi fisheye được kết luận trong mẫu của Đức; các cảnh báo hình học trên ZIP của tôi đã được rà overlay, không thấy lệch lớn hiển nhiên. | Không chỉnh sửa đường cong chỉ theo cảnh báo số điểm; cần GT để xác nhận ngưỡng 5 px. |
| QC1-12 | 0 trong phạm vi mở file | Hai ZIP hiện tại mở được; phiếu không có manifest/hash để kiểm tra revision. | Không có lỗi mở file được ghi nhận; cần kèm manifest khi QC lại. |

### Đối chiếu revision được kiểm với ZIP hiện tại

Phiếu không kèm manifest/hash; các ZIP người kiểm dùng không có trong workspace. Hash của bản sao revision 1 khớp với hash ghi trong manifest revision 1. LINT/XML revision 1 xác nhận đủ bốn tag trên mỗi ảnh và mọi lane B06/B07 có `position=other`, khác với các nhận xét tag/position trong phiếu. Tuy nhiên, revision 1 có sáu đèn giao thông ở A06/A08 mang màu `red` và các vấn đề lane A09 được nêu trong phiếu. Vì thiếu bản ZIP kèm hash của người kiểm, không đủ dữ liệu giải thích các khác biệt còn lại.

SHA-256 revision 1 (bản sao lưu), revision 2 (bản sao lưu) và revision 3:

- Revision 1 front: `04994b6b9e605289464d2415d138b2f34c403902b495223362037ece1779d214`
- Revision 2 front: `91f84f0ed0f9c7adfecdd3b2fa2a793d717fe146862aaabc363241c610dacd7f`
- Revision 3 front: `a8874c2f94c2f87a61fe139d65c307c91cbc4688d93e47a496cb5d7c55082f64`
- Fisheye (không đổi giữa hai revision): `8bea2df53a59e7efa65d024dcfec3b7444023e2a48ac618e33f2ee3a43e5d25a`

Revision 2 đổi sáu đèn được QC1 xác định là xanh tại A06/A08; gộp hai nét vạch đôi A09 thành một lane `position=L1`, `kind=double`, và đổi lane còn lại thành `position=R1`, `style=dashed`. Theo lựa chọn của người nộp, revision 3 khôi phục `position=L1` cho lane đứt theo xác nhận coach rằng A09 không có R1, đồng thời giữ `style=dashed` và vạch đôi đã gộp. Revision 3 đã được nhập lại vào CVAT task front #20; API xác nhận job `completed` với 12/12 ảnh và 113 shapes. LINT vẫn cảnh báo hai lane cùng `L1`; không tự điền lời đáp cho lead.

### Xác nhận ngoại lệ QC1-02 cho lô của tôi

Ngày 20/11/2026, coach xác nhận các vạch L1/R1 còn thiếu dưới đây không nhìn thấy trong ảnh. Không tự vẽ thêm; ghi nhận theo ngoại lệ tại [đặc tả bàn giao](./docs/delivery_road_v1.0.md). `road_check lint` vẫn đếm 6 cảnh báo nặng này trong manifest.

| Ảnh | Vạch không nhìn thấy theo xác nhận của coach |
| --- | --- |
| A05 | L1, R1 |
| A06 | R1 |
| A07 | L1 |
| A09 | R1 |
| A12 | L1 |

Phiếu QC1 tôi lập cho bạn được ghép: [Nguyễn Mạnh Đức (2A202603153)](./thanhquang-qc1-for-nguyenmanhduc.md). Kết quả mẫu 6 ảnh: Rework; 10 lỗi nặng, 7 lỗi chính / 131 mục = 5.34%, 4 lỗi nhẹ. A02 được rà riêng làm ảnh đối chứng ngoài mẫu và không cộng vào tỉ lệ. Đây là QC bộ dữ liệu của bạn ấy, không phải phiếu QC nhận về cho bộ của tôi.

A01 trong phiếu QC tôi lập cho Đức đã được đối chiếu với hướng dẫn bài: vạch đôi được biểu diễn bằng một polyline theo tâm cụm với `kind=double`; hai polyline song song cho cùng cụm được phân loại QC1-05. Đây là kết luận theo guideline, không phải câu trả lời thay coach.

## 5. Kiểm file export

Hai ZIP mở được bằng bộ đọc CVAT for images 1.1 của repository. `contains_images=false` cho cả hai. Các số shape dưới đây là số shape trong hai ảnh đầu mỗi bộ; lint đọc được XML nhưng không xác nhận chất lượng nhãn so với ảnh gốc. Manifest revision 3 ghi front 12 ảnh/113 shapes và fisheye 8 ảnh/49 shapes.

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `thanhquang-front.zip` | Có | A01: 9 | A02: 7 | Có |
| `thanhquang-fisheye.zip` | Có | B01: 4 | B02: 8 | Có |

Revision 3 đã được nhập vào CVAT job #20; API xác nhận front có 113 shapes, 48 tag slots và trạng thái `completed` (12/12 frames). A09 trên CVAT hiện có một lane `L1/double` và một lane `L1/dashed`, không còn `R1`. Fisheye job #21 vẫn `completed` (8/8 frames), có 49 shapes và 32 tag slots.

Kết quả LINT trực tiếp trên hai ZIP revision 3: 20 ảnh, 12 cảnh báo; 6 cảnh báo nặng QC1-02 (A05: L1/R1; A06: R1; A07: L1; A09: R1; A12: L1) có xác nhận ngoại lệ của coach, 6 cảnh báo chính. Overlay A08 cho thấy nét gần ngang ở giao lộ nhưng chưa phân biệt được lane với vạch dừng; A09 vẫn có hai lane `L1`; B03/B06/B07 đã được rà trực quan, không thấy lệch lớn hiển nhiên nhưng LINT không đo sai số ≤5 px khi thiếu GT. Không còn cảnh báo nhẹ; không tự sửa hình học khi chưa đủ căn cứ.

## 6. Ảnh chụp màn hình

Ảnh chụp CVAT có chứa khung hình BDD100K/WoodScape được giữ cục bộ để dùng trong bộ nộp theo kênh coach chỉ định; không commit lên repository công khai theo [quy định nguồn dữ liệu](./ATTRIBUTION.md). Các đường dẫn dưới đây tồn tại trên máy làm bài, không được đồng bộ lên GitHub.

1. **Cần đính kèm:** ảnh trang Project > Labels có cấu hình 6 label, thuộc tính và 4 tag. `labels-tags-task21.png` và `labels-tags-task21-lower.png` chỉ chụp sidebar trong Job, không thay thế được ảnh Project settings.
2. Ảnh canvas front A01 trong task #20: `docs/images/submission-evidence/front-task20.png`.
3. Ảnh canvas fisheye B01 trong task #21: `docs/images/submission-evidence/fisheye-task21.png`. Giá trị tag được xác minh trong XML.
4. XML A01 trích từ ZIP front hiện tại: [annotations-front-A01.xml](./docs/images/submission-evidence/annotations-front-A01.xml), cùng [ảnh chụp XML](./docs/images/submission-evidence/xml-front-A01.png). XML có đủ 4 tag cùng các shape của ảnh; hai file XML minh chứng không chứa ảnh gốc.

Ba loại minh chứng (front, fisheye, XML) hiện có trên máy. Ảnh Project Settings cần được lưu và gửi riêng cùng report qua kênh coach chấp nhận; không commit ảnh chứa dữ liệu nguồn lên repository công khai theo quy định nguồn dữ liệu.

## 7. Tự đánh giá

QC1 đã phát hiện sáu màu đèn giao thông A06/A08 và các nét lane A09 cần chỉnh. Revision 3 giữ sáu màu đèn xanh, gộp vạch đôi A09, và bỏ gán `R1` theo xác nhận coach. Nếu giữ màu đèn sai hoặc tách vạch đôi thành hai lane độc lập, mô hình có thể học nhầm trạng thái đèn và cấu trúc làn. `position=other` trên các lane B06/B07 đã có từ revision 1. LINT revision 3 còn 12 cảnh báo: 6 QC1-02 có xác nhận ngoại lệ; 6 cảnh báo chính đã được rà ảnh/overlay. A08 cần chốt lane hay vạch dừng, A09 cần chốt ý nghĩa hai lane `L1`; B03/B06/B07 không có lệch lớn hiển nhiên nhưng cần GT để xác nhận ngưỡng 5 px. Người gán không nhớ thao tác cụ thể kết thúc polyline/gán tag, nên report chỉ ghi hướng dẫn CVAT, không nhận đó là trải nghiệm cá nhân.

Nhãn là Ground Truth dùng để huấn luyện/đánh giá mô hình. Nếu thiếu tag, pixel và shape không đổi nhưng dữ liệu sẽ mất khả năng phân nhóm theo camera, thời điểm và thời tiết; điều đó có thể che khuất chênh lệch hiệu năng giữa các điều kiện. Ở lần export hiện tại, cả 20 ảnh đã có đủ tag. Các cảnh báo hình học vẫn còn trong ZIP revision 3; kết quả rà trực quan và giới hạn đo sai số được ghi ở mục 5.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

Phần buffer là tùy chọn, không nằm trong 5 file bắt buộc.
