```mermaid

classDiagram
    SearchController --> SearchService
    SearchService --> SearchLog
    SearchService --> Product
    SearchService --> Blog
    SearchService --> Category
    SearchService --> Showroom

    class SearchController {
        +search(term: string): SearchResult[]
    }

    class SearchService {
        +logSearch(term: string): void
        +searchProducts(term: string): Product[]
        +searchBlogs(term: string): Blog[]
    }

    class Product {
        +id: int
        +name: string
        +description: string
        +price: double
        +rating: double
        +category_id: int
        +showroom_id: int
    }

    class Blog {
        +id: int
        +title: string
        +content: string
        +createdAt: Date
    }

    class Category {
        +id: int
        +name: string
        +description: string
    }

    class Showroom {
        +id: int
        +name: string
        +address: string
    }

    class SearchLog {
        +id: int
        +searchTerm: string
        +date: Date
    }

    class SearchResult {
        +products: Product[]
        +blogs: Blog[]
    }
