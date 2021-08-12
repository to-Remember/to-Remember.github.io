---  
layout: post  
title:  "파이썬(19)_모니터_재고관리_프로그램_class_vo_dao_service"  
subtitle:   "재고관리, 프로그램, 클래스, vo, dao, service"  
categories: Python  
tags: Blog Python  
comments: true  
---  

**바로가기**
[모니터 재고관리 프로그램 - 기초](#방법1)
[모니터 재고관리 프로그램 - 심화](#방법2)


- **클래스**:        
int, float, str..와 같은 기본 타입으로 객체를 표현하는 것이 어렵다.        
따라서 객체 표현 가능한 데이터타입을 정의한다.

- **멤버변수**:     
다른 메서드에서도 만들 수 있지만          
호출 순서에 따라 에러가 발생할 수 있으므로            
멤버변수는 생성자에서 정의하는 것이 좋다.


> class Test:      
 
>>   def setData(self, a, b):
        self.a = a
        self.b = b
        
>>   def printData(self):
        print('a:', self.a)
        print('b:', self.b)
        
# 모니터 재고 관리 프로그램

# 방법1

- 모델명, 가격, 수량, 크기             
- 클래스 정의. 파이썬의 모든 클래스는 자동으로 object클래스를 상속받는다.           
- 따라서 object가 가지고 있는 모든 멤버변수와 메서드를 자동으로 상속받는다.         
- 그 중 하나가 __str__():  -> 객체를 설명하는 문자열을 반환한다.           



~~~python
class Monitor:

    #생성자. 객체 초기화하는 함수. 멤버변수 정의 및 초기화.
    #self:현재 객체 참조값. 모든 메서드는 첫번째 파라메터가 self다
    #멤버변수:객체소속의 변수. self.변수
    
    def __init__(self, model='', price=0, amount=0, size=0):
        self.model = model
        self.price = price
        self.amount = amount
        self.size = size

    #메서드 오버라이딩 -> 상속받은 메서드를 수정해서 사용
    def __str__(self):  #객체 설명 메서드로 object로부터 상속받았다.
        return 'model:'+self.model+' / price:'+str(self.price)+' / amount:'+str(self.amount)+' / size:'+str(self.size)


def main():
    monitors = []  #방이 없는 상태
    monitors.append(Monitor('s2440', 1500, 5, 27))
    monitors.append(Monitor('s2455', 2500, 5, 30))
    monitors.append(Monitor('s3440', 4500, 8, 30))

    for i in range(0, 3):
        print(monitors[i])

    for m in monitors:
        print(m)

main()
~~~

# 방법2

- **Dao + Service** - 기능 및 저장 작업         
- 등록: 모니터 정보를 입력받는다 -> Monitor 객체 생성 -> 리스트에 추가                 
- 검색: 검색할 제품의 모델명을 입력받는다 -> 리스트의 객체들을 하나씩 꺼내서 비교 -> 찾은 결과 반환              
- 전체출력: 리스트의 모든 객체 출력              

~~~python
#VO
class Monitor:
    def __init__(self, model='', price=0, amount=0, size=0):
        self.model = model
        self.price = price
        self.amount = amount
        self.size = size

    def __str__(self):
        return 'model:'+self.model+' / price:'+str(self.price)+' / amount:'+str(self.amount)+' / size:'+str(self.size)

#Dao + Service
#멤버변수:
class MonitorService:
    def __init__(self):
        self.monitors = []  #이 객체의 다수 메서드가 사용하는 값. 멤버 변수는 클래스 안에서 전역으로 사용하는 변수

    def addMonitor(self):  #새 모니터 등록. 모니터 데이터를 입력.
        #모니터의 모델명, 가격, 수량, 크기를 키보드로 입력받아 Monitor 객체 생성
        #생성한 객체를 리스트에 추가
        m = input('model:')        #새 모니터 모델 입력
        p = int(input('price:'))   #새 모니터 가격 입력
        a = int(input('amount:'))  #새 모니터 수량 입력
        s = int(input('size:'))   #새 모니터 크기 입력
        mo = Monitor(m, p, a, s)    #방금 입력받은 데이터를 묶어서 Monitor 객체 생성
        self.monitors.append(mo)    #생성한 객체를 리스트에 추가

    #모델명을 파라메터로 받아서 검색하여 검색된 객체 반환
    def getMonitor(self, model):
        #리스트 요소 하나씩 꺼내서 모델명 파라메터와 같은 제품 있으면 반환. 없으면 None 반환
        for i in self.monitors:
            if i.model == model:
                return i    #검색된 객체 반환

    def printMonitor(self):#모델명 입력받아서 똑같은 모니터 객체 찾아서 출력
        # 모델명 입력받아 지역변수에 저장
        name = input('검색할 모델명:')
        mo = self.getMonitor(name)
        if mo==None:
            print('없는 모델명')
        else:
            print(mo)

    def editMonitor(self):
        #수정할 제품 모델명입력받아서 지역변수에 저장
        #제품 검색해서 그 객체를 지역변수에 저장/ 검색했는데 없으면 여기서 종료
        #새 가격과 새 수량을 입력받아서 이 새정보로 객체를 변경
        name = input('수정할 모델명:')
        mo = self.getMonitor(name)
        if mo == None:
            print('없는 모델명. 수정 취소')
        else:
            mo.price = int(input('new price:'))
            mo.amount = int(input('new amount:'))

    def delMonitor(self):
        name = input('삭제할 모델명:')
        mo = self.getMonitor(name)
        if mo == None:
            print('없는 모델명. 삭제 취소')
        else:
            self.monitors.remove(mo)

    def printAll(self):
        for i in self.monitors:
            print(i)

#메뉴 클래스는 메뉴 돌려줄 메서드 하나만 있으면 된다.
#메뉴에서 기능을 선택해서 실행하려면 기능을 제공해주는 서비스 객체가 필요하다. MonitorService를 멤버변수로 생성한다.
class Menu:
    def __init__(self):
        self.service = MonitorService()

    def run(self):
        while True:
            m = int(input('1.모니터등록 2.검색 3.수정 4.삭제 5.전체출력 6.종료'))
            if m==1:
                self.service.addMonitor()
            elif m==2:
                self.service.printMonitor()
            elif m==3:
                self.service.editMonitor()
            elif m==4:
                self.service.delMonitor()
            elif m==5:
                self.service.printAll()
            elif m==6:
                break

def main():
    m = Menu()
    m.run()

main()
~~~