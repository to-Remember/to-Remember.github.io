---  
layout: post  
title:  "파이썬(6)_셋_튜플_딕셔너리"  
subtitle:   "셋, 집합, 튜플, 딕셔너리 "  
categories: Blog  
tags: Blog python     
comments: true  
---  
## 셋

- 셋(set): 집합   
- 요소 중복이 허용되지 않는다.   
- 순서가 없다. 즉, 인덱스가 없다   
- 요소 변경이 불가하며 immutable 이어야 한다.   
- 셋 자체는 변경이 가능하다. (요소 추가/ 삭제 가능)


### 셋 생성
~~~python
s = {1,2,3}
print(s)
print(type(s))  
--> <class 'set'>

s = {}  #주의!칸이 비어있으면 딕셔너리가 된다.
print(type(s))  
--> <class 'dict'> 인것을 확인할 수 있다.

s = {1,2,3} #중복되는 값을 넣어보자.
for i in s:
    print(i)
결과:  #위와 중복된 값이 있으면 에러 없이 저장하지 않는다는 것을 알 수 있다.
1
2
3
~~~
위에다가   
#s={1,2,{3,4,5]}   
#print(s)   
이렇게 덧붙이는 것은 불가하다.   
셋은 변경가능한 요소를 가질 수 없기 때문이다.

### 셋 요소 추가, 삭제
다음과 같이 셋에 요소를 추가할 수 있다.
~~~python
s = {1,2,3}
s.add('bbb')  #요소 한개 추가
print(s)  --> 결과: {1, 2, 3, 'bbb'}

a = [5,6,7]
s.update(a)  #요소 여러개 추가
print(s)  --> 결과: {1, 2, 3, 5, 6, 7, 'bbb'}

#s.remove('aaa')  --> 없는 요소 삭제시 에러
s.discard(1)  #없는 요소 삭제시 무시
print(s)  --> {2, 3, 'bbb', 5, 6, 7}

x = s.pop()  #하나씩 삭제
print(x, '삭제됨')
print(s)
--> 결과:
2 삭제됨
{3, 5, 6, 7, 'bbb'}

x = s.pop() 
print(x, '삭제됨')
print(s)
--> 결과:
3 삭제됨
{5, 6, 7, 'bbb'}

s.clear() #모든 요소 삭제. 리스트에서도 동일
print(s)  --> 결과: set()
~~~

### 합집합, 교집합, 차집합

~~~python
#합집합
s1 = {1,2,3}
s2 = {3,4,5}

s3 = s1|s2  
print(s3)  --> {1, 2, 3, 4, 5}

s4=sl.union(s2)  
print(s4)  --> {1, 2, 3, 4, 5}

#교집합
s3 = s1 & s2
print(s3)  --> {3}

s4 = s1.intersection(s2)
print(s4)  --> {3}

#차집합
s3 = s1 - s2
print(s3)  --> {1, 2}

s4 = s2 - s1
print(s4)  --> {4, 5}

s5 = s1.difference(s2)
print(s5)  --> {1, 2}
~~~

## 튜플(tuple)

- 요소 변경X (우회적으로는 변경 가능 - mutable), 튜플도 변경X   
- 고정된 집합 데이터를 저장 및 읽는 작업을 한다.   
- 여러개의 값을 한번에 초기화하는 작업에 많이 사용한다.   

튜플을 생성해보자.

<튜플 생성>
~~~python
t1 = (1,2,3)
for i in t1:
    print(i, end=', ')
print()

for i in range(0, len(t1)):
    print(t1[i], end=', ')
print()
~~~

~~~python
t2 = ('asd', 12, True, [3,4,5])
print(t2)
~~~

<빈 튜플 생성>
~~~python
t3 = ()
print(type(t3))  --> <class 'tuple'>

t4 = (1) # 만약 괄호 안에 숫자가 있다면 int로 되기에 숫자를 넣고 싶다면 뒤에 콤마를 같이 넣어야 한다.
print(type(t4))  --> <class 'int'>

t5 = (1,)
print(type(t5))  --> <class 'tuple'>
~~~

<다차원 튜플>
~~~python
s1 = ((1,2,3),[4,5])
for i in range(0, 2):
    for j in range(0, len(s1[i])):
        print('s1[',i,'][',j,'j=',s1[i][j])  --> 결과(1)

for i in s1:
    print(type(i))
    for j in i:
        print(j, end = ', ')  --> 결과(2)
    print()  

#요소 수정, 삭제 불가
t1 = (1,2,3,4,[5,6,7])
#t1[0] = 10 #생성 이후 =연산자 사용 불가
t1[4][0] = 50
print(t1)  --> 결과(3)

del t1[4][0]
print(t1)  --> 결과(4)
~~~
결과(1):   
s1[ 0 ][ 0 j= 1   
s1[ 0 ][ 1 j= 2   
s1[ 0 ][ 2 j= 3   
s1[ 1 ][ 0 j= 4   
s1[ 1 ][ 1 j= 5   
결과(2):   
<class 'tuple'>   
1, 2, 3,    
<class 'list'>   
4, 5,    
결과(3):   
(1, 2, 3, 4, [50, 6, 7])   
결과(4):   
(1, 2, 3, 4, [6, 7])   

## 딕셔너리

- 키와 값을 묶어서 저장한다.
- 키는 중복 허용 안한다.
- 키의 타입은 변경 불가한 값이어야 하며, 값의 타입은 제약이 없다. 
- 값은 중복 가능하다.
- 요소의 추가, 변경, 삭제가 가능하다.
- 빈 딕셔너리: {}


~~~python
<생성>
d1 = {'name':'aaa', 'age':12, 'flag':True}
print(d1)
print(type(d1))  --> <class 'dict'>

d2 = {1: 'aaa', 2:'bbbb', 3:'ccc'}
print(d2)
print(type(d2))  --> <class 'dict'>

<요소접근>
print(d1["name"])  --> aaa
print(d1["age"])  --> 12
print(d1["flag"])  --> True

print(d2[1])  --> aaa
print(d2[2])  --> bbbb
print(d2[3])  --> ccc

<요소추가>
d1['tel'] = '1234'
print(d1)  --> {'name': 'aaa', 'age': 12, 'flag': True, 'tel': '1234'}

<요소수정>
d1['name']='bbb'
print(d1) --> {'name': 'bbb', 'age': 12, 'flag': True, 'tel': '1234'}

<전체 항복 불러오기>
items = d1.items()
print(items)
for i in items:
    print(i) 
-->
dict_items([('name', 'bbb'), ('age', 12), ('flag', True), ('tel', '1234')])
('name', 'bbb')
('age', 12)
('flag', True)
('tel', '1234')

<요소 삭제>
del d1['name']
print(d1)  --> {'age': 12, 'flag': True, 'tel': '1234'}

<딕셔너리 함수>
d1['name'] = 'aaa'
print(d1.get('name')) #get(키): 키로 검색된 값을 반환  --> aaa
keys = d1.keys()
print(keys)  --> dict_keys(['age', 'flag', 'tel', 'name'])

vals = d1.values()
print(vals)  --> dict_values([12, True, '1234', 'aaa'])

for k in keys:
    val = d1[k]
    print(k,':',val)
-->
age : 12
flag : True
tel : 1234
name : aaa
~~~



