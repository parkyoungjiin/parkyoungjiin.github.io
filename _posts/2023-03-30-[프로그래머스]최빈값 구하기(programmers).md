---
layout: post
title: [알고리즘]최빈값 구하기(programmers)
tags: ["Algorithm", "알고리즘"]
date: 2023-03-30 11:49
toc:  true
toc_label: "최빈값"
---

## Intro
> 프로그래머스 입문 0단계를 푸는 도중, 안풀렸던 문제를 블로그에 기록하려 한다.<br>
0단계도 쉽지 않다,,

## 문제
최빈값은 주어진 값 중에서 가장 자주 나오는 값을 의미합니다. 정수 배열 array가 매개변수로 주어질 때, 최빈값을 return 하도록 solution 함수를 완성해보세요. 최빈값이 여러 개면 -1을 return 합니다.

처음 생각 -> 최소공배수를 활용한 풀이법 (풀리지 않아서 해설을 먼저 보았다.)
다른 분의 풀이법 -> 딕셔너리를 사용한 풀이

딕셔너리를 사용한 경험이 많이 없어서 떠오르지 않았다.

## 딕셔너리
- 딕셔너리란, 직역하면 사전이라는 뜻을 갖고 있는데 사람 = people 처럼 **키:값 형태**로 저장하는 자료형이다. <br>
- value(값)에는 문자열, 숫자, 리스트, 튜플 다 들어갈 수 있다.
- 딕셔너리 문법 
```Python
# 선언
dict ={}

# 쌍 추가
dict[key] = 값

dict['a'] = 1 # a라는 키에 대응하는 1이라는 값이 추가.
>> dict[a:1]

# 쌍 제거 (키 : 값 삭제)
del dict[key]

del dict[a]
>> {} # 딕셔너리가 비었을 때 빈 중괄호를 리턴함.

# keys()
dict ={a:1, b:2}

dict.keys()
>> dict_keys(['a', 'b'])
# **주의** python3부터 keys를 할 경우 dict_keys라는 객체를 리턴한다.
# 만약, 리턴값이 리스트인 것을 원한다면 list(dict.keys())를 사용해야 한다.
list(dict.keys())


# values()
dict ={a:1, b:2}

dict.values()
>> dict_values(['1','1'])
# values 도 동일하게 dict_values 객체를 리턴한다.
# 동일하게 리스트를 원한다면 list로 감싸주면 된다 !

# items()
# -> key, value를 쌍으로 묶은 값을 dict_items 객체로 리턴.
dict ={a:1, b:2}
dict.items()
>> dict_items([('a':'1'), ('b':'2')])

# in : 딕셔너리 안에 key가 있는 지 조회
dict ={a:1, b:2}

dict in a
>> True

# get : Key로 Value 값 얻기 
dict.get('key')

dict ={a:1, b:2}
dict.get('a')
>> '1'

# clear : Key, Value 모두 지우기
dict ={a:1, b:2}

dict.clear()
dict
>> {} # 딕셔너리가 비었을 때 빈 중괄호를 리턴함.
```



### 참조 사이트
[딕셔너리 문법정리!](https://wikidocs.net/16)<br>
[최빈값 풀이!]()