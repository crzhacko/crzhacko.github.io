---
layout: post
title: "자바 ORM 표준 JPA 프로그래밍 1장 2장"
date: 2020-02-05 05:50:00 +0900
categories: jpa
---

# 1장 JPA 소개

1.  SQL을 직접 다를 때 발생하는 문제점

    - 반복
      - 단순한 CRUD 작업에도 SQL작성과 JDBC API를 사용을 반복해야 한다.
    - SQL에 의존적인 개발
      - 요구사항 추가 또는 변경시 작업해야하는 코드량이 많다.
    - 문제 발생 시 코드 추적이 어렵고, 엔티티를 신뢰할 수 없다.
      - 계층 분할이 어렵다.(SQL을 직접 확인해야 함.)
    - JPA와 문제 해결

      - 저장 기능

      ```java
      jpa.persist(member); // 저장
      ```

      - 조회 기능

      ```java
      String memberId = "helloId";
      Member member = jpa.find(Member.class, memberid); // 조회
      ```

      - 수정 기능

      ```java
      Member member = jpa.find(Member.class, memberid);
      member.setName("이름변경"); // 수정
      ```

      - 연관된 객체 조회

      ```java
      Member member = jpa.find(Member.class, memberId);
      Team team = member.getTeam(); // 연관된 객체 조회
      ```

      > SQL에 의존적인 개발 방식
      >
      > > DAO

      ```java
      public class MemberDAO {
          public Member find(String memberId) {...}
          public Member findWithTeam(String memberId){...}
      }
      ```

      > > SQL

      ```sql
      SELECT MEMBER_ID, NAME, TEL FROM MEMBER M -- find
      ```

      ```sql
      SELECT M.MEMBER_ID, M.NAME, M.TEL, T.TEAM_ID, T.TEAM_NAME -- findWithTeam
      FROM MEMBER M
      JOIN TEAM T
          ON M.TEAM_ID = T.TEAM_ID
      ```

2.  패러다임의 불일치

    - 상속 - 관계형 디비는 상속의 개념이 없어, 객체를 분할해서 각각의 SQL을 작성해야함.
    - 연관관계 - 객체는 참조를 통해, 테이블은 외래키를 사용해서 연관관계를 가짐
    - 객체 그래프 탐색 - `JPA와 문제 해결 > * SQL에 의존적인 개발 방식` 참조
    - 비교 - 같은 트랜잭션 내에서 조회된 같은 객체에 대해 동일성 비교가 가능

3.  JPA란 무엇인가?
    - ORM<sub>Object-Relational Mapping</sub> - 객체와 관계형 데이터베이스를 매핑하는 기술
    - JPA<sub>Java Persistence API</sub> - 자바 진영의 ORM 기술 표준
    - 왜 JPA를 사용해야 하는가?
      - 생산성
      - 유지보수
      - 패러다임의 불일치 해결
      - 성능
      - 데이터 접근 추상화와 벤더 독립성

# 2장 JPA 시작

- 키워드
  - 데이터베이스 방언
    - 특정 데이터베이스만의 고유 기능 - 데이터타입, 함수명, 페이징 처리 등
  - JPQL
    - SQL을 추상화한 객체지향 쿼리 언어 - SQL문법과 유사하나 SQL은 데이터베이스 테이블을 대상으로 쿼리하는 반면, JPQL은 엔티티 객체를 대상으로 쿼리

참고서적: 자바 ORM 표준 JPA 프로그래밍
