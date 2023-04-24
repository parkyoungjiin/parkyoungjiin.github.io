---
layout: post
title: "[CS]자바 자료형(HashSet, HashMap)"
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
- 순서가 중요하지 않다.(저장 순서 유지 X)
- null 요소도 허용된다.
- 출력 시 리스트 형태로 출력된다 (대괄호형태로 출력).

### 중복을 걸러내는 과정
- HashSet은 객체를 저장하기 전에, hashCode() 메서드를 호출하여 해시코드를 얻는다.
- 저장되어 있는 객체들의 해시코드를 비교하여 같은 해시코드가 있다면 다시 equals()메서드로 두 객체를 비교하여 True가 나올 경우 동일한 객체로 판단하여 저장하지 않는다.

### HashSet 메서드
1. 선언

```
HashSet<데이터타입> 변수명 = new HashSet<데이터타입>() // 기본 선언형태;
HashSet<Integer> set = new HashSet<Integer>(Arrays.asList(1,2,3)); //초기값 지정형태
```

2. 메서드(추가, 삭제, 사이즈확인, 포함여부, 출력)
- `add(value)`
```
HashSet<Integer> set = new HashSet<Integer>(); //HashSet생성
set.add(1); //값 1 추가
set.add(2); //값 2 추가
set.add(3); //값 3 추가
```
- `remove(value)` & `clear()`
```
set.remove(1); // 값 1 삭제
set.clear(); // 모든 값 삭제
```

- `size()`
```
HashSet<Integer> set = new HashSet<Integer>(Arrays.asList(1,2,3,4)); //HashSet 생성
System.out.println("set 크기 : " + set.size()); //set 크기 : 4
```
- `contains(value)`
```
HashSet<Integer> set = new HashSet<Integer>(Arrays.asList(1,2,3,4)); //HashSet 생성
System.out.println("확인 : " + set.contains(1)) // 확인 : true
```

- 출력 (Set컬렉션을 그냥 print하게 되면 대괄호 [ ]로 묶여서 set의 전체 값이 출력된다.)
```
HashSet<Integer> set = new HashSet<Integer>(Arrays.asList(1,2,3,4)); //HashSet 생성
System.out.println("출력 : " + set) // 출력 : [1,2,3,4]
```



## HashMap
HashMap이란, Map 인터페이스를 구현한 컬렉션이다. (**인터페이스를 구현한 것이기에 Map의 성질을 모두 갖고 있다**)

### HashMap 특징 
- Map은 키:값 형태로 저장된다.
- 값은 중복 저장되지만 키는 중복 저장될 수 없다는 특징을 갖고 있다.

### HashMap 메서드
1. 선언

```
// HashMap 생성(기본형태)
HashMap<String,String> map1 = new HashMap<String,String>(); 

// HashMap 생성 후 초기값 지정(바로 값 추가 필요할 경우)
HashMap<String,String> map2 = new HashMap<String,String>(){{ 
    put("a","b");
}};
```

2. 메서드(값 추가, 삭제, 출력)
- `put(key, value)`
```
map.put("개발언어","자바"); //'개발언어'라는 키에 '자바'라는 값이 들어감.
map.put("DB","mysql"); //'DB'라는 키에 'mysql;이라는 값이 들어감.
map.put("형상관리","Git"); //'형상관리'라는 키에 'Git'이라는 값이 들어감.
```
- `remove(key)` & `clear()`
```
map.remove("개발언어"); //'개발언어'에 해당하는 값 제거
map.clear(); //모든 값 제거
```

- `get(키)` :키에 대응하는 값이 출력된다.  
```
map.get("DB") // 결과 : mysql
map.get("형상관리") // 결과 : Git
```
- `for반복문과 entrySet()활용`
```
for (Entry<Integer, String> entry : map.entrySet()) {
    System.out.println("[Key]:" + entry.getKey() + " [Value]:" + entry.getValue());
}
// [Key]: DB [Value] : mysql
// [Key]: 형상관리 [Value] : Git
```

- `containsKey 사용예 (이미 HashMap에 키가 있으면 값을 덮어쓰지 않는 예)`
```
//키가 들어있는지 확인. 있으면 덮어쓰지 않는다.
if(!map.containsKey("DB")){
    map.put("DB", PostgreSQL); 
};
```


## 참조 사이트
[HashSet 참조 사이트1](https://crazykim2.tistory.com/474)<br>
[HashSet 참조 사이트2](https://coding-factory.tistory.com/554)<br>
[HashMap 참조 사이트1](https://coding-factory.tistory.com/556)<br>
[HashMap 참조 사이트2](https://crazykim2.tistory.com/587)<br>
[HashMap 참조 사이트3](https://reakwon.tistory.com/151)<br>


