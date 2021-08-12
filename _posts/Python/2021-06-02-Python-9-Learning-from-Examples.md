---  
layout: post  
title:  "파이썬(9)_함수_예제_피카추게임_주소록_만들기"  
subtitle:   "피카츄 게임 만들기, 주소록 만들기"  
categories: Python  
tags: Blog Python  
comments: true  
---  

> [주소록 만들기 바로가기](#함수를-활용하여-주소록-만들기)

# 피카츄 게임 만들기     

- 변수(상태값)      
hp = 30 단, 0이면 죽음     
exp(경험치) = 0     
lv = 1 단, 경험치 20마다 레벨 1 증가     

- 기능 -> 함수로구현     
밥먹기: hp 5증가     
잠자기: hp 10증가     
운동하기: hp 15감소. exp 15증가     
놀기:hp 5감소. exp 7증가. hp감소(생존 체크). exp증가(레벨업 체크)     
종료     

~~~python
#초기값
hp = 30
exp = 0
lv = 1

def eat(hp):
    print('밥을 먹었습니다')
    hp += 5
    return hp

def sleep(hp):
    print('잠을 잤습니다')
    hp += 10
    return hp

def play(hp,exp,lv):
    print('놀았습니다')
    hp -= 5
    if hp <= 0:
        print('사망했습니다')
        exit()
    exp += 7
    if exp >= 20:
        lv += 1
        exp -= 20
        print('레벨업 했습니다')
    return hp, exp, lv

def exercise(hp,exp,lv):
    print('운동을 했습니다')
    hp -= 15
    if hp <= 0:
        print('사망했습니다')
        exit()
    exp += 15
    if exp >= 20:
        lv += 1
        exp -= 20
        print('레벨업!!')
    return hp, exp, lv

while True:
    m = int(input('1. 밥을먹는다 2. 잠을잔다 3. 신나게논다 4. 운동을한다 5. 게임종료: ' ))
    if m == 1:
        hp = eat(hp)
    elif m == 2:
        hp = sleep(hp)
    elif m == 3:
        hp,exp,lv = play(hp,exp,lv)
    elif m == 4:
        hp,exp,lv = exercise(hp,exp,lv)
    elif m == 5:
        print('게임종료')
        exit()

    print('stat: ')
    print('hp:',hp,'exp:', exp, 'lv:', lv)
~~~

# 함수를 활용하여 주소록 만들기

- 한 사람 정보(이름, 전화번호, 주소) -> 3가지 정보를 가짐     
1. 등록(이름 중복 안됨)     
2. 검색(이름으로) -> 정보출력 or 없다.     
3. 수정(이름으로 찾아서 수정) -> 전화번호, 주소 수정     
4. 삭제(이름으로)     
5. 주소록 전체출력     
6. 종료     

~~~python
members = []
titles = ['name:', 'tel:', 'address:']

def addMember():  #등록함수
    m = [0,0,0]
    print('새 멤버 등록')
    for i in range(0, len(m)):
        if i==0:  #이름 입력일때
            while True:
                m[i] = input(titles[i])
                res = getByName(m[i])
                if res==None:
                    break
        else:  #전화, 주소 입력
            m[i] = input(titles[i])

    members.append(m)

def getByName(name):
    for idx, i in enumerate(members):
        if name==i[0]:
            return idx, i #튜플로 반환(idx, i) => res[0]:idx, res[1]:i

def printMember():
    print('멤버 검색')
    name = input('검색할 이름:')
    res = getByName(name)
    if res == None:
        print('not found name')
    else:
        i = res[1]
        cnt = 0
        for j in i:
            print(titles[cnt], j)
            cnt+=1
        print('-------------')

def printAll():
    print('모든 멤버')
    for i in members:  #i는 한명 리스트 ['aaa', '111','asdf']
        cnt=0
        for j in i:
            print(titles[cnt], j)
            cnt+=1
        print('-------------')

def editMember():
    print('멤버 정보 수정')
    name = input('수정할 이름:')
    res = getByName(name)
    if res == None:
        print('not found name')
    else:
        i = res[1]
        i[1]=input('new tel:')
        i[2]=input('new address:')

def delMember():
    print('멤버 삭제')
    name = input('삭제할 이름:')
    res = getByName(name)
    if res == None:
        print('not found name')
    else:
        del members[res[0]]

def main():
    while True:
        menu = int(input('1.등록 2.검색 3.수정 4.삭제 5.전체출력 6.종료'))
        if menu == 1:
            addMember()
        elif menu == 2:
            printMember()
        elif menu == 3:
            editMember()
        elif menu ==4:
            delMember()
        elif menu == 5:
            printAll()
        elif menu == 6:
            break

main()
~~~
