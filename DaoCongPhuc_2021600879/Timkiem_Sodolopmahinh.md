```mermaid

classDiagram
    class User {
        +String userId
        +List searchHistory
        +search()
        +filterResults()
        +viewSearchHistory()
    }

    class SearchLog {
        +String searchId
        +String userId
        +String searchTerm
        +String date
        +saveSearchLog()
        +retrieveSearchLogs()
    }

    class Product {
        +String productId
        +String name
        +String description
        +float price
        +float rating
        +searchProduct()
        +filterProductByCategory()
        +filterProductByShowroom()
    }

    class Blog {
        +String blogId
        +String title
        +String content
        +String author
        +String datePosted
        +searchBlog()
        +filterBlogByCategory()
    }

    class Category {
        +String categoryId
        +String categoryName
        +getCategories()
    }

    class Showroom {
        +String showroomId
        +String showroomName
        +getShowrooms()
        +filterByShowroom()
    }

    User "1" -- "0..*" SearchLog : saves
    User "1" -- "0..*" Product : searches
    User "1" -- "0..*" Blog : searches
    Product "1" -- "0..*" Category : belongs to
    Blog "1" -- "0..*" Category : belongs to
    Product "1" -- "0..*" Showroom : available in
    Blog "1" -- "0..*" Showroom : related to
