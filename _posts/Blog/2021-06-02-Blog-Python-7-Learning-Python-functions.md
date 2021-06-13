---  
layout: post  
title:  "파이썬(7)_함수 사용방법"  
subtitle:   "함수정의, 함수호출 "  
categories: Blog  
tags: Blog python     
comments: true  
---  

## 함수
- 자주 사용하는 코드를 반복적으로 작성하지 않고    
모듈화하여 필요할 때 호출해서 반복 사용하는 것.   

### 함수 사용방법:

__1. 함수를 정의한다.__    
- def함수명(파라메터):    
  실행문1    
  실행문2    


### 함수 정의
~~~python
def hello():
    print('hello')

def add(x, y): #x, y --> 파라미터(매개변수)
    return x+y
~~~

__2. 함수를 호출한다.__

- 이름을 불러준다.    
만약 함수에 파라메터가 있다면 호출시 그 값을 불러줘야 한다.    
add(1,2) #add()함수호출    
함수를 호출하면 그 함수로 점프한다.    

### 함수호출
~~~python
hello()
res = add(1,2) #호출 시 파라미터에 넣어주는 값을 아규먼트(인자)
print(res)
~~~

다음의 예제가 이해하는 데 도움이 될 것이다.
~~~python
def f1():
    print('파라미터, 리턴값 없는 함수')

def f2(num):
    print('입력받은 숫자:', num)

def f3(name, age):
    print('당신의 이름은:', name)
    print('당신의 나이는:', age)


def f4(name, age):
    msg = '당신의 이름은:'+name+', 당신의 나이는:'+str(age)
    return msg

def f5(name, age):
    return name, age  #리턴값이 여러개면 하나의 튜플로 반환된다.

f1()
f2(3)
f3('aaa', 12)
s = f4('aaa', 12)
print(s)
#n, a = f5('bbb', 13)
#print(n, ':', a)
t = f5('bbb', 13) #t는 튜플
print(type(t))
print('name:',t[0], ', age:',t[1])
~~~