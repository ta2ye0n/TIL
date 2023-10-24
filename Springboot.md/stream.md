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

#### 람다 표현식
람다 표현식을 매개변수로 전달받아 해당 람다 표현식에 의해 반환되는 값을 요소로 하는 무한 스트림을 생성하기 위해 Strema 클래스에는 `interate(), generate()`메서드가 정의되어 있다

- `interate(T seed, UnaryOperator<T>f)` : 시드로 명시된 값을 람다 표현식에 사용하여 반환된 값을 다시 시드로 사용하는 방식으로 무한스트림을 생성한다

- `generate(Supplier<T> s)` : 매개변수가 없는 람다 표혀식을 사용하여 반환된 값으로 무한 스트림을 생성한다

#### 파일
파일의 한 행(line)을 요소로 하는 스트림을 생성하기 위해 java.nio.file.Files 클래스에는 `lines()`메서드가 정의되어있다   
또한, java.io.BufferedReader 클래스의 lines() 메서드를 사용하면 파일뿐만 아니라 다른 입력으로부터도 데이터를 `행(line)`단위로 읽어 올 수 있다

#### 빈 스트림
아무 요소도 가지지 않는 빈스트림은 Stream 클래스의 `empty()`메서드를 사용하여 생성할 수 있다

---
### 중개 연산 (스트림의 변환)
- 스트림 API에 의해 생성된 초기 스트림은 중개 연산을 통해 또 다른 스트림으로 변환된다

- 중개 연산은 스트림을 전달받아 `스트림으로 반환`하므로, 중개 연산은 `연속으로 연결해서 사용할 수 있다`
- 스트림의 중개 연산은 필터(filter) - 맵(map) 기반의 api를 사용함으로써 `지연(lazy)연산을 통해 성능을 최적화`할 수 있다

```
대표적인 중개 연산
1. 스트림 필터링 : filter(), distinct()
2. 스트림 변환 : map(), flatMap()
3. 스트림 제한 : limit(), skip()
4. 스트림 정렬 : sorted()
5. 스트림 연산 결과 확인 : peek()
```

#### filter()
```java
어떤 조건으로 Stream의 요소들을 필터링한다

Stream<T> filter(Predicate<? super T> predicate);
```
필요하다면 다른 조건으로 여러 번 사용할 수도 있다

#### distinct()
```java
중복되는 데이터가 제거된 stream을 리턴한다

Stream<T> distinct();
```
참고로, 중복 요소를 확인할 때, 동일한 객체인지 판단하는 기준은 `Object.equals(Object)`메서드이다

#### map()
```
데이털ㄹ 변형하는데 사용한다
데이터에 해당 함수가 적용된 결과물을 제공하는 stream을 리턴한다
```
요소를 어떻게 변경할지 설정할 수 있다
```java
<R> STream<R> map(Function<? super T, ? extends R> mapper);
```

#### flatMap()
```
Map + Flatten
평탄화
복잡한 자료 구조에 저장된 요소들을 단순한 자료구조로 변환한다
```
```java
<R> Stream<R> flatMap(Function<? super T, ?extends Stream<? extends R>> mapper);
```

#### limit()
```
일정 개수만큼만 데이터를 가져와서 새로운 스트림을 생성하고 리턴한다
```
```java
Stream<T> skip(long n)
```
#### skip()
```
일정 개수만큼 요소를 건너띄고, 그 이후의 요소들로만 스트림을 생성하고 리턴한다
```
```java
Stream<T> limit(long maxSize)
```

`skip()`과 `limit()`은 반대된다

#### Sorted()
```java
데이터가 순서대로 정렬된 스트림을 리턴한다

Stream<T> sorted();
Stream<T> sorted(Comparator<? super T> comparator);
```
sorted()는 지정된 Comparator로 스트림을 정렬하는데, Comparator 대신 int 값을 반환하는 람다식을 사용하는 것도 가능하다   
Comparator를 지정하지 않으면 스트림 요소의 기본 정렬 기준(Coparable)으로 정렬하고 스트림의 요소가 Comparable을 구현한 클래스가 아니면 예외가 발생한다

#### peek()
```java
연산과 연산 사이에 올바르게 처리되었는지 확인할 때 사용된다

Stream<T> peek(Consumer<? super T> action);
```
`peek()`와 `forEach()`를 혼동해서는 안된다   
`forEach()` 메서드는 최종 연산이기 때문에 결과를 확인할 수 있으나 `peek()`는 중간 연산이기 때문에 어떠한 최종 연산도 하지 않으면 아무것도 확인할 수 없다
> 보통 잘 사용되지 않는 메서드이다
---