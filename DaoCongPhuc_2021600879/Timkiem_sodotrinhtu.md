sequenceDiagram
    actor U as User
    participant UI as Giao diện
    participant C as Controller
    participant DB as Database

    U->>UI: Nhập từ khóa tìm kiếm
    UI->>C: Gửi yêu cầu tìm kiếm
    
    par Lưu lịch sử
        C->>DB: INSERT SearchLog (searchTerm, date)
    and Tìm sản phẩm
        C->>DB: SELECT id, name, description, price, rating FROM Product
        alt Có category
            C->>DB: JOIN Product với Category
        end
        DB-->>C: Kết quả sản phẩm
    and Tìm blog
        C->>DB: SELECT id, title, cont_, createdAt FROM Blog
        DB-->>C: Kết quả blog
    and Tìm video
        C->>DB: SELECT id, title, desc_, url FROM Video
        DB-->>C: Kết quả video
    end

    C-->>UI: Tổng hợp kết quả

    alt Lọc theo danh mục
        U->>UI: Chọn Category
        UI->>C: Gửi category_id
        C->>DB: SELECT * FROM Category WHERE id = ?
        C->>DB: Query lại với category_id
        DB-->>C: Kết quả đã lọc
        C-->>UI: Cập nhật kết quả
    end

    alt Lọc theo Showroom
        U->>UI: Chọn Showroom
        UI->>C: Gửi showroom_id
        C->>DB: SELECT * FROM Product p JOIN Showroom s ON p.id = s.id
        DB-->>C: Kết quả đã lọc
        C-->>UI: Cập nhật kết quả
    end

    UI-->>U: Hiển thị kết quả tìm kiếm

    alt Không có kết quả
        C-->>UI: Thông báo không có kết quả
        UI-->>U: Hiển thị thông báo
    end