```mermaid
classDiagram
    class 사용자정보 {
        -id: string
        -암호: string
        -성명: string
        +사용자등록(id: string, 암호: string, 성명: string) boolean
        +사용자수정(id: string, 암호: string, 성명: string) boolean
        +사용자삭제(id: string) boolean
        +사용자ID조회(id: string) boolean
    }

    class 도서정보 {
        -도서ID: string
        -도서명: string
        -출판사: string
        -대여상태: boolean
        +도서등록(도서ID: string, 도서명: string, 출판사: string) boolean
        +도서수정(도서ID: string, 도서명: string, 출판사: string) boolean
        +도서삭제(도서ID: string) boolean
        +도서ID조회(도서ID: string) boolean
        +대여상태확인(도서ID: string) boolean
    }

    class 대여정보 {
        -대여ID: string
        -id: string
        -도서ID: string
        -대여일: int
        -반납예정일: int
        -반납일: int
        +대여(id: string, 도서ID: string, 대여일: int, 반납예정일: int) string
        +반납(id: string, 도서ID: string, 반납일: int) string
        +연체확인(반납일: int, 반납예정일: int) boolean
    }

    class 도서UI {
        <<boundary>>
        +대여요청() boolean
        +반납요청() boolean
    }

    %% 연관관계 및 다중성 설정
    대여정보 "0..*" -- "1" 사용자정보 : 사용자조회
    대여정보 "1" -- "1" 도서정보 : 도서정보조회

    %% 의존관계 설정
    도서UI ..> 대여정보 : 의존
