---  
layout: post  
title:  "파이썬(16)_클래스_예제_성적처리프로그램"  
subtitle:   "클래스, 성적처리프로그램, 3가지방법"  
categories: Blog  
tags: Blog python     
comments: true  
---  
# 성적처리 프로그램 만들기

**바로가기**         
[예제2](#예제2)       
[예제3](#예제3)        


# 예제1

~~~python
class Student:

    def __init__(self):
        self.name = ''
        self.num = 0
        self.kor = 0
        self.eng = 0
        self.math = 0
        self.total = 0
        self.avg = 0

    def setData(self, name, num, kor, eng, math):
        self.name = name
        self.num = num
        self.kor = kor
        self.eng = eng
        self.math = math

    def calc(self):
        self.total = self.kor + self.eng + self.math
        self.avg = self.total / 3

    def printData(self):
        print('name:', self.name)
        print('num:', self.num)
        print('kor:', self.kor)
        print('eng:', self.eng)
        print('math:', self.math)
        print('num:', self.num)
        print('total:', self.total)
        print('avg:', self.avg)

def main():
    #클래스 타입의 변수는 먼저 생성해야 사용 가능
    s1 = Student() #객체 생성
    s1.name = 'aaa'
    s1.num = 1
    s1.kor = 45
    s1.eng = 56
    s1.math = 67
    s1.calc()
    s1.printData()

main()
~~~
>실행 결과:     
>> name: aaa     
num: 1     
kor: 45     
eng: 56     
math: 67     
num: 1     
total: 168     
avg: 56.0      


# 예제2

~~~python
class Student:
    def __init__(self, name='', num=0, score=[]):
        self.name = name
        self.num = num
        self.score = score #국영수 총점 및 평균 담을 리스트

    def calc(self):
        for i in range(0,3):
            self.score[3] += self.score[i]

        self.score[4] = self.score[3] / 3

    def printInfo(self):
        print(self.name, end = '\t')
        print(self.num, end = '\t')
        for i in self.score:
            print(i, end = '\t')
        print()

def main():
    s1 = Student('AA', 1, [55,55,55,0,0]) #객체 생성, 메모리 할당, 메모리 초기화
    s1.calc()
    s1.printInfo()

    s2 = Student('BB', 2, [77,77,77,0,0])
    
main()
~~~

>실행 결과:     
>> AA	1	55	55	55	165	55.0	  


# 예제3

~~~python
class Score: #1명의 점수 정보만 다루는 타입
    def __init__(self, kor, eng, math): #멤버 변수는 점수와 관련된 국영수총평
        self.kor = kor
        self.eng = eng
        self.math = math
        #총점 평균 계산
        self.total = self.kor + self.eng + self.math
        self.avg = self.total / 3

    def printScore(self): #점수와 관련된 국영수총평 출력
        print(self.kor, end='\t')
        print(self.eng, end='\t')
        print(self.math, end='\t')
        print(self.total, end='\t')
        print(self.avg, end='\t')
        print()

class Student: #한 학생의 정보(score포함)를 갖는 클래스
    def __init__(self, name, num, score):
        self.name = name
        self.num = num
        self.score = score #score객체. 포함관계

    def printMember(self):
        print(self.name, end='\t')
        print(self.num, end='\t')
        self.score.printScore()

def main():
    sc1 = Score(77,77,77)
    s1 = Student('A', 1, sc1)
    s1.printMember()

    s1 = Student('B', 2, Score(99,99,99)) #즉석에서 생성해도 무방하다
    s1.printMember()

main()
~~~

>실행 결과:     
>> A	1	77	77	77	231	77.0	    
B	2	99	99	99	297	99.0      

