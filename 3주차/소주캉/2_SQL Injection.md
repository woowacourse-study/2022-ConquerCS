# SQL Injection
#### 그게 뭐야?
- 해킹의 목적으로 유저의 입력 값에 기대하지 않는 sql 쿼리문을 동작시키도록 주입하는 공격

## 공격 방법
### 인증 우회
- 입력값과 동시에 다른 쿼리문을 입력하여 조작하는 방법
- '1' = '1' 등 `true`인 조건을 삽입하고 다음에 원하는 쿼리를 삽입하는 등의 방법이 있다. 

### 데이터 노출
- 시스템에서 발생하는 SQL 관련 에러를 유발하여 데이터 베이스 구조를 유추하여 해킹에 활용한다.

## 방어 방법
### 인풋값 검증
- SQL에서 문법으로 기능할 수 있는 문장 부호(`"`, `'`, `;` 등)이 포함된 인풋 값을 검증한다. 
### SQL 관련 에러 감추기
- Presentation 계층에서 접근할 때 발생하는 예외에 데이터 베이스 관련 정보를 노출하지 않게 한다. 
- Global Exception Handling 용도의 500 Internal Error 등이 있다.

### PreparedStatement 사용하기
- PreparedStatement를 사용하면 (`'`, `"`, `\`)등의 SQL 관련 문법으로 기능할 수 있는 문자들에 Escape sequence를 추가로 붙여 문법요소로 기능하지 않게 한다. 

# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/SQL%20Injection.html)
[wikipedic.org](https://en.wikipedia.org/wiki/SQL_injection)
[Real MySQL](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=2909101309302)