# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` |Các loại xe con, xe gia đình, xe taxi, bán tải|Xe chở người cỡ nhỏ, trung, cabin liền thùng bán tải.|
| `truck` |Xe tải chở hàng, xe tải thùng lớn, xe container, xe đầu kéo.|Xe vận tải hàng hóa cỡ vừa đến lớn (không bao gồm xe bán tải cabin nhỏ vì nó thuộc car).|
| `bus` |Xe buýt công cộng, xe khách cỡ lớn.|Xe vận chuyển hành khách nhiều chỗ.|
| `van` |Xe tải van (xe thùng kín), có khoảng chở hàng hoặc chở người, thân xe kín|Nhỏ hơn bus lớn, thùng liền dạng hộp, kín|

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Vẽ bám sát tối đa phần thân xe nhìn thấy được, không thừa vạch đường, bầu trời hay khoảng không bên cạnh.
- Vật thể bị che khuất: Nếu xe bị xe khác hoặc chướng ngại vật che một phần, chỉ vẽ box quanh phần thân nhìn thấy được.
- Vật thể bị cắt bởi rìa ảnh: Vẽ box chạm đúng mép ảnh ở phần bị cắt, không kéo box ra ngoài mép ảnh.
- Vật thể rất nhỏ/mơ hồ: Nếu xe quá mờ/nhỏ không thể xác định thuộc 1 trong 4 lớp trên, không gán box; ghi lại ảnh đó vào mục ca mơ hồ bên dưới.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_037` |Không nhận biết được xe màu xanh thuộc loại xe nào|Không gán nhãn|Không có trong đặc điểm đã nhận dạng theo schema|
| `drive_041` |Xe con màu đen bị kẹt giữa xe taxi và xe buýt, chỉ nhìn thấy một phần rất nhỏ, không đáng kể|Không gán nhãn dù có thể nhận biết đó là car|Vật thể bị che khuất quá lớn, vùng thông tin nhận diện không đủ rõ ràng; gán nhãn sẽ tạo nhiễu cho mô hình và dễ vi phạm IoU.|
| `drive_042` |Không nhận biết được xe đang đi song song với xe tải|Không gán nhãn|Không biết chắc chắn kiểu xe, không hoàn toàn giống với xe nào trong schema|
