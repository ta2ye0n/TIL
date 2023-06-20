# java
---
## 제어문
---
### 조건문
```
주어진 조건식의 결과에 따라 별도의 명령을 수행하도록 제어하는 명령문이다

자바에서 사용하는 대표적인 조건문의 형태
1. if 문
2. if / else 문
3. if / else if / else 문
4. switch 문
```
1.  if 문   
```
조건식의 결과가 참(true)이면 주어진 명령문을 실행하며, 거짓(false)이면 아무것도 실행하지 않는다
```
**if 문 순서도**   
![](https://t1.daumcdn.net/cfile/tistory/11699D474F97B03608)   
``` java
if (조건식) {
    조선식의 결과가 참일 때 실행하고자 하는 명령문
}

//ex) if 문을 사용하여, 해당 문자가 영문 소문자인지를 확인하는 예제
if (ch >= 'a' && ch <= 'z') {

    System.out.println("해당 문자는 영문 소문자입니다.");

}
```
> if 문에서 실행될 명령문이 한 줄 뿐이라면 중괄호 ({})를 생략할 수 있다   
2. if / else 문
``` 
if 문과 함께 사용하는 else문은 if 문과는 반대로 주어진 조거식의 결과가 거짓(false)이면 주어진 명령문을 실행한다
```
**if else 순서도**   
![](https://blog.kakaocdn.net/dn/bPi9L3/btq59OHPH5a/tEZeNzaEUtKPzEdxRqvYmK/img.png)
``` java
if (조건식) {
    조건식의 결과가 참일 때 실행고자 하는 명령문;
} else {
    조건식의 결과가 거짓일 때 실행하고자 하는 명령문;
}
```
3. if / else if / else 문
```
if / else if / else 문은 마치 새로운 구문처럼 보이지만, 사실은 두개의 if / else 문이 연달아 나온 것 뿐이다
조거식을 여러 개 명시할 수 있으므로 중첩된 if 문을 좀더 간결하게 표현할 수 있다
```
**if / else if / else 문 순서도**   
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbRPb4j%2Fbtq6hS3EmuQ%2Fo0GWROZSFwlxwuHsPSPkTK%2Fimg.png)   
``` java
if (조건식1) {
    조건식1의 결과가 참일 때 실행하고자 하는 명령문;
} else if(조건식2) {
    조건식2의 결과가 참일 때 실행하고자 하는 명령문;
} else {
    조건식1의 결과도 거짓이고, 조건식2의 결과도 거짓일 때 실행하고자 하는 명령문;
}

이때 else if문은 여러번 나와도 상관없지만, if 문과 else 문은 단 한 번만 나올 수 있다

// if / else if / else 문을 사용하여, 해당 문자가 영문 소문자나 영문 대문자인지, 아니면 영문자가 아닌지를 확인하는 예제
if (ch >= 'a' && ch <= 'z') {

    System.out.println("해당 문자는 영문 소문자입니다.");

} else if (ch >= 'A' && ch <= 'Z') {

    System.out.println("해당 문자는 영문 대문자입니다.");

} else {

    System.out.println("해당 문자는 영문자가 아닙니다.");

}
```
>if / else if / else 문에서도 실행될 명령문이 한 줄뿐이라면 중괄호({})를 생략할 수 있습니다.

4. switch 문
```
if / else 문과 마찬가지로 주어진 조건 값의 결과에 따라 프로그램이 다른 명령을 수행하도록 하는 조건문

이러한 switch 문은 if / else 문보다 가독성이 더 좋으며, 컴파일러가 최적화를 쉽게 할 수 있어 속도 또한 빠른 편이다

하지만 자바에서는 switch 문의 조건 값으로는 int형으로 승격할 수 있는(integer promotion) 값만이 사용될 수 있다
```
``` java
switch (조건 값) {
    case 값1:
        조건 값이 값1일 때 실행하고자 하는 명령문;
        break;
    case 값2:
        조건 값이 값일2 때 실행하고자 하는 명령문;
        break;
    ...
    default:
        조건 값이 어떠한 case 절에도 해당하지 않을 때 실행하고자 하는 명령문;
        break;
}

default절은 조건 없이 위에 나열된 어떠한 case 절에도 해당하지 않을 때만 실행된다
이 절은 반드시 존재해야 하는 것은 아니며 필요할 때만 선언할 수 있다
```
``` java
// 해당 문자가 영문자 모음인지를 확인하는 예제
switch (ch) {

    case 'a':

        System.out.println("해당 문자는 'A'입니다.");

        break;

    case 'e':

        System.out.println("해당 문자는 'E'입니다.");

        break;

    case 'i':

        System.out.println("해당 문자는 'I'입니다.");

        break;

    case 'o':

        System.out.println("해당 문자는 'O'입니다.");

        break;

    case 'u':

        System.out.println("해당 문자는 'U'입니다.");

        break;

    default:

        System.out.println("해당 문자는 모음이 아닙니다.");

        break;

}
```
- default 절은 위의 예제와 같이 맨 마지막에 위치하는 것이 일반적이지만, case 절 사이에 위치해도 상관없다

- 각 case 절 및 default 절은 반드시 break 키워드를 포함하고 있어야한다
```
break 키워드는 조건 값에 해당하는 case 절이나 default 절이 실행된 뒤에 전체 switch 문을 빠져나가게 해준다
만약 break 키워드가 없다면, 조건에 해당하는 switch문의 case 절 이후의 모든 case 절이 전부 실행될 것이다
```
``` java
// break 키워드를 모두 삭제한 예제
switch (ch) {

    case 'a':

        System.out.println("해당 문자는 'A'입니다.");

    case 'e':

        System.out.println("해당 문자는 'E'입니다.");

    case 'i':

        System.out.println("해당 문자는 'I'입니다.");

    case 'o':

        System.out.println("해당 문자는 'O'입니다.");

    case 'u':

        System.out.println("해당 문자는 'U'입니다.");

    default:

        System.out.println("해당 문자는 모음이 아닙니다.");

}

출력 결과
해당 문자는 'I'입니다.
해당 문자는 'O'입니다.
해당 문자는 'U'입니다.
해당 문자는 모음이 아닙니다.
```
> break 키워드가 없으면, 조건 값에 해당하는 case 절뿐만 아니라 그 이후에 등장하는 모든 case 절과 default 절이 전부 실행된다
``` java
// 조건으로 여러개의 case 절을 사용하여 여러 개의 조건 값을 한번에 검사하는 예제
switch (ch) {

    case 'a':

    case 'e':

    case 'i':

    case 'o':

    case 'u':

        System.out.println("해당 문자는 소문자 모음입니다.");

        break;

    case 'A':

    case 'E':

    case 'I':

    case 'O':

    case 'U':

        System.out.println("해당 문자는 대문자 모음입니다.");

        break;

    default:

        System.out.println("해당 문자는 모음이 아닙니다.");

        break;

}
```