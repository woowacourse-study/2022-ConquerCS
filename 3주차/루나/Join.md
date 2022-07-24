# **조인이란?**

> 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법
>

테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 하므로 이를 이용하여 데이터 검색에 활용한다.

# 조인의 필요성

- 관계형 데이터베이스의 구조적 특징으로 정규화를 수행하면 의미 있는 데이터의 집합으로 테이블이 구성되고, 각 테이블끼리는 관계(Relationship)를 갖게 된다.
- 이와 같은 특징으로 관계형 데이터베이스는 저장 공간의 효율성과 확장성이 향상되게 된다.
- 다른 한편으로는 서로 관계있는 데이터가 여러 테이블로 나뉘어 저장되므로, 각 테이블에 저장된 데이터를 효과적으로 검색하기 위해 조인이 필요하다.

# **JOIN 종류**

<예시용 기준 테이블>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5fe76c3-8b50-4c51-b591-b988c72d0fcb/Untitled.png)

## 내부 조인 (INNER JOIN)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F99799F3E5A8148D7036659](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F99799F3E5A8148D7036659)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc3fc36d-0d7e-4116-b4ac-2c553534911f/Untitled.png)

- 가장 흔한 결합 방식이며, 기본 조인 형식으로 간주된다.
- 내부 조인은 조인 구문에 기반한 2개의 테이블(A, B)의 컬럼 값을 결합함으로써 새로운 결과 테이블을 생성한다.
- **명시적 조인 표현**(explicit)과 **암시적 조인 표현**(implicit) 2개의 다른 조인식 구문이 있다.
    - 명시적 조인 표현
        - 테이블에 조인을 하라는 것을 지정하기 위해 JOIN 키워드를 사용하며, 그리고 나서 다음의 예제와 같이 ON 키워드를 조인에 대한 구문을 지정하는데 사용한다

        ```sql
        SELECT *
        FROM employee INNER JOIN department
        ON employee.DepartmentID = department.DepartmentID;
        ```

    - 암시적 조인 표현
        - SELECT 구문의 FROM 절에서 그것들을 분리하는 컴마를 사용해서 단순히 조인을 위한 여러 테이블을 나열하기만 한다.

        ```sql
        SELECT *
        FROM employee, department
        WHERE employee.DepartmentID = department.DepartmentID;
        ```


## 외부 조인 (OUTER JOIN)

- 조인 대상 테이블에서 특정 테이블의 데이터가 모두 필요한 상황에서 외부 조인을 호라용해 효과적으로 결과 집합을 생성할 수 있다.

### 왼쪽 외부 조인 (LEFT OUTER JOIN)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F997E7F415A81490507F027](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F997E7F415A81490507F027)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b040c8de-ea0b-4efe-9405-96436ec9486f/Untitled.png)

- 우측 테이블에 조인할 컬럼의 값이 없는 경우 사용한다.
- 즉, 좌측 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다.

```sql
SELECT *
FROM employee LEFT OUTER JOIN department
ON employee.DepartmentID = department.DepartmentID;
```

### 오른쪽 내부 조인 (RIGHT OUTER JOIN)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F9984CE355A8149180ABD1D](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F9984CE355A8149180ABD1D)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/231c1423-3c7c-41b5-9852-799919d76a6a/Untitled.png)

- 좌측 테이블에 조인할 컬럼의 값이 없는 경우 사용한다.
- 즉, 우측 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다.

```sql
SELECT *
FROM employee RIGHT OUTER JOIN department
ON employee.DepartmentID = department.DepartmentID;
```

### 완전 외부 조인 (FULL OUTER JOIN)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F99195F345A8149391BE0C3](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F99195F345A8149391BE0C3)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f8c5843f-a531-46c9-9b2a-55c81c207b5c/Untitled.png)

- 양쪽 테이블 모두 OUTER JOIN이 필요할 때 사용한다.
- 사실상의 합집합을 말하며, A와 B의 모든 데이터가 검색된다.

```sql
SELECT *
FROM employee FULL OUTER JOIN department
ON employee.DepartmentID = department.DepartmentID;
```

## 교차 조인 (CROSS JOIN)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F993F4E445A8A2D281AC66B](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F993F4E445A8A2D281AC66B)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dceda54d-d954-4231-b40c-5554e647aa1f/Untitled.png)

- 조인되는 두 테이블에서 곱집합을 반환한다.
- 즉, 두 번째 테이블로부터 각 행과 첫 번째 테이블에서 각 행이 한번씩 결합된 열을 만들 것이다.
- 예를 들어 m행을 가진 테이블과 n행을 가진 테이블이 교차 조인되면 m*n 개의 행을 생성한다
- 명시적 조인 표현

  `SELECT * FROM employee CROSS JOIN department;`

- 암시적 조인 표현

  `SELECT * FROM employee, department;`


## 셀프 조인 (SELF JOIN)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F99341D335A8A363D0614E8](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F99341D335A8A363D0614E8)

- 한 테이블에서 자기 자신에 조인을 시키는 것이다.
- 하나의 테이블을 여러번 복사해서 조인하는 것과 동일하다.
- 자신이 가지고 있는 칼럼을 다양하게 변형시켜 사용할 때 자주 사용된다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A, EX_TABLE B
```

## 동**등 조인(EQUI JOIN)**

- 비교자 기반의 조인이며, 조인 구문에서 **동등비교만을 사용**한다.
- 다른 비교 연산자(<와 같은)를 사용하는 것은 동등 조인으로서의 조인의 자격을 박탈하는 것이다.

### **자연 조인(NATURAL JOIN)**

![https://github.com/WeareSoft/tech-interview/raw/master/contents/images/natural-join.png](https://github.com/WeareSoft/tech-interview/raw/master/contents/images/natural-join.png)

- 동등 조인의 한 유형으로 조인 구문이 조인된 테이블에서 동일한 컬럼명을 가진 2개의 테이블에서 모든 컬럼들을 비교함으로써, 암시적으로 일어나는 구문이다.
- 결과적으로 나온 조인된 테이블은 동일한 이름을 가진 컬럼의 각 쌍에 대한 단 하나의 컬럼만 포함하고 있다.
- SQL : `SELECT * FROM employee NATURAL JOIN department;`