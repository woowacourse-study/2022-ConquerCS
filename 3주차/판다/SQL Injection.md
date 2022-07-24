## SQL Injection
- 클라이언트의 입력값을 조작하여 서버의 DB를 공격하는 기법. 
- 취약점 공격의 일종
- 사용자가 입력한 데이터를 검증하지 않아서 발생
- DB 스키마를 몰라도 어차피 sql injection에 취약한 DB인 경우 스키마 구조 획득이 가능


## 방어 조치
- 이스케이핑
- 권한 설정
- prepared statement -> 가장 추천
- procedure -> 일종의 쿼리 함수화
- 프론트에서 입력값 검증 -> 서버에서 입력값 검증 -> prepared statement로 파라미터 바인딩 -> procedure를 통한 처리 -> 서버에서 출력값 검증 -> 프론트에 전달
