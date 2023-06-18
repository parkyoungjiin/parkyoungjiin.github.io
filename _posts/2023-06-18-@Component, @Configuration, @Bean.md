---
layout: post
title: "[SpringBoot] 어노테이션과 리플렉션"
tags: [Springboot]
date: 2023-06-16 11:49
categories : [SpringBoot, Spring]
toc:  true
toc_label: "어노테이션과 리플렉션"
---

## Intro
> 어노테이션, 리플렉션을 정리하면서 자주 사용했던 @component, @Configuration, @Bean을 정리하면서 차이점이 있고, 구분하여 정리할 필요가 있다고 생각이 들어서 정리한다.


## @Component
- 개발자가 생성한 클래스를 스프링의 Bean으로 등록하고자 할 때 사용.
- 스프링은 @Component 어노테이션을 보고 Bean으로 등록한다.

## @ComponentScan
- @Component, @Controller, @Service, @Repository, @Configuration이 선언된 클래스가 있으면 Bean에 등록한다.

## @Bean
- @Bean은 개발자가 외부 라이브러리와 같은 제어 불가능한 것들을 Bean으로 만들 때 사용하는 어노테이션임.
- 수동으로 스프링 컨테이너에 빈을 등록하는 방법이며,  <span style="color:red">@Configuration과 반드시 같이 사용해야만 한다.</span>
  -  <span style="color:blue">why?</span> 스프링 컨테이너는 @Configuration이 붙은 클래스를 자동으로 빈으로 등록한다. 그리고 해당 클래스를 파싱하여 @Bean이 있는 메소드를 찾아 빈에 등록한다. 그렇기에 반드시 같이 사용해야 함.
  - <span style="color:blue">클래스에 @Configuration을 , 메서드에 @Bean을 선언하면 된다!</span>
  - 

### @Component과 @Configuration & @Bean 차이점.
- @Component와 @Configuration & @Bean 두 개 모두 빈을 등록한다는 공통점을 갖고 있는데 무슨 차이점이 있는걸까?
- @Component의 경우는 개발자가 직접 컨트롤할 수 있는 클래스


## 리플렉션(Reflection)이란?
> 사전적 의미로는 투영을 뜻한다. 구체적인 클래스 타입을 알지 못하더라도 그 클래스의 메서드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API를 의미하며 컴파일 시간이 아닌 실행시간(ex.요청 들어왔을 때)에 동적으로 특정 클래스의 정보를 추출할 수 있는 프로그래밍 기법이라 할 수 있다.

- 요청(ex. http://localhost:8080/context-path/xxxx)이 들어오게 되면 리플렉션을 통해 context-path뒤에 붙은 주소를 기반으로 컨트롤러에서 함수를 찾아낸다.
- 즉, 주소를 작성해둘 때는 어떤 클래스를 사용할 지 모르지만 런타임 시점에 가져와 실행해야 하는 경우 리플렉션이 필요하다.
  - 
- 스프링에서는 어노테이션이 리플렉션을 제공함.
## 참고 사이트
[참고 게시물 1](https://mangkyu.tistory.com/75)
[참고 게시물 2](https://mangkyu.tistory.com/234)

