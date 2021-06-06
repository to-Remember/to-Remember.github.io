---
layout: post
title:  "파이썬(1)"
subtitle:   "제어문 및 반복문"
categories: Blog
tags: python   
comments: true
---


## _파이썬(1)-제어문 및 반복문_

## 제어문
프로그램의 흐름을 제어하는 문장으로 프로그램의 가장 기초이며 기본이다.

#### if문
- 조건을 만족하면 블록을 실행한다.
- 불만족시 실행하지 않고 건너뛴다.
- if조건: -> 블록 시작
- *들여쓰기가 끝날때까지

#### if-else문
- 조건 만족시 if블록을 실행한다
- 불만족시 else를 실행한다.
 ```sh
>>> if 조건:
>>>     print('조건만족')
>>> else:
>>>     print('조건불만족')
```

#### if-elif-elif-else
- 3개 이상의 조건일 경우 사용
-  e.g., 1. 게임시작 2. 캐릭터 선택 3. 연습 4. 게임종류
 ```sh
 메뉴가 2일 경우
>>> menu = 2
>>> if menu ==1:
>>>     print('game start')
>>> elif menu==2:
>>>     print('select char')
>>> elif menu==3:
>>>     print('exercise')
>>> elif menu==4:
>>>     print('game over')
>>> else:
>>>     print('다시 입력하시오')
결과:
select char
*메뉴가 2로 지정되어 있기에 select char이 출력된 것
```
## 반복문

특정 동작을 반복한다.

### while문:
- 조건이 True일 동안 반복한다.
- 조건이 False가 되면 중단한다.
```sh
(e.g.,1)
>>> a = 3
>>> while a > 0:
>>>     print(a)
>>>     a -= 1
>>> print('while밖')
결과:
3
2
1
while밖
```

```sh
(e.g.,2)
>>> a = 1
>>> while a < 3:
>>>     print(a)
>>>     a += 1
결과:
1
2
```
