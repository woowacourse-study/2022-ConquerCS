# RDB
## 특징
- 데이터는 정해진 데이터 스키마에 따라 테이블에 저장된다.
- 데이터는 관계를 통해 여러 테이블에 분산된다.

**핵심은 중복을 방지하는 것**

## 장점
- 명확하게 정의된 스키마로 데이터 무결성 보장
- Relation은 각 데이터를 중복 없이 저장

## 단점
- 객체 - 테이블 관계 불일치
- 스키마의 수정에 별도의 과정이 필요하여 덜 유연하다.
- 테이블간의 관계에서 오는 복잡함과 비효율이 발생한다.
- 수평적 확장이 어려워 주로 수직적 확장을 한다.

## 언제 사용할까?
- 관계를 맺고 있는 데이터가 자주 변경되는 어플리케이션의 경우 중복이 없는 RDB가 유리하다.
- 변경의 여지가 적은 명확한 스키마를 사용할 경우

# NoSQL
## 특징
- 데이터의 스키마, 관계가 없다.
- 데이터를 RDB처럼 여러 테이블에 분산하는 게 아니라 관련 데이터를 동일한 컬렉션에 저장한다.

## 장점
- 스키마가 없어서 유연하다. 
- 어플리케이션에서 필요로 하는 형식으로 저장되므로 읽기 - 쓰기 속도가 빠르다.
- 수직, 수평 확장이 모두 용이하다.

## 단점
- 데이터 중복이 발생한다.

## 언제 사용할까?
- 데이터 구조가 변경/확장의 여지가 많은 경우
- 데이터 변경에 비해 조회의 빈도가 높은 경우
- DB를 수평 확장(Scale Out)하는 경우

# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html)
[NoSQL](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788966260706&orderClick=LAG&Kc=)