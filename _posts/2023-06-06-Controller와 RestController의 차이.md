---
layout: post
title: "[SpringBoot] Controller와 RestController의 차이"
tags: [Springboot]
date: 2023-06-06 11:49
categories : [SpringBoot, Spring]
toc:  true
toc_label: "Controller와 RestController의 차이"
---

## Intro
> @Controller와, @RestController의 차이를 명확하게 기억하기 위해 정리한다.

## @Controller
1. @Controller의 경우는 View 페이지를 반환하기 위해 사용한다.
2. @Controller 어노테이션을 사용한 경우 JSON 데이터를 응답받기 위해서는 @ResponseBody를 사용해야 한다.
  - @ResponseBody를 사용하면 HTTP Response Body에 데이터를 담아 요청을 받을 수 있다.
3. 원리
- URI 형식으로 웹 서비스에 요청
- DispatcherServlet이 처리할 대상 찾음.
- Controller에 위임.
- 요청 처리 후 ViewName 반환.
- ViewResolver를 통해 ViewName에 해당하는 View를 사용자에게 반환.

## @RestController
1. Controller에 ResponseBody가 추가된 어노테이션이다.
2. JSON 형태로 객체 데이터를 반환한다.
3. 원리
  - 웹브라우저에서 요청 시 응답을 해줄 때 JSON 형태로 리턴해야 한다.
  - 이 때, 자바 오브젝트를 리턴하면 MessageConverter가 자동으로 Jackson 라이브러리를 호출하여 JSON 데이터로 변환하여 응답한다.

## 결론
- Controller -> HTML 파일 응답.
- RestController -> Data 응답.
- ```@RestController = @Controller + @ResponseBody```


## 참고 사이트
[RestController vs Controller 참고 블로그](https://mangkyu.tistory.com/49)<br>
[로직그림이 잘 설명되어 있는 블로그](https://dncjf64.tistory.com/288)
