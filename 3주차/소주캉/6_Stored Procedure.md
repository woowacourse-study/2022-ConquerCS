# Stored Procedure
#### 그게 뭔데?
- 여러 쿼리를 하나의 그룹으로 묶어서 하나의 단위를 독립적으로 실행하는 과정이다.

### 장점은?
#### 절차적 기능을 구현
- SQL은 조건문이나 반복문같은 제어 문장을 사용할 수 없으나 Stored Procedure는 DBMS 서버에서 절차적인 기능을 실행할 수 있는 제어 기능을 제공한다. 
#### DB 보안 향상
- Stored Program은 자체 보안 설정 기능을 가지고 있으며, Program 단위로 실행 권한을 부여할 수 있다. 이런 보안 기능을 조합해서 특정 테이블의 읽기와 쓰기 또는 특정 column 에만 권한을 설정하는 등 세밀한 권한 제어가 가능하다.
#### 기능 추상화
- 어플리케이션 단의 로직과 Stored Procedure를 분리하여 DB에 책임을 분산하고 어플리케이션은 Procedure가 제공하는 더 추상화된 결과물에 의존하게 할 수 있다. 
#### 최적화 & 캐시
- Procedure 최초 실행시 최적화 상태로 컴파일 되어 cache에 저장된다. 이 후 여러 번 사용될 때 미리 컴파일된 결과를 cache에서 가져와서 쓸 수 있다. 

### 단점은?
#### 낮은 처리 성능
- Stored Procedure는 DB Engine에서 해석되고 실행된다. DB Engine은 절차적 처리를 주목적으로 하지 않아 다른 프로그래밍 언어에 비해 문자, 숫자 연산 성능이 좋지 않다. C/C++, Java에 비해 수십배 느리다.

#### 호환성 감소
- 구문 규칙이 표준화되어있지 않고 각 Vendor마다 차이가 있기 때문에 추상화가 어려워 재사용이 어렵다.

#### 디버킹 어려움
- 에러가 발생했을 때, 어플리케이션 코드에 비하여 DB 내의 Procedure는 디버깅하기 어렵다. 

# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/Stored%20PROCEDURE.html)
[Real MySQL](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=2909101309302)