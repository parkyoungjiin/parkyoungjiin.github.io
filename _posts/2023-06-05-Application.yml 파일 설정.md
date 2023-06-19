---
layout: post
title: "[SpringBoot]Applicaton.yml 파일 설정"
tags: [Springboot]
date: 2023-06-05 11:49
categories : [SpringBoot]
toc:  true
toc_label: "스프링 부트"
---

## Intro
> 스프링 부트 강의를 통해 블로그 만들기를 하고 있는데, 부트 환경 설정부터 개념 정리, 스프링 시큐리티, 카카오 로그인 등 강의 들었던 내용을 정리하고자 한다.

## Application.yml
1. 개념
- 레거시에서 web.xml, root-context.xml, servlet-context.xml 설정했던 작업들을 한 파일로 작성할 수 있는 파일이다. Application.yml 파일로 부트 대부분의 설정을 한다고 생각하면 된다.

2. 특징
- <span style='color:#1E90FF'>형식 : key: value</span>(<span style="color:red">주의 !<span> 콜론 뒤에 공백을 한 칸 무조건 띄워야함.)
- 중괄호가 없음.
- 들여쓰기 스페이스 2칸 필수(지키지 않으면 파일 동작 X)
- yaml 파일은 간소화하여 <span style='color:#1E90FF'>가독성이 좋은 파일임.</span>
    - properties의 경우는 중복되는 코드들이 있는 반면, Application.yml은 중복을 제거하여 가독성이 좋다.
    - 계층 구조로 되어있어서 가독성이 좋음.
- 기본으로 프로젝트 생성 시에는 properties로 되어있는데, 이를 rename을 통해 변경해줘야 한다.
- 파일위치 : src/main/resources/

## Application.yml 설정
### 1. 서버 설정
- 코드
```yml
server:
  port: 8000
  servlet:
    context-path: /
    encoding:
      charset: UTF-8
      enabled: true
      force: true
```
- context-path : 프로젝트 실행 시 기본 진입점.

### 2. DB 설정
- 코드
```yml
spring:
  mvc:
    view:
      prefix: /WEB-INF/views/
      suffix: .jsp
      
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/blog?serverTimezone=Asia/Seoul
    username: DB 아이디
    password: DB 비밀번호
```
- prefix(접두어) : controller에서 뷰를 리턴할 때 뷰 파일이 위치한 경로를 지정해준다.
- suffix(접미어) : controller에서 뷰를 리턴할 때 뷰 파일의 형식을 지정함.
- prefix, suffix를 통해 controller에서 중복으로 작성하는 부분을 피할 수 있다.


### 3. JPA 설정
- 코드
```yml
jpa:
    open-in-view: true
    hibernate:
      ddl-auto: update
      naming:
        physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
    show-sql: true
    properties:
      "[hibernate.format_sql]": true
```
- open-in-view : true/false
  - **OSIV(Open-Session-In-View)**라 하며, JPA에서 영속성 컨텍스트를 뷰까지 열어두는 기능이다.
- ddl-auto
    - ddl-auto : create
        - 서버를 시작할 때 마다 DB를 생성한다.
        - **주의** ! 데이터가 들어있는 경우 기존 데이터를 삭제하기에 처음에 DB를 생성한 후 update로 수정해야 한다.
    - ddl-auto : update
        - DB에서 수정된 내용들만 DB에 반영한다.
    - ddl-auto : none
        - 아무런 작업을 하지 않는다.
- show-sql: true/false
    - SQL 작업 내용을 콘솔창 출력 여부(true : 출력 / false : 미출력)
- properties:hibernate.format_sql: true
    - show-sql 내용을 깔끔하게 출력해준다.

    

