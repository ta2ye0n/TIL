
# JAVA
---
## JAVA 데이터 타입
1. 논리형
```
Boolean - true와 false 중 하나를 값으로 갖으며 조건식과 논리적 계산에 사용

크기 - bit : 8 byte : 1
```
2. 문자형
```
char - 문자를 저장하는데 사용되며, 변수에 하나의 문자만 저장이 가능

크기 - bit : 16 byte : 2
```
3. 정수형
```
short, byte, int, long - 정수를 저장하는데 사용되며, 주로 int가 사용됨 byte는 이진 데이터를 다룰때 사용되며 short는 C언어와의 호환을 위해서 추가 됨

크기 - byte - bit : 8 byte : 1
       short - bit : 16 byte : 2
       int - bit : 32 byte : 4
       long - bit : 64 byte : 8
```
4. 실수형
```
float, double - 실수를 저장하는데 사용되며, 주로 double이 사용됨

크기 - float - bit : 32 byte : 4
       double - bit : 64 byte : 8
```
4-1. 실수형의 정밀도   
```
실수형은 정수형과 저장방식이 다르기에 같은 크기라도 훨씬 큰값을 표현할 수는 있지만, 오차가 발생할 수 있음 정밀도가 중요한데, 정밀도가 높을수록 오차의 범위가 즐어듬

정밀도 float  - 7자리
       double - 15자리
```
---
## 자료형
1. 기본형(Primitive Type)
```
논리형(boolean),문자형(char),정수형(byte,short,int,long),실수형(float,double) 계산을 위한 실제 값을 저장
```
2. 참조형(Reference Type)
```
객체의 주소를 저장한다. 기본적으로 'Java.lang.Ovject'를 상속받을 경우 참조형이 됨 즉, 기본형을 제외하고는 참조형이라 생각하면 됨
```

기본형은 메모리영역의 스택영역에 실제 값들이 저장된다면, 참조형은 실제 인스튼스는 합영역에 생성되있고, 그 영역의 주소를 스택영역에서 저장하고 있다고 보면 됨

---