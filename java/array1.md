# JAVA
---
## 배열
---
### 1차원 배열
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

**배열 복사**   
```
배열은 한번 선언되고 나면 공간 자체를 직접 늘릴수는 없기 때문에 간접적인 방법으로 배열을 확장해야 됨 
따로 공간이 큰 배열을 새로 만드렁 주고 기존의 배열의 내용을 새로 만든 배열에 복사하는 식으로 하여 배열을 간접적으로 확장하는 방법
다만, 이러한 작업은 비용이 많이 들기 때문에 처음부터 배열의 길이를 넉넉하게 잡는 것이 베스트
```
방법   
● for 문으로 순회해 직접 한땀 한땀 복사하도록 지정   
● 자바에서 제공해주는 `System.arraycopy()`메서드나 `Arrays.compyOf()`메서드를 사용   
>Arrays.copyOf는 System.arraycopy를 래핑한 함수일뿐임 
즉, 둘이 동일하다고 보면됨
다만 Arrays.copyOf 가 좀더 직관적이라 이쪽이 더 많이 사용되는 편   
``` java
import java.util.Arrays;

class Test{
	public static void main(String[] args) {
        int[] arr1 = {10, 20, 30, 40, 50};

		int[] arr2 = new int[arr1.length * 2]; // 우선 초기 배열보다 길이가 두배인 새로운 배열을 선언
        
        // 루프문으로 순회하여 복사
        for(int i = 0 ; i < arr1.length ; i++) { // arr1의 길이만큼 반복문 실행	
            arr2[i] = arr1[i];	// arr1배열의 원소값을 순회하며 arr2배열에 저장
        }
        arr1 = arr2; // 원래의 배열을 가리키고있던 참조변수 arr1이 새로 복사된 arr2 배열을 가리키도록 한다.
	}
}
```   
``` java
class Test{
	public static void main(String[] args) {
        int[] arr1 = {10, 20, 30, 40, 50};

        int[] arr2 = new int[arr1.length * 2]; // 우선 초기 배열보다 길이가 두배인 새로운 배열을 선언

        // System.arraycopy() 메서드 사용
        System.arraycopy(arr1, 0, arr2, 0, arr1.length); // arr1의 index 0부터 arr1.length 전체 길이 만큼 arr2의 index 0 부터 붙여넣는다.
        /*
        - 첫번째 인자 : 복사할 배열
        - 두번째 인자 : 복사를 시작할 배열의 위치
        - 세번째 인자 : 붙여넣을 배열
        - 네번째 인자 : 복사된 배열값들이 붙여질 시작위치 (차례대로 붙여 넣어진다)
        - 다섯번째 인자 : 지정된 길이만큼 값들이 복사된다.
        */
	}
}
```
``` java
import java.util.Arrays;

class Test{
	public static void main(String[] args) {
        int[] arr1 = {10, 20, 30, 40, 50};

        int[] arr2 = new int[arr1.length * 2]; // 우선 초기 배열보다 길이가 두배인 새로운 배열을 선언

		// Array.copyOf() 메서드 사용     
        arr2 = Arrays.copyOf(arr1, arr1.length); // arr1 배열을 arr1.length 전체 길이만큼 전체 복사해서 arr2에 할당
        System.out.println(Arrays.toString(arr2)); // [10, 20, 30, 40, 50]
        
        arr2 = Arrays.copyOfRange(arr1, 1, 3); // 배열요소 시작점, 끝점 지정. 1, 2 만 복사해서 반환
        System.out.println(Arrays.toString(arr2)); // [10, 20, 30, 40, 50]
	}
}
```
> for 문 보다 메서드를 이용하는게 거의 두배 정도로 빠르게 복사한다고 함   

**배열 정렬**   
```
Arrays.sort() 메서드를 이용해 배열을 정렬할 수 있음

이때 정렬된 배열을 새로 반환하는 것이 아닌, 자기 자신 배열을 정렬시킴
```
``` java
import java.util.Arrays;

class Test{
	public static void main(String[] args) {
        int[] arr = { 3,2,0,1,4 };

        // 오름차순 정렬
        Arrays.sort(arr); // 자기 자신 배열을 정렬 시킴 (정렬된 배열을 반환하는 것이 아니다)
        System.out.println(Arrays.toString(arr)); // [0,1,2,3,4]

        // 내림차순 정렬 
        Arrays.sort(arr, Collections.reverseOrder()); // 배열을 내림차순으로 정렬할 때는 Collections 클래스의 reverseOrder() 함수를 사용
        System.out.println(Arrays.toString(arr)); // [4,3,2,1,0]

        // 배열 일부부만 정렬
        int[] arr = { 3,2,0,1,4 };
        Arrays.sort(arr, 0, 3); // 배열 요소 0, 1, 2 만 정렬
        System.out.println(Arrays.toString(arr)); // [0, 2, 3, 1, 4]
	}
}
```

**배열 비교**    
```  
만일 두개의 배열의 구성이 같은지 같지 않은지 비교하기 위해서 일일히 for문으로 순화하여 원소를 비교하는 식으로도 구현을 할 수 있지만,
Arrays.equals() 메서드를 이용하면 간단히 처리 할 수 있음
```
``` java
 import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        String[] arr1 = { "홍길동", "임꺽정", "박혁거세", "주몽", "고담덕" };
        String[] arr2 = { "홍길동", "임꺽정", "박혁거세", "주몽", "고담덕" };
        String[] arr3 = { "홍길동", "임꺽정", "박혁거세", "주몽" };

        System.out.println("arr1 == arr2 : " + Arrays.equals(arr1, arr2)); // arr1 == arr2 : true
        
        System.out.println("arr1 == arr3 : " + Arrays.equals(arr1, arr3)); // arr1 == arr3 : false
    }
}
```  