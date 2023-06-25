# java
---
## 제어문
---
### 기타 제어문

루프의 제어
``` 
일반적으로 조건식의 검사를 통해 루프로 진입하면 다음 조건식을 검사하기 전까지 루프안에 있는 모든 명령문을 실행한다
하지만 continue문과 break문은 이러한 일반적인 루프의 흐름을 사용자가 직접 제어 할 수 있도록 도와준다
```

1. continue 문
```
continue 문은 루프 내에서 사용하여 해당 루프의 나머지 부분을 건너뛰고, 바로 다음 조건식의 판단으로 넘어가게 해준다
보통 반복문 내에서 특정조건에 대한 예외 처리를 하고자 할때 자주 사용한다
```
![](https://i0.wp.com/www.happyfam.or.kr/ysoh/wp-content/uploads/sites/3/1/cfile26.uf.171F2E264A9A0E4F735073.png?resize=260%2C379)
``` java
// 1부터 100까지의 정수 중에서 5의 배수와 7의 배수를 모두 출력하는 예제

for (int i = 1; i <= 100; i++) {
    if (i % 5 == 0 || i % 7 == 0) {
        System.out.println(i);
    } else {
        continue;
    }
}
```

2. break 문
```
루프 내에서 사용하여 해당 반복문을 완전히 종료시킨 뒤, 반복문 바로 다음에 위치한 명령문을 실행한다
즉 루프 내에서 조건식의 판단 결과와 상관없이 반복문을 완전히 빠져나가고 싶을 때 사용한다
```
![](https://i0.wp.com/www.happyfam.or.kr/ysoh/wp-content/uploads/sites/3/1/cfile26.uf.171F2E264A9A0E4F735073.png?resize=260%2C379)
``` java
// 1부터 100까지의 합을 무한루프를 통해 구하는 예제

int num = 1, sum = 0;

while (true) { // 무한 루프
    sum += num;
    if (num == 100) {
        break;
    }
    num++;
}

System.out.println(sum);
```

3. 이름을 가지는 반복문(break with label)
``` 
일반적인 break문은 단 하나의 반복문만 빠져나게 해준다
따라서 여러 반복문이 중첩된 상황에서 한 번에 모든 반복문을 빠져나가거나, 특정 반벅문까지만 빠져나가고 싶을 때는 다른 방법을 사용해야 한다

이때 사용할 수 있는 방법이 바로 반복에 이름(label)을 설정하는 것이다
가장 바깥쪽 반복문이나 빠져나가고 싶은 특정 반복문에 이름을 설정한 후, break 키워드 다음에 해당 이름을 명시하면 된다
그러면 해당 break 키워드는 현재 반복문이 아닌 해당 이름의 반복문 바로 다음으로 프로그램의 실행 옮겨준다

단, 이때 이름(label)은 가리키고자 하는 반복문의 키워드 바로 앞에 위치해야 한다
```
> c언어나 c++과는 달리 자바에는 goto문이 없다
따라서 이렇게 반복문을 가리키는 이름(label)은 break문이나 continue 문에만 사용될 수 있다

``` java
// 구구단 중에서 2단부터 4단까지를 출력하는 예제

   for (int j = 2; j < 10; j++) {
        if (i == 5) {
            break allLoop;
        }
        System.out.println(i + " * " + j + " = " + (i * j));
    }

}