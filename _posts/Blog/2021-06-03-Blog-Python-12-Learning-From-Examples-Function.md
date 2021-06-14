---  
layout: post  
title:  "파이썬(12)_예제_함수"  
subtitle:   "함수예제_정의_호출"  
categories: Blog  
tags: Blog python     
comments: true  
---  

#### 함수 예제
1. 이름이 printName이고 파라미터로 문자열하나를 받아서 파라미터값을 출력하는 함수를 정의하고 호출해라. 함수 리턴값 없음     

2. 파라미터로 숫자 3개를 받고, 이중 가장 큰 값을 반환해라. 이름은 maxNum 함수로 정의 및 호출해라. 

3. 파라미터로 리스트하나를 받아서 리스트에 담긴 숫자 모두의 합을 구하여 반환하는 함수를 정의 및 호출해라. 함수 이름은 sumNum     

4. 파라미터로 문자열하나 숫자하나를 받는 이름이 f1인 함수를 정의해라. 호출시 파라미터의 순서가 바뀌어도 동작되도록 정의 및 호출해라. 리턴값은 없음     

5. 위 f1함수 파라미터의 기본값을 설정하시오. 문자열 파라미터의 기본값은 'aaa', 숫자 파라미터의 기본값은 0 이다     

~~~python
# 1

#함수정의
def printName(x):
    print(x)

#함수호출
printName('asdf')

# 2

def maxNum(n1, n2, n3):
    if n1>=n2:
        m = n1
    else:
        m = n2
    if m < n3:
        m = n3
    return m

max_num = maxNum(7,4,9)
print('max_num:', max_num)

# 3

def sumNum(arr):
    s = 0
    for i in arr:
        s+=i
    return s

list_sum = sumNum([1,2,3,4,5])
print('list_sum:', list_sum)

# 4

def f1(s, n):  #s:문자열, n:숫자
    print('s:', s)
    print('n:', n+4)

#f1(10, 'aads')
f1(n=10, s='asdf')  #키워드 인자:각 아규먼트가 어느 파라미터변수로 저장될지 지정. 순서 바꿔도 잘됨

# 5
def f1(s='aaa', n=0):  #s:문자열, n:숫자
    print('s:', s)
    print('n:', n+4)

f1('asd', 123)
f1()#기본값을 지정한 파라미터는 호출시 값 할당을 생략가능

#파라미터의 기본값이 지정된것과 지정되지 않은것을 섞어서 쓸때 순서가 중요하다. 
#기본값 없는 파라미터가 먼저 정의되어야 한다.
def f1(c, a=1, b=2):
    print(c, a, b)

f1(1)
f1(1,2)
~~~

