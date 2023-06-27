---
layout: post
title: "[JPA] 즉시로딩(EAGER) & 지연로딩(LAZY)"
tags: [JPA]
date: 2023-06-26 11:49
# last_modified_at: 2023-06-24 20:23

categories : [SpringBoot, JPA]
toc:  true
toc_label: "즉시로딩(EAGER) & 지연로딩(LAZY)"
---

## Intro
> 객체의 필드에 @ManyToOne 설정할 때 Fetch 속성이 나온다. 여기서 LAZY와 EAGER을 선택할 수 있는데, 즉시로딩과 지연로딩이라는 개념이며 이를 정리 하고자 한다.

## 즉시로딩(EAGER) vs 지연로딩(LAZY)
> 이 2가지 개념의 공통점은 JPA에서 데이터를 조회할 때 FetchType을 설정한다는 점이다.<br> 
> 여기서 FetchType이란, 하나의 Entity(객체)를 조회할 때, 연관관계에 있는 객체들을 어떻게 가져올 것인가를 나타내는 설정값이다.<br> 
> <span style ="color:#1E90FF">즉시로딩(EAGER)은</span> 데이터를 조회할 때 연관된 모든 객체의 데이터까지 한 번에 불러 오는 것이다.<br> 
> <span style ="color:#1E90FF">지연로딩(LAZY)은</span> 필요한 시점에 연관된 객체의 데이터를 불러오는 것을 말한다.

## 즉시로딩(EAGER)
- 즉시로딩(EAGER)의 JPA fetchType의 기본값 : @xxToOne
- 예시
  - ```@xxToxx(fetch=fetchType.EAGER)```
  - 가정 : Board(N) & User(1) => @ManyToOne
    
    ```java
    //-------Board 객체----------
    public class Board {
    @Id
    @GeneratedValue
    private int id;
    
    @Column(nullable = false, length = 100)
    private String title;
    
    @Lob // 대용량 데이터
    @Column(columnDefinition = "LONGTEXT")
    private String content;
    
    private int count; // 조회
    
    @ManyToOne(fetch = FetchType.EAGER) // Board를 조회할 때 User도 같이 조회한다(즉시로딩을 사용한다.)
    @JoinColumn(name = "userId")
    private User user; 
        
    @CreationTimestamp
    private Timestamp createDate;
	
    }

    //--------User 객체----------
    public class User {
      @Id
	    @GeneratedValue(strategy = GenerationType.IDENTITY) 
	    private int id; 

      @Column(nullable = false, length = 100, unique = true)
      private String username; // 유저네임
      
      @Column(nullable = false, length = 200) 
      private String password; // 패스워드
      
      @Column(nullable = false, length = 50)
      private String email; // 이메일
    }
    ```
- 결과
  - Board를 조회하는 시점에 User 객체도 같이 조회하는 쿼리를 한꺼번에 날려서 같이 데이터를 불러온다.
  - 즉, EAGER 전략은 해당 객체를 불러올 때 fetchType을 EAGER로 해둔 객체도 같이 불러온다는 것을 알 수 있다.

## 지연로딩(LAZY)
- 지연로딩(LAZY))의 JPA fetchType의 기본값 : @xxToMany
- 예시
  - ```@xxToxx(fetch=fetchType.LAZY)```
  - 가정 : Board(1) & Reply() => @OneToMany
    
    ```java
    //-------Board 객체----------
    public class Board {
    @Id
    @GeneratedValue
    private int id;
    
    @Column(nullable = false, length = 100)
    private String title;
    
    @Lob // 대용량 데이터
    @Column(columnDefinition = "LONGTEXT")
    private String content;
    
    private int count; // 조회
    
    @ManyToOne(fetch = FetchType.LAZY) // Board를 조회할 때 User를 불러오지 않는다.(LAZY 전략을 사용한다.)
    @JoinColumn(name = "userId")
    private User user; 
        
    @CreationTimestamp
    private Timestamp createDate;
	
    }

    //--------User 객체----------
    public class User {
      @Id
	    @GeneratedValue(strategy = GenerationType.IDENTITY) 
	    private int id; 

      @Column(nullable = false, length = 100, unique = true)
      private String username; // 유저네임
      
      @Column(nullable = false, length = 200) 
      private String password; // 패스워드
      
      @Column(nullable = false, length = 50)
      private String email; // 이메일
    }
    ```
- 결과
  - LAZY 전략은 EAGER과 달리 Board를 조회하는 시점에 User 객체를 조회하는 쿼리를 날리지 않고 Board만 조회한다.
  - 즉, LAZY는 전략은 해당 객체를 불러올 때 fetchType을 LAZY 설정하게 되면 연관관계에 있는 나머지 객체는 조회를 미룬다는 것을 알 수 있다.



## 참고 사이트
[즉시로딩 vs 지연로딩 참고 게시물](https://velog.io/@jin0849/JPA-%EC%A6%89%EC%8B%9C%EB%A1%9C%EB%94%A9EAGER%EA%B3%BC-%EC%A7%80%EC%97%B0%EB%A1%9C%EB%94%A9LAZY)<br>
[즉시로딩 vs 지연로딩 참고 게시물2](https://thalals.tistory.com/290)<br>


