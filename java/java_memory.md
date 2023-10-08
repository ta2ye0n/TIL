# Java
---
## 메모리 구조
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQRqku%2Fbtru0vJ6Ixx%2F9qCTW7ChXc80fGfQUrT4B0%2Fimg.png)

---
### JVM
```
Java Virtual Machine
자바 가상 머신

자바 프로그램 실행환경을 만들어 주는 소프트웨어
```
자바와 운영체제 사이에서 중개자 역할을 수행하며, 자바가 운영체제에 구애 받지 않고 프로그램을 실행할 수 있도록 도와준다
또한 다른 하드웨어나 다르게 레지스터 기반이 아닌 스택 기반으로 동작한다

---
### 클래스 로더(Class Loader)
```
클래스 파일을 로드하고 링크를 통해 배치하는 작업을 수행하는 모듈

런타임시에 동적으로 클래스를 로딩
```
자바에서 소스를 작성하면 `.java`파일이 생성되고 .java소스를 컴파일러가 컴파일하면 `.class`파일이 생성되는데 클래스 로더는 .class 파일을 묶어서 JVM이 운영체제로 부터 할당받은 메모리 영역인 `Runtime Data Area`로 적재한다

---
### 실행 엔진(Execution Engine)
```
클래스 로더를 통해 JVM 내의 Runtime Data Area에 배치된 바이트 코드들을 명령어 단위로 읽어서 실행
```
실행 엔진은 바이트코드를 명령어 단위로 읽어서 실행한다

---
### 가비지 컬렉터 (Garbage Colletor)
```
힙 메모리 영역에 생성된 객체들 중에서 참조되지 않은 객체들을 탐색 후 제거하는 역할
```
개발자가 따로 메모리를 과닐하지 않아도 되므로, 손쉽게 프로그래밍 할 수 있도록 도와준다
해당 역할을 하는 시간은 정확히 언제인지 알 수 없다

---
### 런타임 데이터 영역(Runtime Data Area)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZR97z%2FbtrvtdBl1Md%2FLbUk2NVlgDmsKMcBiQ9f4K%2Fimg.png)
```
JVM의 메모리 영역으로 자바 애플리케이션을 실행 할 때 사용되는 데이터를 적재하는 영역
```

모든 스레드가 공유해서 사용(GC의 대상)
- 힙 영역(Heap Area)
- 메서드 영역(Method Area)

스레드(Thread) 마다 하나씩 생성
- 스택 영역(Stack Area)
- PC 레지스터 (PC Register)
- 네이틷브 메서드 스택 (Native Method Stack)

#### 메서드 영역 (Method Area)
```
모든 스레드가 공유하는 메모리 영역
```
메소드 영역은 클래스, 인터페이스, 메서드, 필드, Static 변수 등의 바이트 코드를 보관한다

#### 힙 영역 (Heap Area)
```
모든 스레드가 공유하며, new 키워드로 생성된 객체와 배열이 생성되는 영역

메서드 영역에 로드된 클래스만 생성이 가능하고 Garbage Colletor가 참조되는 않는 메모리를 확인하고 제거하는 영역
```

#### 스택 영역 (Stack Area)
```
지역변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값 등이 생성되는 영역
```
메서드 호출 시마다 각각의 스택 프레임이 생성한다
그리고 메서드 안에서 사용되는 값들을 저장하고, 호출된 메서드의 매개변수, 지역변수, 리턴 값 및 연산 시 일어나는 값들을 임시로 저장한다
마지막으로, 메서드 수행이 끝나면 프레임별로 삭제한다

#### PC Register
```
쓰레드가 어떤 부분을 무슨 명령으로 실행해야할 지에 대한 기록하는 부분으로 현재 수행중인 JVM 명령의 주소를 갖음
```

쓰레드가 시작될 때 생성되며, 생성될 때마다 생성되는 공간으로 쓰레드마다 하나씩 존재한다

#### Native method stack
```
자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역
```