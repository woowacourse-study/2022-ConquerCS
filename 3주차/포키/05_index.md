# Index

Table의 column을 색인화(별도의 파일로 저장)

### 

### 목적

- RDBMS에서 검색 속도 향상
  - 해당 Table의 모든 record를 scan하지 않고, 색인화된 파일을 검색하기 때문

### 과정

- Table 생성 → MYD, MYI, FRM 파일 생성
  - FRM: 테이블 구조
  - MYD: 실제 데이터
  - MYI: Index 정보
    - Index 사용 X → 비어있음
    - Indexing하는 경우 생성 → Select 쿼리로 indexing된 column 탐색 시 사용

### 단점

- DB 크기 증가
- 병행성 줄어들어서 한 페이지를 동시에 수정하기 힘들어짐
- 이미 인덱스된 field에서 data를 변경할 시 성능 저하
  - 매번 index를 재작성 해야함

 

## 어떤 Column을 Indexing할까?

### Good

- Where절에서 자주 사용될 때
- 외래키가 사용될 때
- Join에 자주 사용될 때

### Bad

- 중복도 높을 때
- DML이 자주 일어날 때

### DML이 자주 일어나면 안 좋은 이유

- Insert
  - 기존 Block에 여유가 없는 상채에서 새로운 Data가 입력된다면
  - 새로운 Block할당 받아서 Key를 옮기는 작업(index split)
  - 그 동안 해당 Block의 key값이 대해서는 DML blocking → 대기 발생
- Delete
  - Table의 Data는 지워진 공간이 비어서 그 공간을 다시 사용할 수 있지만, Index는 지워지는 것이 아니라 사용하지 않는다는 표시만 해둠
  - Table에서 보이는 data 수와 index data 수가 다를 수 있다
- Update
  - Index는 Update할 수 없어서 Delete후 새로운 Insert 작업 → 2배의 작업 소요


