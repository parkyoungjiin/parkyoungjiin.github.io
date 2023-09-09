---
layout: post
title: "[Algorithm] Lv1. 로또 최고 순위, 최저 순위((programmers)"
tags: [Algorithm, Python]
date: 2023-09-09 10:31
# last_modified_at: 2023-07-07 14:29
categories : [Algorithm]
toc:  true
toc_label: "로또 최고 순위, 최저 순위"
---

## Intro
> 프로그래머스 Lv1. 문제인 로또 최고 최저순위 문제를 풀다가 계속 코드가 깔끔하지 못하고 쓸데없는 분기문을 작성하는 것 같아서 기억하고자 포스팅한다.

## 문제

![img](https://user-images.githubusercontent.com/112313165/266749313-f7a51184-7223-44ca-96f4-ef21eb6b05de.png)
![img](https://user-images.githubusercontent.com/112313165/266749317-7616bc01-3313-4d15-8b3f-5da869a0cc9e.png)

---
## 입출력 예시

![img](https://user-images.githubusercontent.com/112313165/266749318-fba60988-c81a-4cbd-b05a-26022730cefc.png)

---
## 🥸 나의 접근 방법
1. 로또 맞춘 개수에 따른 등수를 dict 선언한다.
2. lottos 번호를 하나씩 꺼내서 0이 아닌 숫자 중 로또 당첨 번호일 경우 맞춘 개수 변수에 증감을 진행한다. 0이라면 0을 세는 변수에 증감을 진행한다.
3. 0이 있을 떄 최고 순위는 맞춘 개수 + 0의 개수가 되며, 최저 순위는 맞춘 개수가 된다.
4. 0이 한 개 이상인 경우 맞춘개수 + 0의 개수로 dict[key] = value 문법을 사용하여 answer에 최고 순위를 넣고, 최저 순위는 기존 맞춘 개수로 answer에 최저 순위를 넣었다.

---

## 🤩 다른 접근 방법(정답, 블로그 참고)
1. 기존 풀이와 다른 방법은 아니지만 리팩토링 할 부분이 있어서 적어본다.
   - 수정 부분
     - count 사용
       - 기존 코드에서 0의 개수를 else 절에서 카운트했는데, 굳이 else절에서 사용하지 않고도 count 내장 함수를 사용하여 해결이 가능하다.
     - if, else문 삭제
       - 0이 없다면 연산에서 달라지는 점이 없는데 굳이 if, else문을 사용하지 않았어도 됐다. (습관성으로 If, else문을 사용하였음.)



--- 
## ⭕️ 정답 코드1(나의 풀이)

```python
def solution(lottos, win_nums):
    answer = []
    # 알 수 없는 번호 = 0, 구매한 로또 번호 -> lottos
    # 순위
    # 1. 6개 모두 일치 1등, 5개 2등, ... , 2개 일치 5등, 그외 낙첨
    lotto_rank = {6:1, 5:2, 4:3, 3:4, 2:5, 1:6, 0:6}
    # 맞은 개수
    lotto_right_cnt, zero_cnt = 0, 0

    for i in lottos:
        if i != 0:
            if i in win_nums:
                lotto_right_cnt += 1
        else:
            zero_cnt += 1
    # 0이 한 개라도 있는 경우
    if zero_cnt > 0:
        lotto_high_cnt = lotto_right_cnt + zero_cnt
        answer.append(lotto_rank[lotto_high_cnt])
        answer.append(lotto_rank[lotto_right_cnt])
    else:
        answer.append(lotto_rank[lotto_right_cnt])
        answer.append(lotto_rank[lotto_right_cnt])

    return answer
```
---

## ⭕️ 정답 코드2(리팩토링 코드)

```python
def solution(lottos, win_nums):
    answer = []
    # 알 수 없는 번호 = 0, 구매한 로또 번호 -> lottos
    # 순위
    # 1. 6개 모두 일치 1등, 5개 2등, ... , 2개 일치 5등, 그외 낙첨
    lotto_rank = {6:1, 5:2, 4:3, 3:4, 2:5, 1:6, 0:6}
    # 맞은 개수
    lotto_right_cnt, zero_cnt = 0, lottos.count(0)
    # print(zero_cnt)
    for i in lottos:
        if i in win_nums:
            lotto_right_cnt += 1 
    return [lotto_rank[zero_cnt + lotto_right_cnt], lotto_rank[lotto_right_cnt]]
```
--- 

## 회고

1. <span style ="color:#FF6347">무언가를 세야 할 때 count 함수를  쓰도록 생각하자.</span>
2. 습관적으로 if, else문을 사용하는 것을 지양하자.




## 참조 사이트


