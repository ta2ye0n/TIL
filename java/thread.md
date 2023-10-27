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