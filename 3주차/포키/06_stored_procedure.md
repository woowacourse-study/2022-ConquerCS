# 저장 프로시저(Stored PROCEDURE)

SQL로 작업을 하다 보면, 하나의 원하는 결과를 위해 여러 쿼리문을 사용해야 할 때가 있다

- 한 번의 요청으로 실행할 수 없을까?
- 동일한 로직의 쿼리문을 argument만 바꾸어 사용할 수는 없을까?
- → 프로시저

### 프로시저의 생성

```
CREATE OR REPLACE PROCEDURE 프로시저명(param1 IN 데이터타입, param2 OUT 데이터타입) -- 인자 값은 필수 아님
IS
[
변수명1 데이터타입;
변수명2 데이터타입;
..
]
BEGIN
 필요한 기능; -- 인자값 활용 가능
END;

EXEC 프로시저명(arg1, arg2); -- 호출
```

IN 예시

```
CREATE OR REPLACE PROCEDURE test( name IN VARCHAR2 )
IS
    msg VARCHAR2(5) := '내 이름은';
BEGIN
    dbms_output.put_line(msg||' '||name);
END;

EXEC test('규글');
```

- name 값을 받음
- msg라는 프로시저 내 변수에 값 할당 (`:=`)
- msg와 name을 공백과 결합해서 출력(`||`)
- name에 값 넣어 호출

OUT 예시

```
CREATE OR REPLACE PROCEDURE test( name OUT VARCHAR2 )
IS
BEGIN
    name := 'Gyoogle'
END;

DECLARE
out_name VARCHAR2(100);

BEGIN
test(out_name);
dbms_output.put_line('내 이름은 '||out_name);
END;
```

- name 값을 return할 것
- name에 값 대입
- out_name이라는 변수 선언 후, test 호출하여 반환값을 out_name에 저장

### 장점

- 최적화 & 캐시
  - 프로시저 최초 실행 시 최적화 상태로 컴파일 + 캐시에 저장
  - 여러번 재사용할 시 컴파일 필요없이 캐시에서 가져와서 사용
- 유지 보수
  - 작업 변경 시 프로시저 내부에서 수정만 하면 됨
- 트래픽 감소
  - 클라이언트가 직접 SQL 작성하지 않고 프로시저에 argument만 담아 호출하면 됨
  - SQL이 서버에 이미 저장된 채로 실행 → 네트워크 트래픽 감소
- 보안
  - 프로시저 내에서 참조하는 테이블에 대해 접근을 막을 수 있음

### 단점

- 호환성
  - SQL/PSM 표준과 호환성 낮아, 코드 재사용성 나쁨
- 성능
  - 문자, 숫자 연산에서 성능이 느린 편
- 디버깅
  - 에러 발생 시 원인 찾기 힘들 수 있음

 
