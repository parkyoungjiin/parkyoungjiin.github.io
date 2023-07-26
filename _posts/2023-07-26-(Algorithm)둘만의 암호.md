---
layout: post
title: "[Algorithm]Lv1. 둘만의 암호(programmers)"
tags: [Algorithm, Python]
date: 2023-07-26 10:00
categories : [Algorithm]
toc:  true
toc_label: "배열 회전시키기"
---

## 문제
![img](https://user-images.githubusercontent.com/112313165/256148652-3d8ada4f-d094-4257-a57f-84261f32031d.png)

## 입출력 예시
![img](https://user-images.githubusercontent.com/112313165/256148677-60d571fd-7835-4d66-abfa-091eb5319c76.png)

## 🥸 나의 접근 방법(오답)
1. 알파벳 전체를 담은 문자열 alpha 변수를 선언한다 
2. skip 리스트를 별도로 만든다.
3. skip 리스트에 s + index를 했을 때 alpha변수에 있을 경우 +1을 해준다.


## 🤩 다른 접근 방법(정답)
1. 알파벳 전체를 담은 문자열 alpha 변수를 선언한다.
2. replace를 사용하여 skip할 문자를 제거한다. 
3. 나머지 연산자를 사용하여 "**skip에 있는 알파벳은 제외하고 건너뜁니다.**" 의 규칙을 준수하여 풀이함.


## ❌오답 코드
```python
def solution(s, skip, index):
    # skip은 제외할 인덱스번호, 
    answer = []
    alpha = "abcdefghijklmnopqrstuvwxyz"
    # print(len(alpha))
    skip_alpha = []
    # 스킵해야 할 인덱스 리스트 제작.
    for i in skip:
        skip_index = alpha.index(i)
        skip_alpha.append(skip_index)
    
    print("skip_alpha:", skip_alpha)

    # s의 요소들을 하나씩 꺼내서 인덱스를 계산하여 alpha에서 값을 가져올 것임.
    for i in s:
        s_index = alpha.index(i)
        s_index += index
        # s_index 범위 내에 skip_alpha가 있으면 +1을 해준다.
        for j in range(s_index-index, s_index):
            if j in skip_alpha:
                s_index += 1
        
        if s_index >= len(alpha):
            s_index -= len(alpha)
        
        
        answer.append(alpha[s_index])
    
        
    return print("".join(answer))
```

## ⭕️정답 코드(replace 사용)
```python
def solution(s, skip, index):
    alpha = "abcdefghijklmnopqrstuvwxyz"
    answer = ""

    for i in skip:
        if i in alpha:
            alpha = alpha.replace(i, "")

    for i in s:
        if i in alpha:
            s_index = (alpha.index(i) + index) % len(alpha)
            answer += alpha[s_index]
    return answer
```


## 회고
1. replace를 사용하여 스킵할 리스트 변수를 만들지 않아도 해결가능했다.
2. 나머지 연산자를 사용하여 z로 넘어갈 경우 a로 설정하였음.
    ```python
    # 오답 코드
    if s_index >= len(alpha):
        s_index -= len(alpha)

    # 개선한 코드
    s_index = (alpha.index(i) + index) % len(alpha)
    ```



## 참조 사이트
[둘만의 암호 풀이!](https://velog.io/@bjo6300/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%91%98%EB%A7%8C%EC%9D%98-%EC%95%94%ED%98%B8)<br>