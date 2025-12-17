# I. Địa chỉ và các vấn đề liên quan
- `Quá trình gán địa chỉ`: Chương trình viết bằng ngôn ngữ bậc cao trải qua quá trình dịch và liên kết trước khi được tải vào bộ nhớ để thực hiện
  - `Địa chỉ Logic(tương đối)`: Là địa chỉ được gán cho lệnh và dữ liệu, không phụ thuộc vào vị trí cụ thể của tiến trình trong bộ nhớ. Chương trình ứng dụng chỉ làm việc với địa chỉ logic này. 
  - `Địa chỉ vật lý(tuyệt đối)`: Là địa chỉ chính xác trong bộ nhớ máy tính, được sử dụng bởi các mạch nhớ để truy cập chương trình và dữ liệu
  - `Ánh xạ địa chỉ`: Địa chỉ logic được chuyển thành địa chỉ vật lý nhờ khối **Ánh xạ địa chỉ (MMU)**

# II. Các yêu cầu quản lý bộ nhớ
HDH phải đáp ứng các yêu cầu sau khi quản lý bộ nhớ trong môi trường đa chương trình:

- `Cấp phát lại (Relocation)`: Tiến trình phải có khả năng được tải lại vào bộ nhớ ở một vị trí hoàn toàn mới sau khi bị trao đổi ra đĩa .
- `Bảo vệ (Protection)`: Mọi tham chiếu bộ nhớ của một tiến trình phải được kiểm tra lúc chạy để đảm bảo không tham chiếu trái phép vào vùng nhớ của tiến trình khác . Phần cứng (VXL) thường đảm nhiệm việc kiểm tra này .
- `Chia sẻ (Sharing)`: Phải cho phép các tiến trình cộng tác truy cập tới các vùng nhớ được chia sẻ .
- `Cấu trúc Logic và Cấu trúc Vật lý`: Bộ nhớ được cấu trúc tuyến tính (các byte), trong khi chương trình được tổ chức thành các mô-đun logic . HDH phải quản lý việc chuyển đổi thông tin giữa bộ nhớ chính (nhanh, chi phí cao) và bộ nhớ phụ (dung lượng lớn) .

# III. Các ký thuật cấp phát bộ nhớ
## 1. Phân chương bộ nhớ(partitioning)
- `Phân chương cố định`: Bộ nhớ được chia thành các chương có kích thước và vị trí cố định.
  - **Nhược điểm**: Số lượng tiến trình bị giới hạn , và gây ra phân mảnh trong (internal fragmentation) do tiến trình không sử dụng hết kích thước chương được cấp.
- `Phân chương động`: Kích thước, số lượng và vị trí chương có thể thay đổi. Kích thước chương được cấp bằng đúng kích thước tiến trình cần.
  - **Ưu điểm:** Tránh phân mành trong
  - **Nhược điểm:** Gây ra phân mảnh ngoài
- `Phương pháp kề cận`: Các chương và khối trống có kích thước là lũy thừa của 2 ^ k. Khi cần cấp, khối nhớ lớn được chia đôi liên tục cho đến khi tìm được vùng phù hợp. Hai khối trống cùng kích thước và kề nhau có thể được ghép lại
- `Trao đổi(swapping)`: Các tiến trình đang thực hiện có thể bị tải tạm thời ra đĩa để nhường chỗ cho tiến trình khác và sau đó được tải vào lại.

## 2. Phân trang bộ nhớ(paging)
- `Khái niệm`: Bộ nhớ vật lý được chia thành các khối cố định gọi là **khung trang(page frame)**, và không gian địa chỉ logic của tiến trình được chia thành các **trang(page)** có kích thước băng khung. Các trang của 1 tiến trình có thể nằm rải rác trong bộ nhớ.
- `Ánh xạ địa chỉ`: Địa chỉ logic (gồm số trang p và độ dịch o) được chuyển đổi thành địa chỉ vật lý bằng cách thay p bằng k (số khung) , . Phân trang loại trừ phân mảnh ngoài nhưng vẫn có phân mảnh trong (trung bình bằng nửa trang)