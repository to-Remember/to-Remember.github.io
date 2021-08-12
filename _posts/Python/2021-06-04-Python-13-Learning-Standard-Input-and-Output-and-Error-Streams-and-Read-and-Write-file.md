---  
layout: post  
title:  "파이썬(13)_입력_출력_에러스트림_파일입출력"  
subtitle:   "입력, 출력, 에러 스트림"  
categories: Python  
tags: Blog Python
comments: true  
---  

**바로가기:**     
[파일입출력](#파일입출력)     
[경로표현](#경로표현)     
[파일쓰기](#파일쓰기)     
[읽고 쓰기 위치 제어](#파일의-읽고-쓰기-위치-제어)     
[파일제어](#파일제어)    
[파일읽기](#파일읽기)     

# 입출력     
- **입력**: 데이터가 외부에서 프로그램 방향으로 흘러오는 것.     
- **출력**: 데이터가 프로그램에서 외부로 흘러나가는 것.      
- **예외처리**: 예외 발생시 프로그램이 중단되는 것을 막아 안정성을 높인다.     

- 표준입출력(stdio)     
sys.stdin:표준입력     
sys.stdout:표준출력     
sys.stderr:표준에러     

~~~python
import sys

def main():
    sin = sys.stdin  #키보드 입력 스트림. 스트림:데이터의 흐름을 소프트웨어로 구현한 것
    sout = sys.stdout  #콘솔 출력 스트림
    serr = sys.stderr   #콘솔 에러 출력 스트림

    num = sout.write('문자를 입력하시오\n')  #write():출력 스트림에 출력
    sout.write(str(num)+' 개의 문자 출력됨\n')
    s = sin.read(5)  #read(size):입력 스트림에서 size만큼 읽음
    sout.write('입력받은 값:'+s+'\n')
    sout.write('한줄을 입력하시오\n')
    sin.readline()
    s = sin.readline()
    sout.write('입력받은 값:' + s + '\n')
    serr.write('에러 메시지')

main()
~~~

# 파일입출력     

1. **파일오픈**       
  file = open(파일경로, [모드:기본은 r])      
  open("a.txt", "r")     
- 모드:r(읽기. 파일 없으면 에러)     
- w(쓰기. 파일이 없으면 새로생성. 있으면 파일 내용 지우고 새로씀)     
- a(이어쓰기. 있으면 파일 내용 이어씀)     
- t(텍스트), b(바이너리)     
- r+(읽고쓰기), w+(읽고쓰기), a+(읽고쓰기)     

2. **읽기/쓰기 작업**     
- 읽기     
read(size):size 크기만큼 파일에서 읽어서 반환     
read():파일 전체 읽어서 반환     
readline(): 한줄읽어서 반환     
- 쓰기     
write(출력값): 파일에 출력값을 씀     
writelines(리스트, 튜플...):리스트나 튜플에 들어있는 값들을 파일에 출력     
  
3. **파일 닫음**     
- 파일 사용 후 무조건 파일 닫음     
file.close()     

# 경로표현     

1. 절대경로       
2. 상대경로     
- 현재 프로그램을 기준으로 해당 파일을 찾아감     
-./ 현재 디렉토리     
../ 상위 디렉토리     
디렉토리명  --> 하위 디렉토리     
  ./files/a.txt     
  ../6day/names.py     

~~~python
def read1():
    print('====read1====')
    file = open('./files/a.txt', 'r', encoding='utf-8')  #파일 읽기 모드로 오픈
    while True:
        s = file.read(5)  #5바이트씩 읽기
        if s == '':  #더이상 읽을 것이 없을 때 멈춤
            break
        else:
            print(s, end='')
    file.close()

def read2():
    print('====read2====')
    file = open('./files/a.txt', 'r', encoding='utf-8')
    s = file.read()  #한번에 전체 읽기
    print(s)
    file.close()

def read3():
    print('====read3====')
    file = open('./files/a.txt', 'r', encoding='utf-8')
    while True:
        s = file.readline()  #한줄씩 읽기
        if s=='':
            break
        else:
            print(s)
    file.close()

def main():
    read1()
    read2()
    read3()

main()
~~~

# 파일쓰기

~~~python
def write1():
    file = open('./files/b.txt', 'w', encoding='utf-8')
    file.write('hello file')
    file.close()

def write2():
    file = open('./files/c.txt', 'w', encoding='utf-8')
    while True:
        s = input('메시지 입력(멈추려면 /stop):')
        if s=='/stop':
            break
        else:
            file.write(s+'\n')
    file.close()

def copy(src, dest):#파일복사
    f1 = open(src, 'r', encoding='utf-8')
    f2 = open(dest, 'w', encoding='utf-8')
    data = f1.read()
    f2.write(data)
    f1.close()
    f2.close()

def write3():
    f = open('./files/b.txt', 'a', encoding='utf-8')
    f.write('가나다라')
    f.close()

def write4():
    s = ['aaa\n', 'bbb\n', 'ccc\n']
    f = open('./files/e.txt', 'w', encoding='utf-8')
    f.writelines(s)
    f.close()

def with_open():
    with_open('./files/e.txt', 'r') as f:  #파일오픈 with블록. open()동일. open()이 반환하는 파일 객체를 as 뒤 변수에 저장. 파일 닫기 생략.
        while True:
            s = f.readline()
            if s=='':
                break
            else:
                print(s)

def main():
    # write1()
    #write2()
    #copy('./files/a.txt', './files/d.txt')
    with_open()

main()
~~~

# 파일의 읽고 쓰기 위치 제어

- tell(): 현재 위치 반환     
- seek(off, whence):      
whence를 기준으로 off만큼 떨어진 위치로 이동. whence는 0(맨앞), 1(현재위치), 2(맨뒤)     

~~~python
def writeFile():
    f = open('./files/f.txt', 'w')
    s = 'abcdefghijklmnopqrstuvwxyz'
    f.write(s)
    f.close()

def readFile():
    f = open('./files/f.txt', 'rb')
    s = f.read(3)  #3바이트 읽음
    print(s)
    print('현재위치:', f.tell())
    f.seek(5, 1)
    print('현재위치:', f.tell())
    s = f.read(1)
    print('현재 위치에서 5이동:', s)

    f.seek(-2, 1)
    s = f.read(1)
    print('현재 위치에서 -2이동:', s)
    f.seek(10, 0)
    s = f.read(1)
    print('맨앞에서 10이동:', s)
    f.seek(-1, 2)
    s = f.read(1)
    print('맨뒤에서 -1이동:', s)

    f.close()

def main():
    writeFile()
    readFile()

main()
~~~

# 파일제어

1. **파일절삭**     
지정한 크기로 파일 단편화     
file.truncate(size)     
2. **파일명 바꾸기**     
os.rename(old, new)     
3. **파일 삭제**     
os.remove(파일명)     
4. **현재 작업디렉토리**     
  os.getcwd()     
5. **작업 디렉토리 변경**     
os.chdir(path)     
6. **디렉토리 생성**     
os.mkdir(path)     
7. **디렉토리 삭제**     
os.rmdir(path)     
8. **디렉토리 안에 있는 파일 목록**     
os.listdir(path)     
9. **파일 존재 확인**     
os.path.isfile(path) => 파일 있으면 True, 없으면 False     
10. **디렉토리 존재 확인**     
os.path.isdir(path) => 디렉토리 있으면 True, 없으면 False     

~~~python
import os
def trunc():
    file_name = './files/g.txt'
    f = open(file_name, 'w')
    s = 'abcdefghijklmnopqrstuvwxyz'
    f.write(s)
    f.truncate(10)
    f.close()

    f = open(file_name, 'r')
    s = f.read()
    print(s)
    f.close()

def rename():
    os.rename('./files/g.txt', './files/g123.txt')
    with open('./files/g123.txt', 'r') as f:
        print(f.read())
'''  에러
    with open('./files/g.txt', 'r') as f:
        print(f.read())
'''

def file_test():
    print('현재 디렉토리:', os.getcwd())
    if os.path.isdir('test'):
        print('files 디렉토이 있음')
    else:
        print('files 디렉토이 없음')
        os.mkdir('test')

    os.chdir('test')  #작업 디렉토리 test로 변경
    print('현재 디렉토리:', os.getcwd())

    fname = ['f1.txt', 'f2.txt', 'f3.txt']
    for i in fname:
        f = open(i, 'w')
        f.write(i+' content')
        f.close()

    files = os.listdir()  #test 디렉토리 파일 목록(이름)
    print(files)
    for i in files:
        with open(i, 'r') as f:
            s = f.read()
            print(i, ' : ', s)

    os.remove(files[0])  #test 디렉토리에서 f1.txt 파일 삭제

    for i in files:
        if os.path.isfile(i):
            print(i, ' 파일 존재함')
        else:
            print(i, ' 파일 삭제됨')

    os.chdir('../')
    print('현재 디렉토리:', os.getcwd())

def main():
    file_test()

main()

~~~

# 파일읽기

~~~python
def read1():
    print('====read1====')
    file = open('./files/a.txt', 'r', encoding='utf-8')#파일 읽기 모드로 오픈
    while True:
        s = file.read(5)  #5바이트씩 읽기
        if s == '':  #더이상 읽은것이 없을 때 멈춤
            break
        else:
            print(s, end='')
    file.close()

def read2():
    print('====read2====')
    file = open('./files/a.txt', 'r', encoding='utf-8')
    s = file.read()  #한번에 전체 읽기
    print(s)
    file.close()

def read3():
    print('====read3====')
    file = open('./files/a.txt', 'r', encoding='utf-8')
    while True:
        s = file.readline()  #한줄씩 읽기
        if s=='':
            break
        else:
            print(s)
    file.close()

def main():
    read1()
    read2()
    read3()

main()
~~~
