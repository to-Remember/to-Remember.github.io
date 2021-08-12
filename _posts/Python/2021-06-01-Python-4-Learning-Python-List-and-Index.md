---  
layout: post  
title:  "파이썬(4)_리스트요소_다차원리스트"  
subtitle:   "리스트 요소 접근 및 다차원 리스트"  
categories: Python  
tags: Blog Python     
comments: true  
---  

## 리스트 요소 접근

~~~python
a = [1, 2, 3]
print(a[0])  ---> 0번방 값 출력
print(a[1])
print(a[2])

결과:
1
2
3
~~~

~~~python
a=[1,2,3]

for i in range(0, 3): ---> i: 인덱스. 방번호
    print(a[i], end=', ')
print()
for i in a: ---> i : 요소
    print(i, end=', ')
print()

결과:
1, 2, 3, 
1, 2, 3,
~~~

~~~python
b = ['aaa', 'bbb', 'ccc']
print('b의 길이: ', len(b))
print('asdf의 길이: ', len('asdf'))
print('b의 요소 출력:')
for i in range(0, len(b)):
    print(b[i], end=', ')
print()

for i in b:
    print(i, end=', ')
print()

결과:
b의 길이:  3
asdf의 길이:  4
b의 요소 출력:
aaa, bbb, ccc, 
aaa, bbb, ccc, 
~~~

## 다차원 리스트

- 다차원 리스트는 복잡한 구조의 데이터를 표현하기 위해 사용한다.


~~~python
<예시>

a = [[1,2,3], [4,5,6]]

print(a[0])  ---> [1,2,3]
print(a[1])  ---> [4,5,6]

print(a[0][0])  ---> 1
print(a[0][1])  ---> 2
print(a[0][2])  ---> 3
print(a[1][0])  ---> 4
print(a[1][1])  ---> 5
print(a[1][2])  ---> 6

for i in a:  ---> 2번 반복한다. 방 2개 짜리 리스트
    for j in i:  ---> [4,5,6]
        print(j, end=',')
    print()    
---> 
1,2,3,
4,5,6,

for i in range(0, len(a)):
    for j in range(0, len(a[i])):
        print(a[i][j], end=',')
    print()
---> 
1,2,3,
4,5,6,

for i in range(0, len(a)):
    for j in range(0, len(a[i])):
        a[i][j] *= 10 # a[i][j] = a[i][j] * 10

for i in a:  ---> 2번 반복. 방 2개 짜리 리스트
    for j in i:#[4,5,6]
        print(j, end=',')
    print()
--->
10,20,30,
40,50,60,

# 요소 입력받아 저장하기
for i in range(0, len(a)):  
    for j in range(0, len(a[i])):
        a[i][j]=int(input('num:'))

print(a)
--->
[[5, 6, 7], [55, 66, 77]]  -> 입력한 값이 출력된 것.
~~~












