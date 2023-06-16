---
layout: post
title: "[SpringBoot] @RequestBody, @RequestParam, @PathVariable 정리"
tags: [Springboot]
date: 2023-06-11 11:49
categories : [SpringBoot, Spring]
toc:  true
toc_label: "RequestBody, RequestParam 정리"
---

## Intro
> 자주 사용하던 어노테이션인 RequestBody, RequestParam, PathVariable의 차이를 명확하게 정리하기 위해 정리한다.

## @RequestBody
- RequestBody는 HTTP 요청이 들어왔을 때 Body에 담긴 값을 <span style="color: red">자바 객체로 변환</span> 해주는 어노테이션이다.
- 비동기 처리(AJAX)를 할 때 사용한다.
- xml, json 기반 메시지를 사용하는 요청의 경우 유용하다.

## @RequestParam
- RequestParam는 HTTP 요청이 들어왔을 때 URI의 <span style="color: red">queryString에 붙은 name=value 형태의 값을 받을 때</span> 사용하는 어노테이션이다.
- 예시 : http://localhost:8080/user=1&page=1
- 예시의 요청이 들어오면 user라는 변수와 page라는 변수를 받을 때 사용 가능함.

## @PathVariable
- REST API에서 요청이 들어올 때 URI에 가변형 변수 부분을 받는 어노테이션이다.
- 여기서 변수뒤에 오는 값과 매핑 주소의 변수명과 동일해야 함.
- 예시 : http://localhost:8080/api/user/1
- 코드
```java
@GetMapping("/api/user/{id}")
public void findById(@PathVariable int id) { // int id == {id}  변수명이 같아야 함.
		System.out.println("id:" + id);
		// 출력 => id: 1

	}
```

## 결론
- 쿼리스트링에 붙은 변수를 받기 위해서는 @RequestParam을 사용한다.
- Post로 전송 시 자바 객체(ex, User 객체)로 받기 위해서는 @RequestBody를 사용한다.
- JSON, AJAX를 사용할 때 @RequestBody를 사용한다.
- API 요청이 있을 때 변수를 사용하고 싶다면 @PathVariable을 사용한다.

## 참고 사이트
[참고 게시물](https://u0hun.tistory.com/21)
