---  
layout: post  
title:  "파이썬(3)_리스트_인덱스_enumerate"  
subtitle:   "리스트 요소 생성/수정/삭제, enumerate"  
categories: Python  
tags: Blog Python     
comments: true  
---  
  
  
## 리스트  
- 하나의 이름에 여러개 값을 담기 위해 사용한다.  
- 즉, 집합 데이터를 효율적으로 사용하기 위해 사용한다.  
  
~~~python
<리스트 사용 안한 예>
s1 = 90
s1 = 80
s3 = 70
sum = s1+s2+s3+....+s100
~~~

~~~python
<리스트 사용 예>
score=[89,67,5,34,65,78,34]
sum = score[0] + score[1] + score[2] + ....
for i in score:
   sum+=i
~~~


## 리스트 요소 및 인덱스


>__a = [1, 2, 3]__

- 리스트 요소는 리스트에 저장된 값 하나를 말한다.  
1, 2, 3 각각을 리스트 요소라고 한다.

- 인덱스는 1, 2, 3 이 위치하는 자리를 뜻한다.  
이때 주의해야 할 것은 인덱스는 0번째부터 센다는 것이다.  
즉, 1은 0번방에 2는 1번방에 3은 2번방에 위치한다고 봐야 한다.

- e.g.,)
a = [1, 2, 3]
print(a[0]) ---> 결과: 1 이 나온다.   
print(a[3]) ---> 결과: 에러가 뜰 것이다.  
a는 방이 0부터 2로 3개가 있다. 3은 범위 밖의 인덱스이므로 에러가 나는 것이다.   
방을 확장하고 싶다면 append를 사용하면 된다.   
a.append(4) ---> 결과: a 리스트에 4를 추가시켜 준다.


## 빈 리스트 생성
~~~python
e = []
e.append(1) 
e.append(2) 
print(e)

결과:
[1, 2]
## e라는 빈 리스트를 만들고 난 후 append를 이용하여 요소를 넣은 것
~~~
~~~python
f = list() #리스트 함수로 생성
f.append("aaa")
f.append("bbb")
print(f)

결과:
['aaa', 'bbb']
## 위와 마찬가지로 append를 이용하여 방을 확장한 것
~~~

## 리스트 요소 변경

리스트 요소는 수정 및 삭제가 가능하다.

~~~python
a = [1,2,3,4,5]
print(a)  ---> 결과: [1, 2, 3, 4, 5]

a[2]=30  #수정(값 재할당)
print(a)  ---> 결과: [1, 2, 30, 4, 5]

del a[2]  #2번방 삭제
print(a)  ---> 결과: [1, 2, 4, 5]

del a[1:3]  #범위로 삭제(1~2)
print(a)  ---> 결과: [1, 5]

a.remove(1) #해당 값을 찾아서 삭제. 없는 값이면 에러.
print(a)  ---> 결과: [5]

b = [2,7,4,5,3]
print(b.index(7)) #7이 위치하는 방 출력  ---> 결과: 1
list.sort(b) #정렬
print(b)  ---> 결과: [2, 3, 4, 5, 7]
~~~

## enumerate

- enumerate():
- 리스트에서 요소를 하나씩 순서대로 추출하는 것을 반복한다.
- 방번호와 요소를 추출하여 반복적으로 반환한다
~~~python
a = [9,8,7,6,5]

print(a)  ---> (1)

for i in a:
    print(i)  ---> (2)

for idx, i in enumerate(a):
    print('idx:', idx, ', i:', i)  ---> (3)

for idx, i in enumerate(a):
    print('a[',idx,']=',i)  ---> (4)
~~~    

- 결과(1):       
[9, 8, 7, 6, 5]  
- 결과(2):   
9    
8   
7   
6   
5   
- 결과(3):   
idx: 0 , i: 9   
idx: 1 , i: 8   
idx: 2 , i: 7   
idx: 3 , i: 6   
idx: 4 , i: 5   
- 결과(4):   
a[ 0 ]= 9   
a[ 1 ]= 8   
a[ 2 ]= 7   
a[ 3 ]= 6   
a[ 4 ]= 5





