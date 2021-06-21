---  
layout: post  
title:  "파이썬(15)_클래스_예제_주소록_다양한형태의멤버변수_포함관계"  
subtitle:   "class, address book, class, member variables type"  
categories: Blog  
tags: Blog python     
comments: true  
---  

**바로가기**       
[다양한 형태의 멤버변수](#다양한-형태의-멤버변수)          
[포함관계](#포함관계)           

# 객체 지향 프로그래밍

- 순차적프로그래밍은 시간의 흐름 순서대로 코드를,     
객체지향 프로그래밍은 객체를 중심으로 개발한다.     
- 객체를 정의하고 객체와 객체 사이의 관계를 정의하는 방식으로 프로그래밍 한다.     
- 객체: 세상을 프로그램으로 모델링할대 모델링의 대상이 되는 사람이나 사물, 개념.     


# 주소록 만들기       

주소록 만들기 기초 예제     
심화 예제는 다음 글에서 볼 수 있다.     
- Member 클래스 정의      
- 멤버변수:      
id, pwd, name, email      
- 기능:      
멤버변수 출력      

~~~python
class Book: #Book이라는 이름의 타입을 정의

    def __init__(self, id, pwd, name='홍길동', email='gildong@hong'):
        self.id = id
        self.pwd = pwd
        self.name = name
        self.email = email

    def printBook(self):
        print('id:', self.id)
        print('pwd:', self.pwd)
        print('name:', self.name)
        print('email:', self.email)

def main():

    b1 = Book('aaa', '1111', 'a', 'a@a')
    b1.printBook()

    b2 = Book(id='bbb', pwd='2222', name='b', email='b@b')
    b2.printBook()

    b3 = Book('ccc', '3333')
    b3.printBook()

    b4 = b3
    b4.name = '가나다'
    b4.email = '가나다@email.com'
    b4.printBook()
    b3.printBook()

main()
~~~

# 다양한 형태의 멤버변수

다음의 예제로 다양한 형태의 멤버변수를 살펴볼 수 있다.

~~~python
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def printPoint(self):
        print('좌표:(',self.x,' , ', self.y,')')

class Test:
    def __init__(self):
        self.num = 0       #정수
        self.s = ''         #문자열
        self.arr = []       #리스트
        self.point = Point()   #객체. 포함관계:클래스타입의 멤버변수 / 관계(포함관계-has a, 상속관계-is a)

    def printData(self):
        print('num:', self.num)
        print('s:', self.s)
        print('arr:', self.arr)
        #self.point.x = 20
        #self.point.y = 30
        self.point.printPoint()

def main():
    t1 = Test()#객체 생성
    t1.num = 10
    t1.s = 'hello class'
    t1.arr.append(1)
    t1.arr.append(2)
    t1.arr.append(3)
    t1.point.x = 20
    t1.point.y = 30
    #t1.point = Point(3,4)
    t1.printData()

main()
~~~

# 포함관계

다음의 예제로 포함관계를 살펴볼 수 있다.

~~~python
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def printPoint(self):
        print('좌표:(',self.x,' , ', self.y,')')

class Test:
    def __init__(self):
        self.p = Point()   #None 상수
        self.num = 0    #int 값

def main():
    t1 = Test() #Test 객체 생성 => 메모리 할당. 생성자를 호출해야 객체 메모리를 할당받는다
    t1.num = 10
    t1.p.x = 10
    t1.p.y = 20
    t1.p.printPoint()

main()
~~~
