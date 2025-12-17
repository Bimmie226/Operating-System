# I. Các khái niệm liên quan đến tiến trình
- `Định nghĩa tiến trình`: Tiến trình là một chương trình đang trong quá trình thực hiện. Tiến trình là một thực thể động được cấp tài nguyên cụ thể để thực hiện lệnh, khác với chương trình(thực thể tĩnh)
- `Trạng thái tiến trình`: Tiến trình chuyển đổi qua mô hình 5 trạng thái: Mới khởi tạo, sẵn sàng(chờ CPU), Chạy(đang sử dụng CPU), chờ đợi(chờ sự kiện I/O), và kết thúc. 
- `Khối quản lý tiến trình(PCB)`: 
  - HDH lưu trữ thông tin cần thiết để quán lý mỗi tiến trình trong một cấu trúc dữ liệu gọi là PCB. 
  - PCB bao gồm: 
    - Số định danh(PID)
    - Trạng thái tiến trình
    - Nội dung các thanh ghi CPU (con trỏ lệnh, ngăn xếp)
    - Thông tin phục vụ điều độ (mức ưu tiên)
    - Thông tin bộ nhớ
    - Danh sách tài nguyên đã sử dụng

# II. Luồng thực hiện(Thread)
- `Khái niệm Luồng`: Trong HDH hiện đại, tiến trình có thể tách vai trò thực hiện lệnh ra khỏi đơn vị sở hữu tài nguyên. Một luồng thực hiện là một chuỗi lệnh được cấp phát CPU để thực hiện độc lập. Hệ thống hiện nay thường hỗ trợ đa luồng
- `Phân chia tài nguyên`: Tiến trình là đơn vị sở hữu chung tài nguyên(không gian nhớ logic, file, thiết bị I/O). Trong khi đó, mỗi luồng có ngăn xếp và khối quản lý luồng riêng để lưu trữ con trỏ lệnh và nội dung thanh ghi
- `Ưu điểm`: Đa luồng tăng hiệu năng, tăng tính đáp ứng, dễ dàng chia sẻ thông tin và tận dụng được kiến trúc đa CPU
- `Các mức luồng`:
  - **Luồng mức người dùng:** Được trình ứng dụng tạo và quản lý. Chuyển đổi nhanh vì không cần chuyển đổi sang chế độ nhân. Nhược điểm lớn là nếu một luồng bị phong tỏa, toàn bộ tiến trình bị phong tỏa
  - **Luồng mức nhân**: Được HDH tạo và quản lý. Tăng tính đáp ứng và khả năng thực hiện đồng thời.

# III. Điều độ tiến trình
- `Điều độ`: Là quá trình quyết định tiến trình/luồng nào được sử dụng CPU khi nào và trong bao lâu
- `Các dạng điều độ`: 
  - Đến trước phục vụ trước (FCFS): Đơn giản, công bằng, nhưng thời gian chờ đợi trung bình lớn
  - Điệu độ quay vòng (RR): Sử dụng lượng tử thời gian(t) và cơ chế phân phối lại để cải thiện thời gian đáp ứng
  - Ưu tiên tiến trình ngắn nhất(SPF): Chọn tiến trình có chu kỳ sử dụng CPU tiếp theo ngắn nhất 
  - Ưu tiên thời gian còn lại ngắn nhất(SRTF): Là SPF(Chọn tiến trình có chu kỳ sử dụng CPU tiếp theo ngắn nhất) có thêm cơ chế phân phối lại; khi một tiến trình mới xuất hiện, HDH so sánh thời gian còn lại
  - Điệu độ có mức ưu tiên: Tiến trình có mức ưu tiên cao hơn được cấp CPU trước

