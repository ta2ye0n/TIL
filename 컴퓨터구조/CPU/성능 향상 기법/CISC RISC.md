# 컴퓨터 구조
---
## CISC / RISC
---
### 명령어 집합
```
CPU가 이해할 수 있는 명령어들의 모음
```
`명령어 집합구조 (ISA)`라고 부른다

CPU 마다 ISA가 다를수 있다
ISA가 다르다는건 CPU가 이해할 수 있는 명령어가 다르다는 뜻이고, 명령어가 달라지면 어셈블리어도 달라진다
즉 같은 소스 코드로 만들어진 같은 프로그램이라 할지도 ISA가 다르면 CPU가 이해할 수 있는 명령어도 어셈블리어도 달라진다

ISA가 다르면 그에 따른 나비 효과로 많은 것이 달라진다
제어장치가 명령어를 해석하는 방식, 사용되는 레지스터의 종류와 개수, 메모리 관리 방법등 많은 것이 달라지고 이는 CPU 설계에도 큰 영향을 미친다

---
### CISC
```
Complex Instruction Set Computer
복잡한 명령어 집합을 활용하는 컴퓨터
```
복잡하고 다양한 명령어들을 활용하는 CPU 설계 방식이다

CISC는 다양하고 강력한 기능의 명령어 집합을 활용하기 때문에 명령어의 형태와 크기가 다양한 `가변 길이 명령어`를 활용한다
다양하고 강력한 명령어를 활용한다는 말은 상대적으로 적은 수의 명령어로도 프로그램을 실행할 수 있다는것을 의미한다

적은 수의 명령어만으로도 프로그램을 동작시킬 수 있다는 점은 `메모리 공간을 절약`할 수 있다는 장점이 있다
하지만 CISC는 활용하는 명령어가 워낙 복작하고 다양한 기능을 제공하는 탓에 `명령어의 크기와 실행되기까지의 시간이 일정하지 않다`는 단점이 있다
그리고 복잡한 명령어 때문에 명령어 하나를 실행하는 데에 여러 클럭 주기를 필요로 한다

또한 CISC가 활요하는 명령어는 명령어 수행 시간이 길고 가지각색이기 때문에 파이프라인이 효율적으로 명령어를 처리할 수 없다
게다가 CISC가 복잡하고 다양한 명령어를 활용할 수 있지만 사실 대다수의 복잡한 명령어는 사용 빈도가 낮고 실제로는 자주 사용되는 명령어만 사용되었다

이러한 이유들로 CISC 기반 CPU는 성장에 한계가 있다

---
### RISC
```
Reduced Instruction Set Computer
```
RISC는 CISC에 비해 명령어의 종류가 `적다`
그리고 CISC와는 달리 `짧고 규격화된 명령어`, 되도록 1클럭 내외로 실해오디는 명령어를 지향한다
즉, RISC는 `고정 길이 명령어`를 활용한다

명령어가 규격화되어 있고, 하나의 명령어가 1클럭 내외로 실행되기 때문에 RISC 명령어 집합은 명령어 파이프라이닝에 최적화되어 있다

RISC는 메모리에 직접 접근하는 명령어를 load, store `두 개로 제한`할 만큼 메모리 접근을 `단순화하고 최소화를 추구`한다
> 이런 점에서  RISC를 `load-store 구조`라고 부르기도 한다

RISC는 메모리 접근을 단순화, 최소화하는 대신에 `레지스터를 적극적으로 활용`한다
그렇기에 CISC보다 레지스터를 이용하는 연산이 많고, 일반적인 경우보다 범용 레지스터 개수도 더 많다
다만 사용 가능한 명령어 개수가 CISC보다 적기 때문에 RISC는 CISC보다 많은 명령으로 프로그램을 작동시킨다

---
### CISC와 RISC 차이
|CISC|RISC|
|:----:|:-----:|
|복잡하고 다양한 명령어|단순하고 적은 명령어|
|가변 길이 명령어|고정 길이 명령어|
|다양한 주소 지정 방식|적은 주소 지정 방식|
|프로그램을 이루는 명령어의 수가 적음|프로그램을 이루는 명령어의 수가 많음|
|여러 클럭에 걸쳐 명령어 수행|1클럭 내외로 명령어 수행|
|파이프라이닝하기 어려움|파이프라이닝하기 쉬움|