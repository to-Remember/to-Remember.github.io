---  
layout: post  
title:  "파이썬(18)_정적멤버변수_정적메서드_활용법_private멤버변수"  
subtitle:   "정적멤버, 변수, 메서드, private멤버변수 "  
categories: Blog  
tags: Blog python     
comments: true  
---  

파이썬 클래스 특징인 정적멤버변수 및 정적메서드를 살펴볼 것이다. 
 
# 정적멤버          

- **정적멤버 변수**: 정적메모리에 저장. 이 클래스로 만든 모든 객체는 공용으로 사용한다.

~~~python
class Test:
    x = 0  #클래스 변수. 정적 멤버 변수. 공용으로 사용.
    def __init__(self):
        self.y = 0 #일반멤버변수 (앞에 self를 꼭 붙인다. 이 멤버변수는 self객체 소속)

    def printxy(self):
        print('x:',Test.x)
        print('y:',self.y)

def main():
    print(Test.x) #객체 생성 전에도 사용 가능하다. (메모리 특징)
    #print(t1.y) #일반멤버변수는 객체 사용 전에 사용 불가하다.

    t1 = Test()
    Test.x+=1
    t1.y += 1
    t1.printxy()

    t2 = Test()
    Test.x += 1
    t2.y += 1
    t2.printxy()

    t3 = Test()
    Test.x += 1
    t3.y += 1
    t3.printxy()
~~~

# 정적메서드

- **정적메서드**: 클래스 안의 메서드이지만 self가 없다.         
  클래스 소속이기 때문에 객체생성 없이 클래스 이름으로 사용 가능하다.           

~~~python
class Test:
    x = 0

    def __init__(self):
        self.y = 0

    def method1(self):  #일반메서드 -> 클래스변수, 시점이 객체생성 이후이므로 클래스변수. 멤버변수 모두 사용 가능.
        print('method1: 멤버메서드')
        print('x:', Test.x)
        print('y:', self.y)

    def method2():  #정적메서드. 객체 생성전에 사용 가능하므로 일반 멤버 변수 사용 불가
        print('method2: 정적메서드')
        print('x:', Test.x)
        name = 'aaa'
        print()
        #print('y:', self.y)

    def method3(self):  #일반 메서드는 일반 메서드 호출도 가능. 정적메서드 호출도 가능.
        print('method3: 멤버메서드')
        self.method1()  #일반 메서드 호출
        Test.method2()  #정적 메서드 호출

    def method4():  #정적메서드. 객체 생성 전이므로 일반 메서드 호출 불가
        print('method4: 정적메서드')
        #self.method1()
        Test.method2()

def main():
    Test.method2()
    Test.method4()

    t1 = Test()
    t1.method1()
    t1.method3()

main()
~~~

# 정적변수 활용

> **Test 클래스**를 만들고          
객체가 생성되는 것을 **카운팅**하기             

~~~python
class Test:
    cnt = 0  #객체들이 공유해야 하는 값
    def __init__(self):
        Test.cnt += 1
        print(Test.cnt, '번째 객체 생성')

def main():
    for i in range(0,5):
        Test()

main()
~~~

# 정적메서드 활용

> **객체 생성없이** 클래스에 제공하는 메서드(기능)를 사용하는 클래스       
**API 기능** 제공


~~~python
class Math:
    __pi = 3.14  #변수앞에 __붙이면 private멤버변수이므로 클래스 밖에서 안 보인다
    PI = __pi  #우회적으로 파이썬에서 상수를 만드는 방법

    def circle(r):
        return r*r*Math.PI

    def rect(w, h):
        return w*h

def main():
    print('pi:', Math.PI)
    w = Math.circle(5)
    print('원의 넓이:', w)
    w = Math.rect(5, 10)
    print('사각형의 넓이:', w)

main()
~~~