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
