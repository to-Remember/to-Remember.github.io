---  
layout: post  
title:  "파이썬(8)_함수 예제"  
subtitle:   "구구단, 약수/최소값/최대값 구하기 "  
categories: Blog  
tags: Blog python     
comments: true  
---  

- [총합 구하기] (총합-구하기)
- [약수 구하기] (약수-구하기)
- [최소값 구하기] (최소값-구하기)
- [최대값 구하기] (최대값-구하기)
- [구구단] (구구단)
- [계산기 만들기] (계산기-만들기)

##### 총합 구하기

~~~python
def sumList(x):
    s = 0
    for i in x:
        s += i
    return s

def main():
    a = [1, 2, 3, 4, 5]
    k = sumList(a)
    print('총합:', k)

    b = [9, 8, 7, 6, 6, 5, 4]
    k = sumList(b)
    print('총합:', k)

main()
~~~

##### 약수 구하기

~~~python
#파라메터로 숫자를 받아서 그 숫자의 약수 출력. 리턴값 없음
def 약수(num):
    print(num, '의 약수: ', end='')
    for i in range(1, num+1):
        if num%i == 0:
            print(i, end=', ')
    print()

#x = int(input('num:'))
#약수(x)

def 약수2(num):
    res = []
    for i in range(1, num+1):
        if num%i == 0:
            res.append(i)
    return res

def 약수프린트(data):
    print(data[len(data)-1], '의 약수: ', end='')
    for i in data:
        print(i, end=', ')
    print()

x = int(input('num:'))
d = 약수2(x)
약수프린트(d)
~~~

##### 최소값 구하기

~~~python
def minList(x):
    m = x[0]  #첫 요소를 min값으로 초기화,  리스트 요소와 하나씩 비교하면서 더 작은 값을 만나면 바로 m으로 교체
    for i in x:
        if m > i:
            m = i
    return m

def main():
    a = [1, 2, 3, 4, 5]
    min = minList(a)
    print('min:', min)
    
    b = [9, 8, 7, 6, 3, 5, 4]
    min = minList(b)
    print('min:', min)

main()
~~~

##### 최대값 구하기

~~~python
def maxList(x):
    m = x[0]  #첫 요소를 max값으로 초기화,  리스트 요소와 하나씩 비교하면서 더 큰값을 만나면 바로 m으로 교체
    for i in x:
        if m < i:
            m = i
    return m

def main():
    a = [1, 2, 3, 4, 5]
    max = maxList(a)
    print('max:', max)

    b = [9, 8, 7, 6, 3, 5, 4]
    max = maxList(b)
    print('max:', max)

main()
~~~

##### 구구단

~~~python
def gugudan(dan):
    print('<',dan,'단>')
    for i in range(1, 10):
        print(dan,' * ', i, ' = ', dan*i)
        
for i in range(2, 10):
    gugudan(i)
~~~

##### 계산기 만들기

~~~python
def 더하기(a, b):#a, b:계산할 숫자 2개
    c=a+b
    return c

def 빼기(a, b):
    return a-b

def 곱하기(a, b):
    return a*b

def 나누기(a, b):#함수에서 아무값도 반환하지 않으면 None객체 전달됨
    if b!=0:
        return a/b


num1 = int(input('num1:'))#계산할 숫자1
num2 = int(input('num2:'))#계산할 숫자2
res = None  #계산 결과 담을 변수. None:값이 없다는 의미의 상수
op = input('op(+, -, *, /):')#연산자
if op=='+':
    res = 더하기(num1, num2)
elif op=='-':
    res = 빼기(num1, num2)
elif op=='*':
    res = 곱하기(num1, num2)
elif op=='/':
    res = 나누기(num1, num2)

if res == None:
    print('잘못된 수식')
else:
    print(num1, op, num2, '=', res)
~~~
