---  
layout: post  
title:  "파이썬(5)_리스트_예제_최대값_최소값_성적처리프로그램"  
subtitle:   "최대값, 최소값, 성적처리 프로그램"  
categories: Python  
tags: Blog Python     
comments: true  
---  
## 리스트 예제

> 1. 숫자 10개 입력받아 저장하시오.   
> 2. 요소 중 최대값을 찾으시오.   
> 3. 요소 중 최소값을 찾으시오.


~~~python
a = []  
for i in range(0, 10):  ---> 10회 반복을 위해
    a.append(int(input('num:')))

print(a)

max = a[0]  ---> max:최대값을 담을 변수
for i in a:
    if max<i:  ---> i는 최대값
        max = i
print('max:', max)

min = a[0]  ---> min:최소값을 담을 변수
for i in a:
    if min > i:  ---> i는 최소값
        min = i
print('min:', min)

s_num = int(input("검색할 숫자:"))
flag = True  ---> 찾았는지의 여부를 표시해준다. 못찾았을때 True, 찾았을때 False.
for i in range(0, len(a)):
    if a[i]==s_num:
        print(i, '번째 방에 있음')
        flag = False
        break
if flag:  ---> flag가 True면 if문은 True가 되므로 실행
    print('not found')
~~~

> List를 이용하여 성적처리 프로그램을 만드시오.   
학생의 번호, 국어, 영어, 수학 점수를 입력받고, 각 학생의 총점, 평균을 계산하여 결과를 출력하시오.   
*학생은 총 3명

~~~python
person = [0] * 7 

title = ['번호', '이름', '국어', '영어', '수학', '총점', '평균']
for i in range(0, 5):  ---> 입력받아야 하는 값들
    if i==1:
        person[i] = input(title[i])
    else:
        person[i] = int(input(title[i]))
        if i!=0:
            person[5] += person[i]  ---> 총점

person[6]=person[5]/3  ---> 평균

print(title)  ---> 타이틀과 그에 맞는 각 항목들이 출력되게끔
for i in score:
    for j in i:
        print(j, end=', ')
    print()
~~~
