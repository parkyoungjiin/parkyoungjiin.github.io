---
layout: post
title: 자바 자료형(HashSet, HashMap)
tags: [CS, JAVA]
date: 2023-04-09 11:49
toc:  true
toc_label: "자료형"
---

## Intro
> 정보처리기사 실기에서 나온 자바 자료형 중에서 몰랐던 내용들을 정리한다.

## HashSet
HashSet이란, set 인터페이스를 구현한 클래스이다.

### HashSet 특징<br>
- 중복을 허용하지 않는다.
- 순서가 중요하지 않다.
- null 요소도 허용된다.
- 출력 시 리스트 형태로 출력된다.

### 중복을 걸러내는 과정
- HashSet은 객체를 저장하기 전에, hashCode() 메서드를 호출하여 해시코드를 얻는다.
- 저장되어 있는 객체들의 해시코드를 비교하여 같은 해시코드가 있다면 다시 equals()메서드로 두 객체를 비교하여 True가 나올 경우 동일한 객체로 판단하여 저장하지 않는다.

### HashSet 메서드
메서드
- `add()`
- `remove()`
- `size()`
- `clear()`
선언
- `set 변수명 = new HashSet();`
- `Hashset 변수명 = new hashSet();`

## HashMap
HashMap이란, Map 인터페이스를 구현한 컬렉션이다. (***인터페이스를 구현한 것이기에 Map의 성질을 모두 갖고 있다***)
Map은 키:값 형태로 저장되며, 값은 중복 저장되지만 키는 중복 저장될 수 없다는 특징을 갖고 있다.

메서드
- `put()`
- `remove()`
- `clear()`
- `get(키)`
    - 키에 대응하는 값이 출력된다.


### 참조 사이트
[HashSet 참조 사이트](https://crazykim2.tistory.com/474)<br>
