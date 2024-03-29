# **SQL (관계형 DB)**

이론적으로는 **함수 종속(Functional Dependency)에 의해 정규화(Normalization)된 모델**이라고 정의할 수 있다. 결과적으로는 테이블 형태의 저장 구조를 가지며 데이터 사이의 관계를 테이블의 키와 열을 통해 표현하는 저장 방식이다

## 기본 개념

- 데이터는 **정해진 데이터 스키마에 따라 테이블에 저장**된다.
- 데이터는 **관계를 통해 여러 테이블에 분산**된다.

데이터는 테이블에 레코드로 저장되는데, 각 테이블마다 명확하게 정의된 구조가 있다. 해당 구조는 필드의 이름과 데이터 유형으로 정의된다.

따라서 **스키마를 준수하지 않은 레코드는 테이블에 추가할 수 없다.** 즉, 스키마를 수정하지 않는 이상은 정해진 구조에 맞는 레코드만 추가가 가능한 것이 관계형 데이터베이스의 특징 중 하나다.

또한, 데이터의 중복을 피하기 위해 '관계'를 이용한다.

![https://t1.daumcdn.net/cfile/tistory/994D09355C937ECD2D](https://t1.daumcdn.net/cfile/tistory/994D09355C937ECD2D)

하나의 테이블에서 중복 없이 하나의 데이터만을 관리하기 때문에 다른 테이블에서 부정확한 데이터를 다룰 위험이 없어지는 장점이 있다.

## **특징**

### **ACID 속성**

관계형 모델은 ACID라고 불리는 4가지 속성을 만족하는 특징을 가지고 있다

- **Atomicity (원자성)**Transaction은 완벽하게 실행하거나, 전혀 실행되지 않는다
- **Consistency (일관성)**Transaction이 커밋되면, 데이터는 DB 스키마를 준수해야한다
- **Isolation (격리성)**동시에 일어나는 Transaction들은 각각 별도로 실행되어야 한다
- **Durability (내구성)**시스템 장애 시 마지막으로 알려진 상태로 복구할 수 있어야 한다

### **확장**

하드웨어의 계산 성능을 개성시키거나 읽기 전용 워크 로드의 복제물을 추가하여 확장한다

### **데이터의 이용**

데이터를 저장 및 검색하기 위해 SQL을 준수하는 쿼리를 이용하여 요청한다

## **한계**

관계형 데이터베이스의 핵심은 **데이터를 중복해서 저장하지 않도록 설계하는 것**이다

- **데이터 구조를 효율적으로 설계하기 어렵다**는 단점이 생긴다
- 일관성을 보장하는 관계형 모델의 특징에 의해 **수평적인 확장이 어렵다**
- 스키마에 의해 미리 정의된 데이터 타입과 일치하는 구조화된 데이터만 관리할 수 있어 **비정형 데이터**에 대한 관리가 어렵다

# **NoSQL (비관계형 DB)**

특정 데이터 모델에 대해 특정 목적에 맞추어 구축되는 DB로서, 현대적인 애플리케이션 구축을 위한 **유연한 스키마**를 갖추고 있다

NoSQL은 **대량의 분산 데이터**를 저장/조회하는 데에 특화되어 있으며, **개발의 용이성**, **기능성** 및 **확장성**을 인정받고 있다

## SQL 과의 차이점

- SQL은 정해진 스키마를 따르지 않으면 데이터 추가가 불가능했다. 하지만 NoSQL에서는 다른 구조의 데이터를 같은 컬렉션에 추가가 가능하다.
- 문서(documents)는 Json과 비슷한 형태로 가지고 있다. 관계형 데이터베이스처럼 여러 테이블에 나누어담지 않고, 관련 데이터를 동일한 '컬렉션'에 넣는다.
    - 따라서 여러 테이블에 조인할 필요없이 이미 필요한 모든 것을 갖춘 문서를 작성하는 것이 NoSQL이다. (NoSQL에는 조인이라는 개념이 존재하지 않음)
        - 조인하고 싶을 때는?

          ⇒ 컬렉션을 통해 데이터를 복제하여 각 컬렉션 일부분에 속하는 데이터를 정확하게 산출하도록 한다.

- 데이터가 중복되어 서로 영향을 줄 위험이 있다. 따라서 조인을 잘 사용하지 않고 자주 변경되지 않는 데이터일 때 NoSQL을 쓰면 상당히 효율적이다.

## 특징

- 성능과 규모 확장에 최적화된 다양한 데이터 모델 제공
- ACID 속성을 완화여 수평적인 확장 보장
- 분산형 아키텍쳐를 사용하여 액세스 분할성 존재
- 객체 기반 API를 통해 데이터를 쉽게 저장 및 검색

### 확장성

**변화무쌍**한 작업 부하에 대한 **요구 사항을 효율적으로 충족시키는 능력**

필요에 따라 서버를 추가하는 scale-out 작업이 이루어진다.

**RDBMS**에서는 단일 데이터베이스 시스템을 구동하는 여러 서버를 관리하기위해 데이터베이스 소프트웨어가 필요하여 복잡성과 운영 비용이 증가할 수 있다. 그러나, **NoSQL**은 **클러스터 하나에서 서버 여러개를 이용하도록 설계되었다.** 즉, 새로운 서버를 추가/제거할 때 NoSQL DBMS는 사용 가능한 새 서버를 사용하도록 조정한다.

### 비용

주요 **NoSQL** 데이터베이스들은 **오픈 소스** 형태로 제공되며 대부분 오픈 소스 개발자는 자신의 소프트웨어를 사용하는데 비용을 매기지 않는다.

### 유연성

**RDBMS**는 관계형 데이터 모델을 사용해 해결 가능한 문제의 범위 "내에서는" 유연한 편이다. 하지만 데이터베이스 설계자는 프로젝트를 시작할 때 애플리케이션 지원에 필요한 **모든 테이블과 컬럼을 파악**해야 할 뿐만 아니라 대부분의 테이블에 값이 채워져있어야 한다.

**NoSQL** 데이터베이스는 고정된 테이블 구조가 필요하지 않다. 즉, 데이터베이스 설계를 변경하지 않고도 필요한 새로운 속성을 **동적으로 추가**할 수 있다.

### 가용성

**NoSQL** 데이터베이스는 저렴한 비용으로 서버를 여러개 이용할 수 있도록 설계되었다

서버 하나가 중지되거나 서비스를 일시 중지해야할 경우 클러스터 내 다른 서버가 작업량 전체를 떠맡을 수 있다

# NoSQL vs RDBMS

## **확장 개념**

두 데이터베이스를 비교할 때 중요한 Scaling 개념도 존재한다.

데이터베이스 서버의 확장성은 '수직적' 확장과 '수평적' 확장으로 나누어진다.

- 수직적 확장 : 단순히 데이터베이스 서버의 성능을 향상시키는 것 (ex. CPU 업그레이드)

  ⇒ RDBMS!

- 수평적 확장 : 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미 (하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동)

  ⇒ NoSQL!


## RDBMS

### **장점**

- 하나의 테이블에서 중복 없이 하나의 데이터만을 관리하므로, 다른 테이블에서 부정확한 데이터를 다룰 위험이 없어짐
- 명확하게 정의된 스키마, 데이터 무결성 보장
- 관계는 각 데이터를 중복없이 한번만 저장

### **단점**

- 덜 유연함. 데이터 스키마를 사전에 계획하고 알려야 함. (나중에 수정하기 힘듬)
- 관계를 맺고 있어서 조인문이 많은 복잡한 쿼리가 만들어질 수 있음
- 대체로 수직적 확장만 가능함

## **NoSQL**

### **장점**

- 스키마가 없어서 유연함. 언제든지 저장된 데이터를 조정하고 새로운 필드 추가 가능
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장됨. 데이터 읽어오는 속도 빨라짐
- 수직 및 수평 확장이 가능해서 애플리케이션이 발생시키는 모든 읽기/쓰기 요청 처리 가능

### **단점**

- 유연성으로 인해 데이터 구조 결정을 미루게 될 수 있음
- 데이터 중복을 계속 업데이트 해야 함
- 데이터가 여러 컬렉션에 중복되어 있기 때문에 수정 시 모든 컬렉션에서 수행해야 함 (SQL에서는 중복 데이터가 없으므로 한번만 수행이 가능)

## 어떤 DBMS를 선택할까

### RDBMS **데이터베이스 사용이 더 좋을 때**

- 데이터 구조가 명확하며 변경 될 여지가 없으며 명확한 스키마가 중요한 경우
- 중복된 데이터가 없어(데이터 무결성) 변경이 용이하기 때문에 관계를 맺고 있는 데이터가 자주 변경이 이루어지는 시스템
- 관계를 맺고 있는 데이터가 자주 변경되는 애플리케이션의 경우

  ⇒ NoSQL에서는 여러 컬렉션을 모두 수정해야하므로 비효율적이다.

- 변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우

### **NoSQL 데이터베이스 사용이 더 좋을 때**

- 정확한 데이터 구조를 알 수 없고 데이터가 변경/확장이 될 수 있는 경우
- Update가 많이 이루어지지 않고, 조인을 잘 사용하지 않는 시스템
- 읽기를 자주 하지만, 데이터 변경은 자주 없는 경우
- 데이터베이스를 수평으로 확장해야 하는 경우 (막대한 양의 데이터를 다뤄야 하는 경우)
    - 막대한 데이터를 저장해야 해서 Database를 Scale-Out를 해야 되는 시스템
- 정확한 데이터 구조를 알 수 없거나 변경/확장 될 수 있는 경우

하지만 위의 내용들은 하나의 제시 방법이지 완전한 정답이 정해져 있는 것은 아니다. SQL을 선택해서 복잡한 JOIN문을 만들지 않도록 설계하여 단점을 없앨 수도 있고 NoSQL을 선택해서 중복 데이터를 줄이는 방법으로 설계해서 단점을 없앨 수도 있다.

# 예시 - **영화 추천 서비스 개발**

> 영화 시상식에서 노미네이트 된 영화를 기반으로 **영화 추천 서비스**를 만들고 있으며 API를 통해 TMDB ID, 제목, 년도, 포스터와 같은 기본적인 영화 정보를 검색해야 하기 때문에 해당 정보를 저장할 **영화 DB**가 필요합니다. 또한 카테고리, 노미네이트, 수상작들과 같은 정보가 담긴 **시상 DB**가 필요할 것 같습니다. 지금까지는 간단하게 SQLite를 사용하고 있었으나 본 영화 목록, 보고 싶은 목록들의 기능을 넣어서 버전 2.0 개발할 예정인데 **과연 NoSQL이 적합할지 궁금합니다**!
>

위와 같은 서비스를 개발하고자 한다면 SQLite와 NoSQL DBMS 중 어떤 것을 선택해야할까?

> 만약 서비스 구성하는데 **비관계형 데이터베이스를 써야 하는 이유를 정확하게 알지 못하면 관계형 데이터베이스를 사용하는 것을 일단 추천합니다**. 그리고 기존에 하나인 데이터베이스에서 **영화 데이터와 시상 데이터를 찢어서 사용한다는 것은 이미 두 테이블 간 관계가 있는 것**으로 보입니다. 만약에 관계형 데이터 형태인데 무리하게 NoSQL를 사용하려고 하면 분명히 나중에 후회를 할 것입니다.
>

> 만약에 특정 데이터, 예를 들어 보고 싶은 목록 리스트를 **문서 형태로 만든다면 PostgreSQL의 JSON형태로 저장하는 기능 활용하여 관계형과 비 관계형을 함께 효율적으로 사용**할 수 있을 것 같네요.
>

결론적으로, **굳이 NoSQL을 사용해야할 이유가 명확하지 않다면, 관계형 데이터베이스를 사용하는 것이 더 안전**하다. 특히, 데이터 간 관계가 확실한 경우에는 오히려 더 비효율적인 결과를 일으킬 수도 있다

개발하고자 하는 서비스의 데이터 모델을 선택할 때 답해보아야하는 질문은 아래와 같이 정리해볼 수 있다

1. **어떤 데이터를 다루는가?**

   서비스에서 주로 사용하는 데이터의 구조, 관계, 그리고 사용 방법에 대해서 정확하게 정의해야한다

2. **주요 서비스가 무엇인가?**

   같은 도메인 내에서도 어떤 서비스를 제공하는 지에 따라 DB 관리 방향이 완전히 달라질 수 있다주요 기능을 정리하고, 해당 기능을 구조적으로 가장 잘 지원하는 모델을 선택해야 한다