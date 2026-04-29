```mermaid
classDiagram
    %% Boundary Class
    class BankUI {
        <<Boundary>>
        +displayMenu() void
        +getUserInput() String
        +showResult(message: String) void
    }

    %% User Entity Class
    class User {
        -id: String
        -pw: String
        -name: String
        -phone: String
        -address: String
        +registerUser(id: String, pw: String, name: String, phone: String, address: String) boolean
        +updateUser(pw: String, name: String, phone: String, address: String) boolean
        +deleteUser(id: String) boolean
        +searchUser(id: String) User
    }

    %% Account Entity Class
    class Account {
        -number: String
        -balance: long
        +withdraw(id: String, amount: long) boolean
	+deposit(id: String, amount: long) boolean
        +transfer(id: String, targetAccountNumber: String, amount: long) boolean
        +computeBalance() long
    }

    %% Relationships
    %% BankUI가 Account를 사용하여 업무를 처리하는 의존관계
    BankUI ..> Account : <<use>>

    %% 1명의 사용자가 1개 이상의 계좌를 가지는 연관관계 (다중성 1 : 1..*)
    %% Account에서 User로의 조회를 위한 방향성 설정
    User "1" <-- "1..*" Account : 사용자 조회(searchUser)