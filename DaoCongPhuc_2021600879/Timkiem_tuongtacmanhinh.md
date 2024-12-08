```mermaid

sequenceDiagram
    participant User
    participant SearchInterface
    participant SearchLog
    participant Product
    participant Blog
    participant Category
    participant Showroom

    User->>SearchInterface: Nhập từ khóa và nhấn tìm kiếm
    SearchInterface->>Product: Gọi search() với từ khóa
    Product-->>SearchInterface: Trả về danh sách sản phẩm
    SearchInterface->>Blog: Gọi search() với từ khóa
    Blog-->>SearchInterface: Trả về danh sách bài viết
    SearchInterface->>SearchLog: Lưu thông tin tìm kiếm (searchTerm)
    SearchLog-->>SearchInterface: Xác nhận lưu trữ
    SearchInterface->>Category: Lọc theo danh mục (nếu có)
    Category-->>SearchInterface: Trả về danh sách danh mục
    SearchInterface->>Showroom: Lọc theo showroom (nếu có)
    Showroom-->>SearchInterface: Trả về danh sách showroom
    SearchInterface->>User: Hiển thị kết quả tìm kiếm
    alt Nếu không có kết quả
        SearchInterface->>User: Thông báo "Không tìm thấy kết quả"
    end
    alt Nếu có lỗi kết nối CSDL
        SearchInterface->>User: Thông báo lỗi kết nối
    end
