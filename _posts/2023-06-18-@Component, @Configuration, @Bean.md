---
layout: post
title: "[Spring] @Component, @Configuration, @Bean 정리"
tags: [Spring]
date: 2023-06-18 11:49
categories : [Spring]
toc:  true
toc_label: "@Component, @Configuration, @Bean 정리"
---

## Intro
> 어노테이션, 리플렉션을 정리하면서 자주 사용했던 @component, @Configuration, @Bean을 정리하면서 차이점이 있고, 구분하여 정리할 필요가 있다고 생각이 들어서 정리한다.


## @Component
- 개발자가 직접 생성한 클래스를 스프링의 Bean으로 등록하고자 할 때 사용.
- 스프링은 @Component 어노테이션을 보고 Bean으로 등록한다.

## @Configuration & @Bean
- @Bean은 개발자가 외부 라이브러리와 같은 제어 불가능한 것들을 Bean으로 만들 때 사용하는 어노테이션임.
- 수동으로 스프링 컨테이너에 빈을 등록하는 방법이며,  <span style="color:#FF6347">@Configuration과 반드시 같이 사용해야만 한다.</span>
  -  <span style="color:#1E90FF">why?</span> 스프링 컨테이너는 @Configuration이 붙은 클래스를 자동으로 빈으로 등록한다. 그리고 해당 클래스를 파싱하여 @Bean이 있는 메소드를 찾아 빈에 등록한다. 그렇기에 반드시 같이 사용해야 함.
  - <span style="color:#1E90FF">클래스에 @Configuration을 , 메서드에 @Bean을 선언하면 된다!</span>
- 메서드 이름이 빈 이름으로 등록 되기에 중복된 빈 이름이 존재하지 않도록 주의 해야한다.
- 코드 예시
  ```java
  @Configuration
  public class EncoderConfig {
	@Bean
	public BCryptPasswordEncoder encoder() {
		return new BCryptPasswordEncoder();
	}
  ```

## @Component과 @Configuration & @Bean 차이점.
- @Component와 @Configuration & @Bean <span style="color:#1E90FF">두가지 방법 모두 빈을 등록한다는 공통점<span>을 갖고 있는데 무슨 차이점이 있는걸까?
- @Component의 경우는 <span style="color:#FF6347">개발자가 직접 컨트롤할 수 있는(직접 개발한) 클래스</span>에 사용하는 반면, @Configuration & @Bean의 경우에는 <span style="color:#FF6347">개발자가 통제할 수 없는 라이브러리 클래스</span>에 사용한다는 차이점이 존재한다.



 
## 참고 사이트
[참고 게시물 1](https://mangkyu.tistory.com/75)
[참고 게시물 2](https://mangkyu.tistory.com/234)
[참고 게시물 3](https://velog.io/@leesomyoung/SpringBoot-%EB%B9%88-%EB%93%B1%EB%A1%9D%EC%9D%84-%EC%9C%84%ED%95%9C-Configuration-Bean-Component)

