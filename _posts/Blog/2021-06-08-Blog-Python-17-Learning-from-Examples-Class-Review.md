---  
layout: post  
title:  "파이썬(17)_클래스_예제_주소록_그리고_DAO_Service_맛보기"  
subtitle:   "클래스, 복습, VO, DAO, Service"  
categories: Blog  
tags: Blog python     
comments: true  
---  

# 클래스 예제 살펴보기

- **예제(1):**  Person 사람, 이름, 나이 저장, 기능 출력하기        
- **예제(2):**  주소록 리스트 다루기          

> 첫 번째 예제는 두 가지 방법으로 살펴볼 것이다.       
방법1은 기본기를 다지기 위해 구성된 코드로 비교적 지저분하다.          
깔끔한 코드로 넘어가려면 **예제(1)-2** 로 바로가기 하면 된다.             

**바로가기**        
[예제(1)-2](#예제12)         
[예제(2)](#예제2)

# 예제(1)
<기본기 다지기 (코드 지저분)>
~~~python
class Person:
    def __init__(self): #생성자
        #멤버 변수 정의. 객체의 데이터를 담는 변수.
        self.name = ''
        self.age = 0

        #리스트라면 self.arr = [] 이렇게 초기화
        #객체타입(객체형)이면 self.point = None
        #물론 클래스는 타입을 안가려서 아무렇게 입력해도 되지만 위 형식을 지키는 것이 바람직

    #메서드. 클래스 안에 정의한 함수. 이 객체의 기능. 정보 출력
    #멤버변수는 항상 self를 붙이며, 이는 현재객체를 뜻한다(물론 self말고 다른 문자 입력 가능.이름은 기능이 없기에).
    #모든 메서드의 첫번째 파라미터는 현재 객체의 참조값이 자동으로 전달된다.
    def printPerson(self):
        #name = 'xxx' -> 이건 지역변수
        print('name:', self.name)
        print('age:', self.age)

def main():
    p1 = Person() #생성자 호출은 -> 클래스명() -> 객체가 사용할 메모리 할당받아 참조값을 반환함.
    #반환받은 참조값을 변수 p1에 저장
    p1.name = 'Apple' #멤버 변수값 쓰기
    p1.age = '20' #멤버 변수값 쓰기
    
    #print(p1.name) #멤버 변수값 읽기
    #print(p1.age) #멤버 변수값 읽기
    #필요없는 코드. 출력하는 메소드를 이미 만들어놨기에
    
    p1.printPerson()

    p2 = Person()
    p2.name = 'Banana'
    p2.age = '7'
    
    #print(p2.name) #멤버 변수값 읽기
    #print(p2.age) #멤버 변수값 읽기

    p2.printPerson()


밑의 내용 추가 가능:
    persons = [] #밑의 리스트를 담을 객체를 생성한 것
    for i in range(0,3) #객체 3개 만들어서 루프 돌리기


main()
~~~

# 예제(1)-2
~~~python
class Person:
    def __init__(self, name='', age=0):  # 생성자
        # 멤버 변수 정의. 객체의 데이터를 담는 변수.
        self.name = name
        self.age = age

    def setData(self, name, age):
        self.name = name
        self.age = age

    def printPerson(self):
        name = 'xxx' #지역변수
        print('지역변수 name:', name)
        print('name:', self.name)
        print('age:', self.age)

def main():
    p1 = Person('aaa',12)  # 생성자 호출은 -> 클래스명() -> 객체가 사용할 메모리 할당받아 참조값을 반환
    p1.printPerson()

    p2 = Person()
    p2.printPerson()

main()
~~~

# 예제(3)
<DAO, Service 맛보기>
~~~python
#이름, 전화, 주소
#VO (멤버를 만든 클래스를 VO(Value Object 또는 DTO(Data Transfer Object)라고 한다.
class Member:
    def __init__(self,name='',tel='',address=''):
        self.name = name
        self.tel = tel
        self.address = address
        print()

    def printMember(self):
        print('name:',self.name)
        print('tel:',self.tel)
        print('address:',self.address)

# DAO(Database Access Object) : DB에 접근하는 객체.
# 일단 이 코드에선 DB대신 리스트를 사용할 것. 데이터 추가/검색/수정/삭제 기능을 구현하는 클래스

class MemDao: #저장소 관련 작업만 담당. (리스트 작업만 전담하고 있음) -> 추가 검색 수정 삭제
    def __init__(self):
        self.datas = []

    def insert(self, m):
        self.datas.append(m)

    def select(self, name):
        for i in self.datas:
            if i.name == name:
                return i #검색된 객체의 참조값 반환. 객체에 다이렉트로 접근 가능

    def selectAll(self):
        return self.datas

    #def update(self, m): #m에다가 수정할 사람의 이름, 새전화, 새주소
    #이건 DB랑 연동할 때 필요. 이후에 학습할 것

    def delete(self, m):
        self.datas.remove(m) #이건 값을 찾아서 삭제해주는 것.
        #del self.datas[idx] -> 이건 방 번호를 알아야 함. 따라서 현재 함수에 적합하지 않음.

# Service(비즈니스 로직을 구현하는 것) : 사용자에게 제공할 기능을 구현하는 클래스. 추가/검색/수정/삭제
class MemService:
    def __init__(self):
        self.dao = MemDao()

    def addMember(self):
        name = input('name:')
        tel = input('tel:')
        address = input('address:')
        m = Member(name, tel, address)
        self.dao.insert(m)

    def printMember(self):
        name = input('search name:')
        m = self.dao.select(name)
        if m == None:
            print('없는 이름')
        else:
            m.printMember()

    def printAll(self):
        datas = self.dao.selectAll()
        for i in datas:
            i.printMember()

    def editMember(self):
        name = input('수정할 사람 name:')
        m = self.dao.select(name)
        if m == None:
            print('없는 이름')
        else:
            m.tel = input('new tel:')
            m.address = input('new address:')

    def delMember(self):
        name = input('수정할 사람 name:')
        m = self.dao.select(name)
        if m == None:
            print('없는 이름')
        else:
            self.dao.delete(m)

class Menu:
    def __init__(self):
        self.service = MemService()

    def run(self):
        while True:
            menu = int(input('1.등록 2.검색 3.수정 4.삭제 5.전체출력 6.종료'))
            if menu == 1:
                self.service.addMember()
            elif menu == 2:
                self.service.printMember()
            elif menu == 3:
                self.service.editMember()
            elif menu == 4:
                self.service.delMember()
            elif menu == 5:
                self.service.printAll()
            elif menu == 6:
                break

def main():
    m = Menu()
    m.run()

main()
~~~
