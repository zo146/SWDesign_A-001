```usecaseDiagram
    actor 교수
    actor 학생

    package "학사관리 시스템" {
        usecase "교수 등록" as UC1
        usecase "교수 인증" as UC2
        usecase "과목 등록" as UC3
        usecase "과목 조회" as UC4
        usecase "과목 점수 입력" as UC5
       
        usecase "학생 등록" as UC6
        usecase "학생 인증" as UC7
        usecase "학생 조회" as UC8
        usecase "수강 신청" as UC9
        usecase "학점 조회" as UC10
    }

    교수 --> UC1
    교수 --> UC2
    교수 --> UC3
    교수 --> UC4
    교수 --> UC5

    UC5 ..> UC2 : <<include>>
    UC5 ..> UC4 : <<include>>
    UC5 ..> UC8 : <<include>>

    학생 --> UC6
    학생 --> UC7
    학생 --> UC8
    학생 --> UC9
    학생 --> UC10

    UC9 ..> UC7 : <<include>>
    UC10 ..> UC7 : <<include>>