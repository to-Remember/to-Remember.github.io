---  
layout: post  
title:  "파이썬(11)_전역변수_지역변수_함수종료return_재귀함수"  
subtitle:   "전역변수_지역변수__return_재귀함수"  
categories: Python  
tags: Blog Python     
comments: true  
---  
**바로가기**       
[함수종료 return](#함수종료-return)      
[재귀함수](#재귀함수)      

# 전역변수 및 지역변수

~~~python
a=10  #전역변수
def f1(param1):#param1:  #지역변수
    b = 20   #지역변수
    print('a:', a)  #전역변수 a
    print('param1:', param1)
    print('b:', b)

def f2():
    a=30  #새 지역변수 정의
    print('a:', a)
    #print(b)       #f1의 지역변수이므로 사용불가
    #print(param1)  #f1의 지역변수이므로 사용불가

def f3():
    global a
    a=50#전역변수 a변경
    print('a:', a)  #전역변수 출력
    #print('x:', x)  #x는 전역변수 이지만 호출 이후에 선언해서 안보인다

def main():
    f1(35)
    f2()
    f3()

main()

x = 100  #전역변수
~~~

# 함수종료 return

~~~python
def f1():
    while True:
        menu = input('숫자 입력하라. 멈추려면 0입력')
        print('입력값:', menu)
        if menu=='0':
            return  #함수종료. None 상수 반환. (None:아무값도 없다라는 의미의 상수)

def f2(name):
    return '당신의 이름은 '+name  #문자열 반환

def f3():
    print('test f3')  #함수에서 반환값이 없으면 자동으로 None이 반환된다.

def main():
    res = f1()
    print('f1의 리턴값:', res)
    res = f2('aaa')
    print('f2의 리턴값:', res)
    res = f3()
    print('f3의 리턴값:', res)

main()
~~~

# 재귀함수

- 자신을 호출하는 함수이다.     
- 반복동작을 짧게 구현할 수 있는 장점이 있다.     
- 그러나 스택 사용량이 늘어나서 스택 오버플로우 문제가 발생할 수 있다.     
- 대부분 재귀는 루프로 대체 가능하기 때문에 루프로 대체하는 것이 좋다.     

~~~python
#5! = 5*4*3*2*1
def fact(num):
    if num==1:
        return 1
    else:
        return num * fact(num-1)

def fact2(num):
    res = 1
    for i in range(1, num+1):
        res *= i
    return res

def fibo1(num):
    if num <= 2:
        return 1
    else:
        return fibo1(num-1)+fibo1(num-2)

def fibo2(cnt):
    i, j, k = 1, 1, 0
    for x in range(1, cnt+1):
        if x<3:
            print(1, end='\t')
        else:
            k = i+j
            print(k, end='\t')
            i = j
            j = k

def fibo3(cnt):
    res = [1,1]
    for i in range(2, cnt+1):
        res.append(res[i-2]+res[i-1])
    return res

def main():
    
    res = fibo3(50)
    print(res)
    
main()
~~~
