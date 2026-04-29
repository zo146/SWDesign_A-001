```mermaid
graph LR
    %% Actor 설정
    Admin((관리자/사용자))

    subgraph "독서 대여 시스템"
        UC1([사용자 등록])
        UC2([사용자 수정])
        UC3([사용자 삭제])
        UC4([사용자 id 조회])
        UC5([도서 등록])
        UC6([도서 수정])
        UC7([도서 삭제])
        UC8([도서 id 조회])
        UC9([대여상태 확인])
        UC10([대여])
        UC11([반납])
        UC12([연체 확인])
    end

    %% 기본 연결
    Admin --> UC1
    Admin --> UC2
    Admin --> UC3
    Admin --> UC4
    Admin --> UC5
    Admin --> UC6
    Admin --> UC7
    Admin --> UC8
    Admin --> UC9
    Admin --> UC10
    Admin --> UC11

    %% 포함 관계 (Include) - 점선으로 표현
    UC10 -.->|include| UC4
    UC10 -.->|include| UC8
    UC10 -.->|include| UC9

    UC11 -.->|include| UC4
    UC11 -.->|include| UC8
    UC11 -.->|include| UC12

    %% 스타일링
    style Admin fill:#f9f,stroke:#333,stroke-width:2px



Class다이어그램

classDiagram
    class User {
        + userID: String
        + password: String
        + name: String
    }

    class Book {
        + bookID: String
        + title: String
        + publisher: String
        + rentalStatus: boolean
    }

    class RentalInfo {
        + rentID: String
        + userID: String
        + bookID: String
        + rentDate: int
        + dueDate: int
        + returnDate: int
    }

    class LibrarySystem {
        + addUser(userID: String) boolean
        + updateUser(userID: String) boolean
        + deleteUser(userID: String) boolean
        + searchUserID(userID: String) boolean
        + addBook(bookID: String) boolean
        + updateBook(bookID: String) boolean
        + deleteBook(bookID: String) boolean
        + searchBookID(bookID: String) boolean
        + checkRentalStatus(bookID: String) boolean
        + rentBook(userID: String, bookID: String) boolean
        + returnBook(userID: String, bookID: String) boolean
        + checkOverdue(rentID: String) boolean
    }

    %% 수정된 관계 설정
    LibrarySystem "1" o-- "*" User : 사용자 관리
    LibrarySystem "1" o-- "*" Book : 도서 관리
    LibrarySystem "1" o-- "*" RentalInfo : 대여 기록 관리
    
    %% 엔티티 간의 관계는 데이터 참조이므로 일반 연관 유지
    User "1" -- "0..*" RentalInfo : 도서 대여
    Book "1" -- "0..*" RentalInfo : 대여 정보 포함