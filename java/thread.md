# JAVA
---
## Thread
```
프로세스(process) 내에서 실제로 작업을 수행하는 주체
```
모든 프로세스에는 한 개 이상의 스레드가 존재하여 작업을 수행한다
또한, 두개 이상의 스레드를 가지는 프로세스를 `멀티스레드 프로세스(multi-threaded process)`라고 한다

---
### 스레드의 생성과 실행
```
1. Runnable 인터페이스 구현 방법
2. Thread 클래스 상속받는 방법
```
두 방법 모두 스레드를 통해 작업하고 싶은 내용을 `run()`메서드에 작성하면 된다

```java
Ex)

class ThreadWithClass extends Thread {

    public void run() {

        for (int i = 0; i < 5; i++) {

            System.out.println(getName()); // 현재 실행 중인 스레드의 이름을 반환함.
            try {
                Thread.sleep(10);          // 0.01초간 스레드를 멈춤.
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class ThreadWithRunnable implements Runnable {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName()); // 현재 실행 중인 스레드의 이름을 반환함.
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Thread01 {
    public static void main(String[] args){

        ThreadWithClass thread1 = new ThreadWithClass();       // Thread 클래스를 상속받는 방법

        Thread thread2 = new Thread(new ThreadWithRunnable()); // Runnable 인터페이스를 구현하는 방법

        thread1.start(); // 스레드의 실행
        thread2.start(); // 스레드의 실행
    }
}
```

> Runnable 인터페이스는 몸체가 없는 메서드인 run() 메서드 단 하나만을 가지는 간단한 인터페이스이다
---
### Thread 클래스
- JDK에서 지원하는 `java.lang.Thread` 제공
- <Thread 생성자>

|Thread()||
|:------:|:------:|
|Thread(String name)|스레드 이름|
|Thread(Runnable target)|인터페이스 객체|
|Thread(Runnable target, String name)| 인터페이스 객체와 스레드 이름|

- <Thread 메서드>

|메서드||
|:-----:|:-----:|
|void run()|스레드가 실행할 부분 기술 (오버라이딩 사용)|
|void start()|스레드를 시작 run() 메서드 호출|
|void interrupt()|스레드를 중지 시킴|
|void join()|스레드가 긑날때까지 대기|
|static void sleep(long millis)|millis 시간 동안 현재 스레드를 일시중지 시킴|
|int getProiroty()|스레드의 우선 순위 반환|
|void setpriority(int p)|스레드의 우선순위를 p값으로 변경|
|boolean isDaemon()|스레드가 데몬 스레드인지 여부를 반환|
|boolean isAlive()|스레드가 살아있는지 여부를 반환|
|void setDaemon(boolean on)|스레드를 데몬 스레드로 변경한다|

> static 메서드는 해당 메서드를 호출한 스레드 자신에게 적용된다는 점을 유의해야한다
---
### 멀티 스레드 (multi thread)
```
하나의 프로세스 내에서 둘 이상의 스레드가 동시에 작업을 수행하는 것
```
>멀티 프로세스(multi process) : 여러개의 CPU를 사용하여 여러 프로세스를 동시에 수행하는 것

멀티 스레드는 각 스레드가 자신이 속한 프로세스의 메모리를 공유하므로, `시스템 자원의 낭비가 적다`   
또한, 하나의 스레드가 작업을 할 때 다른 스레드가 별도의 작업을 할 수 있어 `사용자와의 응답성`도 좋아진다

---
### 문맥 교환 (context switching)
```
현재까지의 작업 상태나 다음 작업에 필요한 각종 데이터를 저장하고 읽어오는 작업
```

컴퓨터에서 동시에 처리할 수 있는 최대 작업 수는 CPU의 코어(core) 수와 같다
만약 CPU의 코어 수 보다 더 많은 스레드가 실행되면, 각 코어가 정해진 시간 동안 여러 작업을 번갈아가며 수행하게 된다
이때 각 스레드가 교체될 때 `스레드 간의 문맥교환`이 발생한다

문맥교환에 걸리는 시간이 커지면 커질수록 `멀티 스레딩의 효율은 저하`된다
오히려 많은 양의 단순한 계산은 `싱글 스레드로 동작`하는 것이 더 효율 적일 수 있다

따라서 많은 수의 스레드를 실행하는 것이 언제나 `좋은 성능을 보이는 것은 아니라는 점`을 유의해야 한다

---
### 스레드 그룹(thread group)
```
서로 관련이 있는 스레드를 하나의 그룹으로 묶어 다루기 위한 장치

자바에서는 스레드 그룹을 다루기 위해 TreadGroup이라는 클래스를 제공한다
```

스레드 그룹은 다른 스레드 그룹을 포함할 수도 있고, 이렇게 포함된 스레드 그룹은 `트리형태`로 연결된다

이때 스레드는 자신이 포함된 스레드 그룹이나 그 하위 그룹에는 접근할 수 있지만, 다른 그룹에는 접근할 수 없다
이렇게 스레드 그룹은 스레드가 `접근할 수 있는 범위를 제한하는 보안상`으로도 중요한 역할을 한다

---
### 데몬 스레드 (deamon thread)
```
다른 일반 스레드의 작업을 돕는 보조적인 역할을 하는 스레드

따라서 데몬 스레드는 일반 스레드가 모두 종료되면 더는 할 일이 없으므로, 자동으로 종료된다
```
데몬 스레드의 생성 방법과 실행 방법은 모두 일반 스레드와 같다
단, 실행하기 전에 `setDaemon()`메서드를 호출하여 데몬 스레드로 설정하기만 하면 된다

데몬 스레드는 `일정 시간마다 자동으로 수행`되는 저장 및 화면 갱신 등에 이용된다

---
### 가비지 컬렉터(gabage collector)
```
프로그래머가 동적을 할당한 메모리 중 더 이상 사용하지 않는 영역을 자동으로 찾아내어 해체해 주는 데몬 스레드
```

자바에서는 프로그래머가 메모리에 직접 접근하지 못하게 하는 대신에 가비지 컬렉터가 `자동으로 메모리를 관리`해준다
이러한 가비지 컬렉터를 사용하면 `프로그래밍을 하기가 훨씬 쉬워`지며, 메모리에 관련된 `버그가 발생할 확률`도 낮아진다

보통 가비지 컬렉터가 동작하는 동안에는 프로세서가 `일시적으로 중지`되므로, 필연적으로 `성능의 저하`가 발생한다
하지만 요즘 가비지 컬렉터의 성능이 많이 향상되어, 새롭게 만들어지는 대부분의 프로그래밍 언어에서 가비지 컬렉터를 제공한다