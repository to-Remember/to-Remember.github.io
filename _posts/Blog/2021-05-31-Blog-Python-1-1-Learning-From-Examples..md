---
layout: post
title:  "파이썬(1)_예제"
subtitle:   "합격/불합격, 짝수/홀수, 성인/성별 확인, 학점"
categories: Blog
tags: Blog python   
comments: true
---


## 예제

## if / else / elif 

##### 1. 합격/ 불합격 체크

- 입력한 값이 60보다 크거나 같으면 **합격**을 출력하라,
- 조건 불만족시 **불합격**을 출력하라.

~~~
score = int(input('점수'))
if score >= 60:
    print('합격')
else:
    print('불합격')
~~~


##### 2. 짝수/ 홀수 체크

- 수를 입력받는다
- 입력받은 수가 짝수일 경우 **짝수**를 출력하라.
- 입력받은 수가 홀수일 경우 **홀수**를 출력하라.

~~~
num = int(input('num:'))
if num % 2 == 0
    print('짝수')
else:
    print('홀수')
~~~

##### 3. 성인 여성 체크

- 20세 이상이며
- 여성일 경우 **입장**을 출력하라.
- 조건 불만족시 **성인 여성만 가능**을 출력하라.


~~~
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

~~~
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

#####  4. 점수(1-100) 입력받아 학점 출력

- A: 90-100
- B: 80-89
- C: 70-79
- D: 60-69
- F: 60미만


~~~
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

