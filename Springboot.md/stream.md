# Stream
---
## 스트림 API
```
데이터를 추상화하여 다루고, 다양한 방식으로 저장된 데이터를 읽고 쓰기 위한 공통된 방법을 제공
```
배열이나 컬렉션뿐만 아니라 파일에 저장된 데이터도 모두 같은 방법으로 다룰 수 있게 된다

---
### 특징
- `원본 데이터를 변경하지 않는다`
- 외부 반복을 통해 작업하는 컬렉션과는 달리 `내부 반복(internal iteration)`을 통해 작업을 수행한다
- 지사용이 가능한 컬렉션과는 달리 `단 한번만 사용`할 수 있다
- 필터-맵(filter-map) 기반의 API를 사용하여 `자연(lazy) 연산을 통해 성능을 최적화`한다
- `parallelStream() 메서드를 통한 손쉬운 병렬 처리`를 지원한다
---
### 동작 흐름
세 가지 단계에 걸쳐서 동작한다
```
1. 스트림의 생성
2. 스트림의 중개 연산 (스트림의 변환)
3. 스트림의 최종 연산 (스트림의 사용)
```
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKvMlO%2FbtrrjZuH7g6%2FcbwD9VAKryzLDu3VTIujuK%2Fimg.png)

---
### 스트림의 생성
다양한 데이터소스에서 생성할 수 있다

#### 컬렉션
자바에서 제공하는 `모든 컬렉션의 최고 상위 조상`인 Collections 인터페이스에는 `stream() 메서드가 정의`되어 있다
따라서 Collecion 인터페이스를 구현한 `모든 List와 Set 컬렉션 클래스에서도 stream() 메서드로 스트림을 생성`할 수 있다

#### 배열
배열에 관한 스트림을 생성하기 위해 `Arrays 클래스에는 다양한 형태의 stream() 메서드가 클래스 메서드로 정의`되어있다
이러한 스트림은 `java.util.stream`패키지의 `inStream, LongStream, DoubleStream`인터페이스로 각각 제공된다

#### 가변 매개변수
stream 클래스의 `of() 메서드`를 사용하면 `가변 매개변수(variable parameter)를 전달`받아 스트림을 생성할 수 있다

#### 지정된 범위의 연속된 정수
지정된 범위의 연속된 정수를 스트림으로 생성하기 위해 IntStream나 LongStream 인터페이스에는 `range(), rangetClose() 메서드가 정의`되어 있다

- `range(int startInclusive, int endExclusive)` : 명시된 시작 정수를 포함하지만, 명시된 마지막 정수는 포함하지 않는 스트림을 생성
- `rangeCloase (int startInclusive, int endExclusive)` : 명시된 시작 정수뿐만 아니라 명시된 마지막 정수까지도 포함하는 스트림을 생성

#### 특정 타입의 난수들
특정 타입의 난수로 이루어진 스트림을 생성하지 위해 Random 클래스에는 `ints(), longs(), doubles()`와 같은 메서드가 정의 되어 있다

- 이 메서드들은 매개변수로 스트림의 크리를 `long 타입으로 전달`받을 수 있다
- 만약 매개변수를 전달받지 않으면 `크기가 정해지지 않은 무한 스트림(infinite stream)을 반환`한다
    > 이때에는 `limit()`메서드를 사용하여 따로 스트림의 크기를 제한해야함