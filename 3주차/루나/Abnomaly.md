## 이상이란?

이상 현상이란? 테이블내의 **데이터 중복성에 의해서 발생되는 데이터 불일치 현상**이다

좋은 관계형 데이터베이스를 설계하는 목적 중 하나가 정보의 **이상 현상(Anomaly)** 이 생기지 않도록 고려해 설계하는 것이다.

이상 현상은 **갱신 이상(Modification Anomaly), 삽입 이상(Insertion Anomaly), 삭제 이상(Deletion Anomaly)**으로 구성된다.

## **삽입 이상 (Insertion Anomaly)**

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff556388e-2e40-44b0-81a3-b6bea0919f1b%2FUntitled.png?table=block&id=445c9462-7a9e-4099-811e-27712a5e4e4c&spaceId=ae7599b2-a6a0-4ad1-9149-e9ef3a1ab56c&width=1710&userId=1283b1b0-5fc9-41f0-9b53-56b46ea4c788&cache=v2)

> 불필요한 데이터를 추가해야지, 삽입할 수 있는 상황
>

내가 원하는 값만 테이블에 삽입하고 싶은데, 테이블에 필요하지 않은 필드들 때문에 원치 않는 필드의 값도 삽입해야 하는 경우 ⇒ 기본 값을 넣거나, Null이 들어감.

## **갱신 이상 (Update Anomaly)**

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8b703b4a-dc18-47bb-91db-6143aa642367%2FUntitled.png?table=block&id=c32c19e0-7a3c-4aca-8932-1185e723593b&spaceId=ae7599b2-a6a0-4ad1-9149-e9ef3a1ab56c&width=1710&userId=1283b1b0-5fc9-41f0-9b53-56b46ea4c788&cache=v2)

> 일부만 변경하여, 데이터가 불일치 하는 모순의 문제
>

어떤 값을 업데이트 했을때 그 속성의 다른 속성값들과의 불일치가 발생하는 현상

## **삭제 이상 (Deletion Anomaly)**

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F73879c81-83bf-4150-8192-56685219c3a9%2FUntitled.png?table=block&id=4ed19ffb-21a4-4280-a907-dd9696e0778e&spaceId=ae7599b2-a6a0-4ad1-9149-e9ef3a1ab56c&width=1710&userId=1283b1b0-5fc9-41f0-9b53-56b46ea4c788&cache=v2)

> 튜플 삭제로 인해 꼭 필요한 데이터까지 함께 삭제되는 문제
>

내가 원하는 값만 테이블에서 삭제하고 싶은데, 하나의 튜플이 삭제를 원하지 않는 속성값도 갖고 있기 때문에 같이 지워져서 발생하는 문제

⇒ 위 예시에서 학번이 300번인 학생이 과목 수강을 취소하면 C-73에 대한 정보도 삭제됨