```mermaid

classDiagram
    BlogController --> BlogService
    BlogService --> BlogValidator
    BlogService --> Blog
    BlogService --> Database

    class BlogController {
        +viewAllBlogs(): Blog[]
        +addBlog(title: string, content: string): Blog
        +updateBlog(id: int, title: string, content: string): Blog
        +deleteBlog(id: int): void
    }

    class BlogService {
        +validateBlogData(blog: Blog): boolean
        +saveBlog(blog: Blog): void
        +editBlog(id: int, blog: Blog): Blog
        +removeBlog(id: int): void
    }

    class BlogValidator {
        +validate(blog: Blog): boolean
    }

    class Blog {
        +id: int
        +title: string
        +content: string
        +createdAt: Date
    }

    class Database {
        +insertBlog(blog: Blog): void
        +updateBlog(id: int, blog: Blog): void
        +deleteBlog(id: int): void
        +fetchAllBlogs(): Blog[]
        +fetchBlogById(id: int): Blog
    }
