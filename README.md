# 상품 주문 프로젝트
## 실행방법
`build/libs/homework-0.0.1-SNAPSHOT.jar` 를 아래 명령어로 실행합니다.
`java -jar -Dspring.profiles.active=prd homework-0.0.1-SNAPSHOT.jar`

## 업무 흐름도
![](https://i.imgur.com/2cTXoT7.png)

1. 장바구니 생성

    - 주문이 시작되면 빈 장바구니를 생성한다.

2. 장바구니에 상품을 담음

    - 상품번호, 수량을 입력하면 장바구니에 상품을 담는다.

3. 주문 생성
    - 주문 완료를 입력하면 장바구니를 가지고 주문을 생성한다.
    - 주문 생성 전 상품의 재고수량을 검증하여 재고가 부족하면 SoldOutException을 발생시키고 주문을 종료한다.
    - 정상 재고인 경우 주문을 생성하고, 재고를 차감한 후 종료한다.

## 요구사항

기존 요구사항 이외의 부가적인 요구사항을 추가

-   상품번호는 숫자만 올 수 있습니다.
-   입력이 잘못 되었을 경우 다시 입력받습니다.
-   장바구니에 담긴 상품이 없을 경우 주문이 불가능합니다.

## Entity
![](https://i.imgur.com/qzXk17D.png)

## 테이블
![](https://i.imgur.com/uh9VEJ7.png)

## 프로젝트 구조
![](https://i.imgur.com/OX6JfaF.png)

-   Presentation
    -   CommandLineInterface
        -   사용자 입출력을 담당하는 커맨드라인 인터페이스
-   Domain
    -   Service, ServiceImpl
        -   Store와 Reader를 호출하여 비즈니스 로직을 구현한 레이어
        -   Presentation 레이어에 의해 호출됨
        -   Store, Reader
            -   CRUD 기능을 담당하는 레이어로 Service에 의해 호출됨
            -   Store는 CUD를, Reader는 Read를 담당
            -   Store와 Reader는 서로를 호출하지 않음
        -   Entity, Info
        -   Info는 Entity를 Presentation 레이어로 전달하기 위한 DTO 객체
-   Infrastructure
    -   StoreImpl, ReaderImpl
        -   Store, Reader 구현체로 JPA Repository를 직접 호출
        -   런타임에 Store, Reader에 주입됨
    -   JPA Repository
        -   H2 디비와 연결하는 JPA Repository
-   Common
    -   공통 클래스
        -   현재는 직접 정의한 Exception만 존재

## 사용 프레임워크 및 라이브러리
1. Spring Boot 3.1
2. Spring Data JPA
3. Lombok
4. H2 데이터베이스
