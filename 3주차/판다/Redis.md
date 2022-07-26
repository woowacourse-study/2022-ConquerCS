## 레디스 (Remote Dictionary Server)
- RAM을 사용하는 key-value 구조의 오픈소스 비관계형 DB 관리 시스템
- RAM에 데이터를 저장해서 스캐닝 속도가 빠르다.
- 캐싱이 가능해서 실시간 통신이나 클러스터링에 적합

- SNAPSHOT : 특정 시점의 데이터를 디스크에 백업
- AOF (Append Only File) : 쿼리들을 저장해두고, 서버 셧다운시 재실행 할 수 있도록 한다. 

### value가 될 수 있는 값
- 512MB 까지의 String
- String의 Set
- Sorted Set
- Hash
- List
