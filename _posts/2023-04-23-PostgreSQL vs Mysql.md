---
layout: post
title: "[SQL]PostgreSQL vs Mysql"
tags: [CS, PostgreSQL, Mysql]
date: 2023-04-23 11:49
toc:  true
toc_label: "SQL"
---
## Intro
> DB를 사용할 때 Mysql을 자주 사용했는데, 새로운 DB가 있다는 것을 알게 되었다. 최근에 사용률이 증가하고 있는 Postgre라는 DB를 알아보고 이를 기록한다.

## PostgreSQL이란
1. PostgreSQL 개념
- 개발자 커뮤니티에서 만들어진 SQL으로, 다른 DBMS보다 기능이 더 많다.
    - [Postgre의 역사](https://sungsoo.github.io/2014/08/01/postgresql.md.html)
- 테이블, 열에 대한 정보를 단순히 저장만 하는 것이 아니라, 사용자가 **데이터 형식/인덱스 형식/함수형 언어**를 정의할 수 있다.
    - 본래 데이터 형식 지원 + 사용자 지정 함수도 가능.

2. PostgreSQL 특징
    - **객체 관계형** 데이터베이스 관리 시스템이다.
        - Mysql의 경우는 순수 관계형 데이터베이스
    - 트랜잭션과 ACID를 지원한다. 
    - **동시 연결성 높음** : 트랜잭션을 할 때 읽기 잠금을 사용할 필요가 없어 확장성이 높다
    - **NoSQL 지원**
        - NoSQL, 다양한 데이터 형식을 지원
    - JSON, hstore, XML 등 **다양한 데이터 형식을 기본적 지원**
    - DB 크기에 제한을 두지 않는다.
    - **MVCC(다중 버전 동시성 제어) 지원**
    - **복잡한 쿼리, 대규모 데이터베이스를 다룰 수 있는 풍부한 기능이 필요할 경우** PostgreSQL을 사용한다.

3. Vacuum
    - Vacuum이란, Vacuum은 PostgreSQL에만 존재하는 고유 명령어로, 오래된 영역을 재사용 하거나 정리해주는 명령어이다.
    - 특징에 명시된 MVCC 기법을 사용하기에, 특정 Row를 추가, 업데이트를 할 경우, 디스크 상의 해당 Row를 물리적으로 업데이트하여 사용하지 않고, 새로운 영역을 할당해서 사용한다.
    - [자세한 내용은 여기서 확인!](https://mangkyu.tistory.com/71)

## Mysql
1. 가장 많이 사용하는 SQL
2. 

## 코딩 차이점
|내용|Mysql|PostgreSQL|
|---|---|---|
|대소문자 구분 여부|대소문자 구분 X|대소문자 구분 O|  
|기본문자 집합, 문자열|UTF-8로 변환 필요|UTF-8로 변환 필요 없음.(허용X)|
|IF, IFNULL, CASE문|모두 사용 가능|CASE문만 사용가능<br>IF 대신, coalesce()를 사용함|

## 결론
1. 복잡한 쿼리, 대규모 데이터베이스를 다룰 수 있는 풍부한 기능이 필요할 경우 PostgreSQL이 선택지가 될 수 있음.
2. 대중성, 사용용이, 안정성, 속도 등을 원한다면 MySQL을 사용 ( 최근 NoSQL도 지원)