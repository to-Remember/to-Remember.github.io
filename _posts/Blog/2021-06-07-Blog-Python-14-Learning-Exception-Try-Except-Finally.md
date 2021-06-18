---  
layout: post  
title:  "파이썬(14)_예외발생_예외처리_"  
subtitle:   "try, except, else, finally"  
categories: Blog  
tags: Blog python     
comments: true
---  

바로가기:     
[사용자정의 예외](#사용자정의-예외)


# 예외발생  
- 컴파일시 에러: 문법적 에러(한 예로 뒤에 점을 안찍는 행위)       
- 예외: 런타임시 문제 발생        
- 예외발생 -> 예외 객체를 생성해서 던진다. -> 프로그램이 예외객체를 맞으면 죽는다.     
# 예외처리     
- 프로그램이 예외객체를 맞았을 때 죽지않게 처리한다.     
- 파이썬에서 예외처리가 필수는 아니지만 프로그램의 안정성을 높이기 위해서 사용하는 것이 좋다     

# 예외처리 구문

**try - except구문**     
          
> try:     
----예외발생 예측     
----(예외발생 가능성 있는 것 여기다 넣기)     
----(만약 오류구문 있을 시 밑에 지문 실행 안되고 바로 except구문으로 넘어감)     
----(e.g.)res=3/0     
         
> except 예외명1 as e:  #as e는 발생한 예외 객체를 변수 e에 저장     
----예외처리작성     
    
> except 예외명2:     
----예외처리작성     
    
> except Exception as e: #모든 예외 객체를 받음     
----예외처리작성     
    
> else: #예외가 발생하지 않았을 때 실행되는 블록     
----실행문     
    
> finally: #무조건 실행되는 블록     
----실행문     


**try - except구문** 
~~~python
def main():
    print('프로그램 시작')
    arr = [1,2,3]
    try:
        #arr[3]=4
        #res = 3 / 0
        print('test1')
        res='aaa' + 1
        print('test2')
    except ZeroDivisionError as e:
        print(e)
    except TypeError as e:
        print(e)
    except Exception as e:
        print('예외가 발생했지만 위 except에서 잡지 못하면 여기로 온다')
    else:
        print('예외가 발생하지 않았음')
    finally:
        print('예외가 발생하건, 정상 실행되건 종료전 항상 실행되는 블록')

    print('프로그램 종료')

main()
~~~

# 사용자정의 예외

**1. 예외 클래스를 만든다.**           
파이선에 정의되지 않은 예외 클래스 쓰고 싶을 때 직접 만들어서 사용한다.      
class 예외클래스명(Exception):     
----ef__init__(self,msg): #생성자. 객체 초기화 함수. 사용할 에러 메시지 할당
--------self.msg = msg

**2. 예외 발생을 시킨다.**     
파이선이 인지하지 못하는 예외를 직접 발생시키고 싶을 때 사용한다.     
raise 예외객체 생성     

**3. 함수에서 예외가 발생시** 먼저 그 함수 안에서 예외처리 코드를 찾고 그것을 실행한다.     
코드가 없으면 해당 함수를 호출한 위치에서 예외처리 구문을 또 찾는다 (스택언롤링)       
코드가 있으면 그 예외처리 구문을 실행한다.        
없으면 다운. 프로그램 중단.          

~~~python
class NumError(Exception):
    def __init__(self, msg): #생성자. 객체 초기화 함수
        self.msg = msg

def f1(num): #5이하의 숫자만 가능. 5보다 큰 숫자를 받으면 심각한 발생
    if num > 5:
        raise NumError('num은 5보다 작거나 같아야 함')

    print(num)

def f2(mum):
    if not isinstance(num, int): #a의 타입이 type이냐? 맞으면 True, 아니면 False
        raise TypeError('num은 int이어야 함')
    return num+10

def main():
    try:
        f1(10)
        f1(4)
        f2('asdf')
    except NumError as e:
        print(e.msg)
    except TypeError as e:
        print(e)

main()
~~~


