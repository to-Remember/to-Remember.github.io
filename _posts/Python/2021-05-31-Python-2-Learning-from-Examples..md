---
layout: post
title:  "파이썬(2)_조건문_예제_합격불합격_짝수홀수_성별_학점"
subtitle:   "합격/불합격, 짝수/홀수, 성인/성별 확인, 학점출력"
categories: Python
tags: Blog Python   
comments: true
---


## 예제 바로가기
> [합격/불합격](합격--불합격-체크)     
[짝수/홀수](짝수--홀수-체크)     
[성인/성별](성인-여성-체크)     
[학점출력](점수-입력받아-학점-출력)     



## if / else / elif 

# 합격/ 불합격 체크

- 입력한 값이 60보다 크거나 같으면 **합격**을 출력하라,
- 조건 불만족시 **불합격**을 출력하라.

~~~python
score = int(input('점수'))
if score >= 60:
    print('합격')
else:
    print('불합격')
~~~


# 짝수/ 홀수 체크

- 수를 입력받는다
- 입력받은 수가 짝수일 경우 **짝수**를 출력하라.
- 입력받은 수가 홀수일 경우 **홀수**를 출력하라.

~~~python
num = int(input('num:'))
if num % 2 == 0
    print('짝수')
else:
    print('홀수')
~~~

# 성인 여성 체크

- 20세 이상이며
- 여성일 경우 **입장**을 출력하라.
- 조건 불만족시 **성인 여성만 가능**을 출력하라.


~~~python
(1)
age = int(input('나이:')
if age >= 20:
    gender = input('성별(여:f, 남:m):')
    if gender == 'f':
        print('입장')
    else:
        print('여성만 입장가능')
else:
    print('성인만 입장가능')
~~~

~~~python
(2)
age = int(input('나이:')
gender = input('성별(여:f, 남:m):')
if age >= 20 and gender == 'f':
    print('입장')
else:
    print('성인 여성만 가능')
else:
    print('성인만 입장가능')
~~~

# 점수 입력받아 학점 출력

- A: 90-100
- B: 80-89
- C: 70-79
- D: 60-69
- F: 60미만


~~~python
score = int(input('score(0-100):'))
if score < 0 or score > 100:
    print('잘못된 점수')
else:
    if score >= 90:
        print('A')
    elif score >= 80:
        print("B")
    elif score >= 70:
        print("C")
    elif score >= 60:
        print("D")
    else:
        print("F")
~~~

