---
layout: post
title: "[Algorithm] Lv1. 숫자 짝꿍((programmers)"
tags: [Algorithm, Python]
date: 2023-08-23 10:31
# last_modified_at: 2023-07-07 14:29
categories : [Algorithm]
toc:  true
toc_label: "숫자 짝꿍"
---

## Intro
> 프로그래머스 Lv1. 문제인 숫자 짝꿍 문제에 대해 풀이하고자 합니다.

## 문제
![img](https://user-images.githubusercontent.com/112313165/262611391-40d428f1-d7e4-4c87-abf1-9c572c35a45a.png)

## 입출력 예시
![img](https://user-images.githubusercontent.com/112313165/262611438-da3eadf7-8089-4d62-b80e-e02fe1b3742b.png)

## 🥸 나의 접근 방법(오답)
1.  <span style ="color:#1E90FF">x_dict, y_dict에 for 반복문을 사용하여 2개의 딕셔너리를 제작한다.</span>
      - dict.get()을 사용하여 키 값이 존재하지 않을 경우 1을 넣어주고, 존재하는 경우 증감처리.
2.  <span style ="color:#1E90FF">for 반복문을 사용하여 x_dict.keys() 를 통해 key를 하나씩 꺼내어 key가 y_dict에 존재하는 지 파악</span>
       - <span style ="color:#FF6347">존재하는 경우</span> → 해당 문자열 * 공통횟수(min을 사용)의 문자열을 answer에 증감하여 처리. (문제에서 제시한 0만 존재하는 경우는 "0"으로 출력해야 하기에 여기서 처리하였음.)
       -  <span style ="color:#FF6347">존재하지 않는 경우</span> → 별도의 if문을 사용하여 ‘-1’ 문자열을 return.

### 문제점(테스트 결과: 6~15 실패)
1. 반례
- solution(100, 100) 으로 진행했을 때 0에 대한 처리가 되지 않았음. (출력이 100이 되야 하는데 위 접근방법으로 진행 시 10이 출력 되었음.)
2. 문제 해결과정
- 0만 존재하는 경우를 처리하는 부분을 별도로 분리하였음. (분기가 많아짐에 따라 코드가 복잡해지는 현상 해결)
- <span style ="color:#FF6347">변경 전 코드</span>
    ```python
    for i in x_dict.keys():
        # key가 y_dict에 존재할 경우 & 0이 아닌 경우
        if i in y_dict and i != '0':
                        # min 사용 이유 : x_dict, y_dict에서 적은 횟수가 공통횟수이기 때문에 사용.
            answer += str(str(i) * min(x_dict[i], y_dict[i]))
                # 존재하면서 & 0인 경우 (0인 경우는 1번만 더해야 함.)
        elif i in y_dict and i == '0':
            answer += str(i)
        # 내림차순 정렬하기.
        answer = ''.join(sorted(list(answer),reverse=True))

    # key가 y_dict에 존재하지 않을 경우 -1
    if answer == '':
        answer = '-1'
    ``` 

- <span style ="color:#FF6347">변경 후 코드</span>
    ```python
    for x in x_dict.keys():
        if x in y_dict:
            x = str(x)
            iternum = min(x_dict[x], y_dict[x])
            answer += x * iternum
        answer = "".join(sorted(list(answer), reverse=True))

        

    # # key가 y_dict에 존재하지 않을 경우 -1
    if answer == '':
        return '-1'
    elif len(answer) == answer.count("0"):
        return '0'
    else:
        return answer
    ```

## 🤩 다른 접근 방법(정답, 블로그 참고)
1. 기존 풀이는 X, Y에 있는 값들만 dict에 추가했지만, <span style ="color:#1E90FF">해당 풀이는 0~9까지의 모든 키에 0이라는 값을 넣어서 딕셔너리를 2개 제작함.</span>
2. X, Y 원소들을 하나씩 <span style ="color:#1E90FF">dict[key] 문법을 사용하여 증감처리.</span>
3. <span style ="color:#1E90FF">정렬을 사용하지 않고, range(9,-1,-1)을 사용</span>하여 문제에서 제시하는 가장 큰 정수를 만든다.


## ❌ 오답 코드
```python
def solution(X, Y):

	x_dict = {}
	y_dict = {}
	
	  for i in X:
	      # 존재하지 않을 경우 1을 넣어줌.
      if x_dict.get(i) == None:
          x_dict[i] = 1
      else:
          # 존재할 경우 증감처리
          x_dict[i] += 1
	
	  for i in Y:
	      # 존재하지 않을 경우 1을 넣어줌.
	      if y_dict.get(i) == None:
	          y_dict[i] = 1
	      else:
	          # 존재할 경우 증감처리
	          y_dict[i] += 1
	  # print(x_dict.keys()

		for i in x_dict.keys():
        # key가 y_dict에 존재할 경우 & 0이 아닌 경우
        if i in y_dict and i != '0':
						# min 사용 이유 : x_dict, y_dict에서 적은 횟수가 공통횟수이기 때문에 사용.
            answer += str(str(i) * min(x_dict[i], y_dict[i]))
				# 존재하면서 & 0인 경우 (0인 경우는 1번만 더해야 함.)
        elif i in y_dict and i == '0':
            answer += str(i)
        # 내림차순 정렬하기.
        answer = ''.join(sorted(list(answer),reverse=True))

    # key가 y_dict에 존재하지 않을 경우 -1
    if answer == '':
        answer = '-1'
    
    return answer
```

## ⭕️ 정답 코드1(내가 생각한 풀이)
```python
def solution(X, Y):
    x_dict = {}
    y_dict = {}
    answer = ''
    for i in X:
        # 존재하지 않을 경우 1을 넣어줌.
        if x_dict.get(i) == None:
            x_dict[i] = 1
        else:
            # 존재할 경우 증감처리
            x_dict[i] += 1

    for i in Y:
        # 존재하지 않을 경우 1을 넣어줌.
        if y_dict.get(i) == None:
            y_dict[i] = 1
        else:
            # 존재할 경우 증감처리
            y_dict[i] += 1
    for x in x_dict.keys():
        if x in y_dict:
            x = str(x)
            iternum = min(x_dict[x], y_dict[x])
            answer += x * iternum
        answer = "".join(sorted(list(answer), reverse=True))

        

    # # key가 y_dict에 존재하지 않을 경우 -1
    if answer == '':
        return '-1'
    elif len(answer) == answer.count("0"):
        return '0'
    else:
        return answer
```



## ⭕️ 정답 코드2(블로그 풀이)
```python
def solution(X, Y):
    answer = ''
    x_dict = {str(i) : 0 for i in range(10)}
    y_dict = {str(i) : 0 for i in range(10)}

    for x in X:
        x_dict[x] += 1

    for y in Y:
        y_dict[y] += 1
    # 공통된 정수 제작
    for k in range(9, -1, -1):
        k = str(k)
        iternum = min(x_dict[k], y_dict[k]) # x_dict, y_dict에서 적은 횟수가 공통횟수이기 때문에 사용함.

        answer += k * iternum
        
    if answer == '': # 공백에 대한 처리(중복된 숫자가 없는 경우)
        return "-1"
    elif len(answer) == answer.count('0'): # 0에 대한 처리
        return '0'
    else:
        return answer
```


## 회고
1. 딕셔너리 문법에서 <span style ="color:#FF6347">dict[key],  dict.get() 의 차이를 기억하자.</span>
  - <span style ="color:#1E90FF">전자(dict[key])의 경우는</span> key가 없는 경우 KeyError가 발생하지만,<span style ="color:#1E90FF"> 후자(get)는</span> None이 출력된다. 또한 get(dict, "디폴트 값")을 사용할 수 있다.
2. 분기를 할 때 굳이 한 번에 and 절을 추가하려 하지 말고, 다른 부분에서 처리할 수 있는 방법도 생각해보자.
3. 다른 사람 풀이를 보면, 정렬을 사용하는 대신 문제에서 k범위(0≤K≤9)를 제시한 것을  이용하였다. <span style ="color:#FF6347">문제를 더 확인하고 범위를 이용하도록 풀어보자.</span>



## 참조 사이트
[숫자 짝꿍 풀이!](https://chan-lab.tistory.com/36)<br>


