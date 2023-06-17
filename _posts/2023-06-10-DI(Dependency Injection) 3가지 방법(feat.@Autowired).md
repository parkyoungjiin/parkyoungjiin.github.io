---
layout: post
title: "[SpringBoot] DI(Dependency Injection) 3가지 방법(feat.@Autowired)"
tags: [Springboot]
date: 2023-06-10 11:49
categories : [SpringBoot, Spring]
toc:  true
toc_label: "DI(Dependency Injection) 3가지 방법"
---

## Intro
> 스프링 컨테이너와 스프링 빈에 대한 개념이 잡혔고, 이제 프로젝트에서 자주 사용했던 @Autowired에 대한 개념과 스프링의 특징 중 하나인 DI(Dependency Inversion)을 정리하려 했다. 하지만, Autowired를 포스팅 하기 위해 공부하던 중 DI에 여러가지 방법이 있다는 것을 알게 되었다. 그래서 3가지 방법을 같이 정리한다.

## 3가지 방법
1. Field Injection(필드 주입)
2. Setter Injection(수정자 주입)
3. Constructor Injection(생성자 주입)

## 1. Field Injection
> 필드 상단에 @Autowired를 선언하여 의존성을 주입하는 방법이다. 대부분 이 방법을 사용해서 프로젝트를 진행하였기에 익숙한 방법이다.<br>

- 코드
```java
@Controller
public class BoardController {
	
	@Autowired
	private BoardService boardService;
}
```

### 1-1. @Autowired란
> @Autowired란, 스프링 컨테이너에 등록한 빈에게 의존관계주입이 필요할 때, DI(의존성 주입)을 도와주는 어노테이션이다.<br>

- 스프링에서 빈 인스턴스가 생성된 이후 @Autowired를 설정한 메서드가 자동으로 호출되고, 인스턴스가 자동으로 주입된다.
- @Autowired(required=false) 로 설정하면 빈으로 등록 X, default는 true임.
  - 만약, 의존성 주입할 대상을 찾지 못한다면 애플리케이션 구동에 실패한다.

### 1-2. Field Injection를 무분별하게 사용할 때의 문제점.
> SRP(Single Responsibility Principle)의 원칙을 위배한다.<br>

- 필드 상단에 @Autowired만 작성하면 되기에 의존성을 주입하기 쉬워서 무한정 추가할 수 있다.
- 하지만, 무한정 추가할 경우 SRP(한 클래스는 하나의 책임을 가진다는 원칙)원칙을 위배할 수 있다. 그렇기에 최대한 지양하는 것이 좋다. (3번째 방법인 생성자 주입과 굉장히 코드가 대비된다.)


## 2. Setter Injection (설정자 주입)
> Setter Injection이란, 설정자(setter)의 메서드를 통해 의존성을 주입하는 방법이다. (사용해본 적이 없어서 참고하여 작성함.)<br>

- Setter 메소드에 @Autowired 어노테이션을 붙여 사용한다.
- 수정자 주입을 사용하면 setXXX 메서드를 public으로 열어두어야 하기 때문에 언제 어디서든 변경이 가능하다.
- 코드
```java
@Controller
public class UserController {
    private UserService userService;
    
    @Autowired
    public void setUserService(UserService userService) {
    	this.userService = userService;
    }
}
```

## 3. Constructor Injection (생성자 주입)
> Constructor Injection이란, 생성자를 주입한 뒤 @Autowired를 선언하여 의존성을 주입하는 방법이다.<br>

- 코드
```java
//---------기본 DI 방법----------
@RestController
public class UserController {
	
	private UserRepository userRepository;
	// 생성자 만들기.(Default 생성자 대신, userRepository를 파라미터로 받는 생성자를 통해 DI를 진행함.)
	// -> UserController를 생성(new)할 때 이 생성자를 호출하여 @Repository 어노테이션이 있는 타입이 있다면 주입하는 것.
	public UserController(UserRepository userRepository) {
		this.userRepository = userRepository;
	}
//----------final과 RequiredArgsConstrutor(lombok) 사용 -------
@RequiredArgsConstrutor
@RestController
public class UserController {
	//DI 과정(@Autowired 발전된 코드)
	private final UserRepository userRepository;
}
	/*
		@RequiredArgsConstrutor, final 을 사용하여 밑 코드 생략 가능함. 
public UserController(UserRepository userRepository) {
		this.userRepository = userRepository;
	*/
```

## 결론
> Spring Framwork reference 권장하는 방법은 Constructor Injection(생성자 주입)이다. 테스트 하기에 용이하며 순환 참조를 방조할 수 있다는 장점이 있기 때문이다. 필드 주입과 @Autowired를 사용하는 것을 지양하고 생성자 주입을 사용하려고 노력할 것이다.

## 참고 사이트
[DI 3가지 방법 참고한 게시물1](https://velog.io/@gillog/Spring-DIDependency-Injection-%EC%84%B8-%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95)<br>
[DI 3가지 방법 참고한 게시물2](https://dev-coco.tistory.com/70)
