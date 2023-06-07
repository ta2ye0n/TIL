# java
---
## 배열
---
### 다차원 배열
```
2차원 이상의 배열을 의미하며, 배열요소로 또 다른 배열을 가지는 배열을 의미
간단하게 1차원 배열은 배열 요소로 '단일값'을 가지는 배열이라면 2차원 배열은 배열 요소로 '1차원 배열'을 가지는 배열이며, 3차원 배열은 배열요소로 2차원 배열을 가지는 배열 인 식으로 순차적으로 생각하면 됨
```   
> 메모리의 용량이 허용하는 한 차원의 제한은 없지만 주로 1차원과 2차원 배열이 많이 사용됨   
---
**2차원 배열 생성**
```
엑셀과 같은 테이블 형태의 데이터를 담기위해 사용하는 배열
테이블의 데이터는 행(row)과 열(column)로 구성되어 있음
```
**2차원 배열 선언법**   
1차원배열은 대괄호 []를 1번먼만 썼다면, 2차원은 대괄호 [][] 를 2번 쓰면 됨   
ex)
``` java
// 배열을 선언하고 따로따로 데이터를 적재
int[][] score = new int[4][3];
score[0][1] = 10;
score[0][1] = 20;
...
score[1][0] = 10;
score[1][1] = 20;
...
score[2][0] = 10;
score[2][1] = 20;
...
score[3][0] = 10;
score[3][1] = 20;

// 혹은 한번에 2차원 배열을 지정하여 선언할 수 있다.
int[][] arr2 = {
                  {10,20,30},
                  {10,20,30},
                  {10,20,30},
                  {10,20,30}
                }
```   
**2차원 배열 출력**   
2차원 배열 출력도 1차원 같이 for 문으로 배열을 순화해 출력하도록 지정
``` java
int[][] arr2 = {
                  {10,20,30},
                  {40,50,60},
                  {70,80,90},
                  {100,200,300}
                };
                
for(int i = 0 ; i < number.length ; i++) {	// 먼저 열 부분을 순회하고
    for(int j = 0 ; j < number[i].length ; j++) { // 행 부분을 순회하며 각 원소를 출력
        System.out.print(number[i][j]);
    }
}
```
`Arrays.deeptoString()` 메서드를 통해 2차원 배열을 한방에 출력할 수 있음
``` java
// 1차원 배열 한방 출력
int[] arr = {0,1,2,3,4};
System.out.println(Arrays.toString(arr)); // [0, 1, 2, 3, 4]

// 2차원 배열 한방 출력
int[][] arr2 = {
                  {10,20,30},
                  {40,50,60},
                  {70,80,90},
                  {100,200,300}
                };
System.out.println(Arrays.deepToString(arr2)); // [[10, 20, 30], [40, 50, 60], [70, 80, 90], [100, 200, 300]]
```
**2차원 배열 비교**   
`Arrays.deepEquals()` 메서드를 사용하면 됨
``` java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        String[][] arr1 = { 
            { "홍길동", "임꺽정" },
            { "박혁거세", "주몽", "고담덕" }
        };
        String[][] arr2 = { 
            { "홍길동", "임꺽정" },
            { "박혁거세", "주몽", "고담덕" }
        };
        String[][] arr3 = { 
            { "홍길동" },
            { "주몽", "고담덕" }
        };

        System.out.println("arr1 == arr2 : " + Arrays.deepEquals(arr1, arr2)); // arr1 == arr2 : true

        System.out.println("arr1 == arr3 : " + Arrays.deepEquals(arr1, arr3)); // arr1 == arr3 : false
    }
}
```
---
### 배열 종류
**가변 배열**   
```
2차원 배열이 테이블 형태라고 해서 반드시 가로와 세로가 똑같은 정방 행렬일 필요가 없음
자바에서의 다차원 배열은 마지막 차수의 길이를 다르게 지정할 수 있기 때문에, 각 요소로 들어가는 1차원 배열의 길이를 각기 다르게 해도 2차원 배열 데이터를 생성하는데 문제 없음
```
ex)
``` java
int[][] score = {
	{100, 100, 100, 100},
    {20, 20, 20},
    {30, 30},
    {40, 40},
    {50, 50, 50}
}
```   
**객체 배열**   
```
보통 배열에 정수나 문자를 적재하여 꺼내 써왔을 것인데, 객체 자체도 배열에 넣어 사용할 수 있음
객체 역시 하나의 자료형으로 취급
``` 
``` java
// myObject 클래스
class myObject{
    int id;
    String description;

    myObject(int id, String description) {
        this.id = id;
        this.description = description;
    }
}

// myObject 클래스를 담을 수 있는 공간 3개 크기의 객체 배열 생성
myObject[] arrayObj = new myObject[3];

// 객체 배열 초기화
arrayObj[0] = new myObject(101, "first");
arrayObj[1] = new myObject(102, "second");
arrayObj[2] = new myObject(103, "third");

// 객체 배열 사용
System.out.println(arrayObj[0].description); // "first  array, John"

/* ************************************ */

// 객체 배열 선언 + 초기화 한번에
myObject[] arrayObj2 = {
    new myObject(101, "first"), 
    new myObject(101, "second"), 
    new myObject(101, "third")
};
```