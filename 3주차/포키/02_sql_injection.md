# SQL Injection

조작한 SQL 쿼리를 DB에 주입해서 비정상적 명령을 실행하는 공격

 

## 공격

### 인증 우회

- 로그인 input 창에 쿼리를 같이 입력
- 항상 참이 되는 or문을 추가한다거나, #을 추가해서 뒤의 조건절이 주석처리 되도록 해버린다거나..

### 데이터 노출

- 에러메세지를 역이용
- GET 방식 API를 의도적으로 에러 나도록 호출 →DB구조 유추해서 해킹에 활용

 

## 방어

- input값의 특수문자 검사
- SQL 서버 오류 메세지 감추기
- prepareStatement 사용 → 특수문자 자동으로 escape 처리


