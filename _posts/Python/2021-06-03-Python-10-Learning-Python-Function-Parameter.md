---  
layout: post  
title:  "파이썬(10)_파라미터_인자"  
subtitle:   "파라미터_(im)mutable_요구인자_키워드인자_가변인자"  
categories: Python  
tags: Blog Python
comments: true  
---  
**바로가기**    
[파라미터 mutable](#파라미터-mutable)     
[요구인자](#요구인자)    
[키워드인자](#키워드-인자)
[가변인자](#가변인자)


# 파라미터 immutable

- 함수의 파라메터로 immutable한 값 전달의 예     
immutable(값 변경 안되는 요소. 상수). int, str, float, bool, tuple     

~~~python
def f1(num, name):
    print('f1에서 변경전')
    print('num:', num)
    print('name:', name)
    num = 123
    name = 'asf'
    print('f1에서 변경후')
    print('num:', num)
    print('name:', name)

def main():
    num = 10
    name = 'aaa'
    print('main에서 변경전')
    print('num:', num)
    print('name:', name)
    f1(num, name)
    print('main에서 변경후')
    print('num:', num)
    print('name:', name)

main()
~~~

# 파라미터 mutable

- 함수의 파라메터로 mutable한 값 전달의 예     
mutable: 변경되는 값. 리스트, 셋, dictionary     

~~~python
def f1(arr):
    print('f1안에서 변경전: ', arr)
    arr[0]=100
    print('f1안에서 변경후: ', arr)

def main():
    x = [1,2,3,4,5]
    print('main 변경전: ', x)
    f1(x)
    print('main 변경후: ', x)

main()
~~~

# 요구인자

~~~python
def f1(name, tel, age):
    print('name:', name)
    print('tel:', tel)
    print('10년 후 age:', age+10)

def main():
    n = 'aaa'
    t = '1234'
    a = 12

    f1(n, t, a)
    #f1(a, n, t)  ---> 순서대로 안할시 에러

main()
~~~

# 키워드 인자

~~~python
def f1(name, tel, age=5):  #age=5: 아규먼트 기본값
    print('name:', name)
    print('tel:', tel)
    print('10년 후 age:', age+10)

def main():
    n = 'aaa'
    t = '1234'
    a = 12

    #키워드 인자
    f1(tel=t, age=a, name=n)
    f1(n, t)
main()
~~~

# 가변인자

~~~python
def f1(*x):  #가변인자. 튜플로 받아온다
    print('함수시작')
    for i in x:
        print(i)
    print('함수끝')

def add(*nums):
    s = 0
    for i in nums:
        s+=i
    return s

def main():
    f1()
    f1('aaa', 'bbb')
    f1('ccc', 'ddd', 'eee', 'fff')

    s = add(1,2,3)
    print('add(1,2,3):', s)
    s = add(1, 2, 3, 4, 5)
    print('add(1,2,3, 4, 5):', s)

main()
~~~
