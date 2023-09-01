---
layout: single
title: "부트캠프 48일차"
tag: [bootcamp, spring framework, spring boot, jpa]
---

# Spring Boot

## ORM

&nbsp;&nbsp; ORM(Object Relational Mapping)이란, 객체와 RDB(Relational Database)의 테이블을 자동으로 매핑하는 기술이다.
객체 지향 언어의 객체와 RDB의 테이블은 패러다임 불일치가 존재하기 때문에 곧바로 이 둘을 매핑하기란 쉽지 않다.  
&nbsp;&nbsp; 때문에 객체와 테이블 사이에서 이 둘을 매핑시켜주는 역할이 필요한데 그것을 가능케 하는 기술이 바로 ORM이다.

> 장점

- DB의 쿼리를 객체지향적으로 조작할 수 있다.
- 재사용 및 유지보수에 용이하다.
- DB에 대한 종속성이 줄어든다.

> 단점

- ORM만으로 모든 쿼리를 구현하는 데에는 한계가 있다.
- 애플리케이션의 객체 관점과 DB의 관계 관점의 불일치가 발생한다.

<br>

## JPA

&nbsp;&nbsp; JPA(Java Persistence API)는 JAVA에서 채택한 ORM 기술 표준으로, 인터페이스의 모음이다.
JPA은 내부적으로 JDBC를 사용해서 개발자 대신 적절한 SQL을 생성해준다.  
&nbsp;&nbsp; JPA의 구현체는 대표적으로 세 가지가 있다. 이 중 가장 많이 사용되는 구현체는 Hibernate이다.

1. Hibernate
2. EclipseLink
3. DataNucleus

### Spring Data JPA

&nbsp;&nbsp; Spring Data JPA는 JPA를 편리하게 사용할 수 있도록 도와주는 스프링의 프로젝트이다.
Spring Data JPA는 하이버네이트에서 자주 사용되는 기능을 더 쉽게 사용할 수 있게 구현한 라이브러리이며, 기본적인 기능들은 인터페이스로 제공된다.

#### Entity 설계

1. @Entity : 해당 클래스를 엔티티로 설정
2. @Table : 엔티티 이름과 테이블 이름이 다를 경우 사용
3. @Id : 기본값
4. @GeneratedValue : 기본값을 자동으로 생성하는 방법 설정
   - 애플리케이션에서 자체적으로 값을 생성할 경우 사용하지 않음
   - AUTO(default) : DB에 맞게 자동 생성
   - IDENTITY : 기본값 생성을 DB에 위임(AUTO_INCREMENT)
   - SEQUENCE : @SequenceGenerator 어노테이션으로 식별자 생성기를 설정하고 값을 자동 주입 받음
   - TABLE : 어떤 DBMS를 사용하더라도 동일하게 동작하기를 원할 경우 사용
5. @Column : 필드를 DB 컬럼에 매핑할 때 필요한 설정을 추가하고 싶을 때 사용
6. @Transient : DB와 매핑하지 않도록 설정

#### Repository 설계

1. JpaRepository<T, ID>를 상속 받는 인터페이스를 생성(따로 구현하지 않아도 된다.)
   - T : 엔티티 타입
   - ID : 기본값 타입
2. Repository 메서드명 규칙
   - findBy{fieldName} : findById(Long id)
   - And/Or : findByIdAndName(Long id, String name)
   - Like/NotLike : SQL의 like와 동일한 기능
   - StartsWith/StartingWith : 특정 키워드로 시작하는 문자열 조건
   - EndsWith/EndingWith : 특정 키워드로 끝나는 문자열 조건
   - IsNull/IsNotNull : 레코드 값이 Null이거나 Null이 아닌 값을 검색
   - True/False : boolean 타입의 레코드를 검색
   - Before/After : 시간을 기준으로 검색
   - LessThan/GreaterThan : 특정 숫자를 기준으로 비교
   - Between : 두 값 사이의 데이터를 조회
   - OrderBy : SQL의 order by와 동일한 기능 : findByNameOrderByPriceAsc(String name)
   - countBy : SQL의 count와 동일한 기능

#### DAO 설계

&nbsp;&nbsp; 일반적으로 인터페이스 - 구현으로 설계함

1. getById : 프록시 객체를 반환
2. findById : 실제 객체를 반환

<br>

___

**[참고]**  
장정우, 스프링 부트 핵심 가이드(스프링 부트를 활용한 애플리케이션 개발 실무)  
깃허브 주소 : [https://github.com/chocolaggibbiddori/springboot-wikibooks](https://github.com/chocolaggibbiddori/springboot-wikibooks)

[<== 부트캠프 46일차](/bootcamp-day46)