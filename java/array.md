# JAVA
---
## 배열
```
일반적으로 "리스트같은 객체(list-like objects)"라고 기술 됨
배열은 보통 리스트에 저장된 다수의 값들을 포함하고 있는 하나의 객체
배열을 구성하는 각각의 값을 배열 요소(element)라고 하며, 배열에서의 위치를 가리키는 숫자를 인덱스(index)라고 칭함
```

**1. 배열의 선언**   
```
선언방법 
● 타입[] 변수이름;
ex) int[] score;
    String[] name;
● 타입 변수이름[];
ex) int score[];
    String name[];
 ```
배열의 선언은 타입 뒤 혹은 변수이름뒤에 대괄호(`[]`)를 붙히면 됨   

2. 배열의 생성
```java
타입[] 변수이름 = new 타입[길이];
```   
`new`연산자를 사용해 배열의 타입과 길이를 지정하면 메모리에 해당 길이 만큼 영역을 확보함   
생성한 배열은 인덱스(index) 번호를 통해 배열에 접근 할 수 있음      
> 이때 배열의 길이는 최초 생성시 선언한 길이에서 정적이므로 길이의 변경을 원할 때는 새로운 배열을 생성해줘야 함  

**배열의 출력** 
``` java
int[] iArr = {100, 95, 80, 70, 60}

System.out.println(iArr); // [I@7ad041f3
// [I : 배열 integer
// @7ad041f3 : 주소값
```
사실 이값은 메모리에 있는 배열의 주소값(타입@주소)를 가리키는 것   
→ `for 문`을 이용해서 배열 각 원소들을 순화하여 출력하도록 하드코딩 해주거나, 자바에서 제공해주는 `Arrays.toString()`메서드를 이용해서 배열을 문자열 형식으로 만들어 출력할 수도 있음   
``` java
import java.util.Arrays; // Arrays.toString()을 사용하기 위한 import

class Test{
    public static void main(String[] args) {
        int[] iArr = {100, 95, 80, 70, 60}

        // 루프문으로 직접 배열 원소 출력
        for(int i = 0; i < iArr.length; i++){
            System.out.println(iArr[i]);
        }

        // Arrays.toString() 메서드 사용하여 심플하게 바로 출력
        System.out.println(Arrays.toString(iArr)); // [100, 95, 80, 70, 60]
    }
}

** 다만 char 형 배열은 예왼인데, 문자같은 경우 println 으로 바로 출력이 가능
```