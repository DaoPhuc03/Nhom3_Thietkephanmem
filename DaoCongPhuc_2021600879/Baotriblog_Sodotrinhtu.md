```mermaid

sequenceDiagram
    actor A as Admin
    participant UI as Giao diện
    participant C as Controller
    participant V as Validator
    participant DB as Database

    Note over A,DB: Xem danh sách blog
    A->>UI: Click menu "BLOG"
    UI->>C: Yêu cầu danh sách blog
    C->>DB: SELECT id, title, cont_, createdAt FROM Blog
    DB-->>C: Trả về danh sách
    C-->>UI: Hiển thị danh sách blog

    Note over A,DB: Thêm blog mới
    A->>UI: Click "Thêm mới"
    UI-->>A: Hiển thị form thêm blog
    A->>UI: Nhập title, cont_, l_ & Click "Thêm mới"
    UI->>C: Gửi dữ liệu blog mới
    C->>V: Validate dữ liệu
    
    alt Dữ liệu hợp lệ
        V-->>C: Xác nhận hợp lệ
        C->>DB: INSERT INTO Blog (title, cont_, l_, createdAt)
        DB-->>C: Xác nhận thêm
        C->>DB: SELECT * FROM Blog
        DB-->>C: Trả về danh sách mới
        C-->>UI: Cập nhật danh sách
    else Dữ liệu không hợp lệ
        V-->>C: Báo lỗi
        C-->>UI: Thông báo lỗi
        UI-->>A: Hiển thị thông báo
    end

    Note over A,DB: Sửa blog
    A->>UI: Click "Sửa"
    UI->>C: Yêu cầu thông tin blog
    C->>DB: SELECT * FROM Blog WHERE id = ?
    DB-->>C: Trả về blog (id, title, cont_, l_, createdAt)
    C-->>UI: Hiển thị form sửa
    A->>UI: Sửa thông tin & Click "Cập nhật"
    UI->>C: Gửi dữ liệu đã sửa
    C->>V: Validate dữ liệu

    alt Dữ liệu hợp lệ
        V-->>C: Xác nhận hợp lệ
        C->>DB: UPDATE Blog SET title=?, cont_=?, l_=? WHERE id=?
        DB-->>C: Xác nhận cập nhật
        C->>DB: SELECT * FROM Blog
        DB-->>C: Trả về danh sách mới
        C-->>UI: Cập nhật danh sách
    else Dữ liệu không hợp lệ
        V-->>C: Báo lỗi
        C-->>UI: Thông báo lỗi
        UI-->>A: Hiển thị thông báo
    end

    Note over A,DB: Xóa blog
    A->>UI: Click "Xóa"
    UI-->>A: Hiển thị xác nhận xóa
    A->>UI: Xác nhận xóa
    UI->>C: Yêu cầu xóa blog
    C->>DB: DELETE FROM Blog WHERE id = ?
    DB-->>C: Xác nhận xóa
    C->>DB: SELECT * FROM Blog
    DB-->>C: Trả về danh sách mới
    C-->>UI: Cập nhật danh sách
