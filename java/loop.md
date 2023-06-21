# java
---
## 제어문
---
### 반복문
```
프로그램 내에서 똑같은 명령을 일정 횟수만큼 반복하여 수행하도록 제어하는 명령문
프로그램이 처리하는 대부분의 코드는 반복적인 형태가 많으므로, 가장 많이 사용되는 제어문 중 하나

자바에서 사용되는 대표적인 반복문의 형태
1. while 문
2. do / while 문
3. for 문
4. Enhanced for 문
```
1. while 문
``` java
특정 조건을 만족할 때까지 계속해서 주어진 명령문을 반복 실행한다

while (조건식) {
    조건식의 결과가 참인 동안 반복적으로 실행하고자 하는 명령문;
}
``` 
![](https://www.dotnetkorea.com/docs/c-language/16-while-do/while-flowchart.png)   
``` java
while 문은 조건식이 참(true)인지를 판단하여, 참이면 내부의 명령문을 실행한다
내부의 명령문을 전부 실행하고 나면, 다시 조건식으로 돌아와 또 한번 참인지를 판단한게 된다

// while 문을 5번 반복해서 실행하는 예제
int i = 0;

while (i < 5) {

    System.out.println("while 문이 " + (i + 1) + "번째 반복 실행중입니다.");

    i++; // 이 부분을 삭제하면 무한 루프에 빠지게 됨.

}

System.out.println("while 문이 종료된 후 변수 i의 값은 " + i + "입니다.");
```
while 문 내부에 조건식의 결과를 변경하는 명령문이 존재하지 않을 때는 프로그램이 영원히 반복되게 된다
이것을 무한 루프(infinite loop)에 빠졌다고 하며, 무한 루프에 빠진 프로그램은 영원히 종료되지 않는다

2. do / while 문
```
먼저 루프를 한 번 실행한 후에 조건식을 검사한다
즉, do / while 문은 조건식의 겨로가와 상관없이 무조건 한 번은 루프를 실행한다
```
![](https://www.dotnetkorea.com/docs/c-language/16-while-do/do-while-flowchart.png)   
``` java
do {
    조건식의 결과가 참인 동안 반복적으로 실행하고자 하는 명령문;
} while (조건식);

// 예제
int i = 1, j = 1;

 

while (i < 1) {

    System.out.println("while 문이 " + i + "번째 반복 실행중입니다.");

    i++; // 이 부분을 삭제하면 무한 루프에 빠지게 됨.

}

System.out.println("while 문이 종료된 후 변수 i의 값은 " + i + "입니다.");

 

do {

    System.out.println("do / while 문이 " + i + "번째 반복 실행중입니다.");

    j++; // 이 부분을 삭제하면 무한 루프에 빠지게 됨.

} while (j < 1);

System.out.println("do / while 문이 종료된 후 변수 j의 값은 " + j + "입니다.");
```
> 위의 예제가 만약 while 문이었다면 단 한번의 출력도 없었을 것이다

3. for 문
```
자체적으로 초기식, 조건식, 증감식을 모두 포함하고 있는 반복문이다
```
![](https://www.memoengine.com/Posts/files/for-statement-flowchart_637762290827072976.png)
``` java
for (초기식; 조건식; 증감식) {
    조건식의 결과가 참인 동안 반복적으로 실행하고자 하는 명령문;
}

이때 for 문을 구성하는 초기식, 조건식, 증감식은 각각 생략 할 수 있다

// 예제
for (i = 0; i < 5; i++) {

    System.out.println("for 문이 " + (i + 1) + "번째 반복 실행중입니다.");

}

System.out.println("for 문이 종료된 후 변수 i의 값은 " + i + "입니다.");
```

4. Enhanced for 문
```
JDK 1.5부터 Enhanced for 문이라는 반복문이 추가되었다
이 반복문은 컬렉션 프레임워크와 배열에서 유용하게 자주 사용된다
```