# Annotation
---
## Lombok
```
Java 라이브러리로 반복되는 getter, setter, toString 등의 메서드 작성 코드를 줄여주는 코드 다이어트 라이브러리이다

복잡하고 반복되는 코드가 줄어듦으로써 코드의 가독성을 높일 수 있고 코딩 생산성 또한 높일 수 있다 다만 개발자마다 호불호가 나뉘는 라이브러리이다

또한 편리성을 제공하는 라이브러리일수록 주의할 사항으로 API 설명과 내부 동작을 어느정도 숙지하고 사용해야한다
```
---
### @Getter/@Setter(접근자/설정자)
`거의 Lombok에서 가장 많이 사용되는 어노테이션`
ex) `xxx`라는 필드에 선언하면 자동으로 `getXxx()`(boolean 타입인 경우, `isXxx()`)와 `setXxx()` 메소드를 생성해준다
```java
@Getter @Setter
private String name;
```
위와 같이 특정 필드에 어노테이션을 붙여주며느 다음과 같이 자동으로 생성된 접근자와 설정자 메소드를 사용할 수 있다

또한, 필드 레벨이 아닌 클래스 레벨에 `@Getter` 또는 `@Setter`를 선언해줄 경우, 모든 필드에 접근자와 설정자가 자동으로 생성된다

---
### @NonNull
 @NonNull은 `메소드나 생성자의 파라미터에 추가하여 null인지 아닌지를 체크`하는 기능을 한다. 만약 @NonNull을 설정한 파라미터의 값이 null로 들어오면 `NullPointerException`을 발생시킨다
```java
@NonNull @Setter
private String id;

obj.setId(null); // NullPointerException 발생
```
---
### @Cleanup
`close()가 필요한 경우` @Cleanup을 사용하면 close() 메소드가 없어도 알아서 close() 해준다
```java
ex)
InputStream
OutputStream
```
> try-wirh-resource 구문과 비슷한 효과를 가진다

---
### @ToString
해당 객체의 정보를 String으로 출력하는 메소드를 직접 만들지 않아도 되고 `toString() 메소드를 자동으로 생성`해준다

`@ToString(exclude="id)`와 같이 `exclude`를 사용하면 toString() 결과에서 id를 제외시킬수 있다

---
### @EqualsAndHashCode
`해당 객체와 동일한지 아닌지를 판단해주는 equal()메소드`와 `해시값을 생성하는 hashCode() 메소드`의 기능을 사용할 수 있게 해준다

callSuper 속성을 통해 eqauls와 hashCode 메소드 자동 생성 시 부모 클래스의 필드까지 감안할지의 여부를 설정할 수 있다

`@EqualsAndHashCode(callSuper=true)`로 설정시 부모 클래스 필드 값들도 동일한지 체크하며, false(기본값)일 경우 자신 클래스의 필드 값만 고려한다

---
### @Data
`@Getter, @Setter, @requiredArgsConstructor,@ToString,@EqualsAndHashCode`를 한번에 설정해주는 어노테이션이다

모든 필드를 대상으로 접근자, 설정자가 자동 생성되고, final 또는 @NonNull 필드 값을 파라미터로 받는 생성자가 만들어지고 toString, equals, hashCode 메소드가 자동으로 만들어진다

---
### @Value
@Data와 거의 동일하지만 `모든 변수가 private, final이 되고, 이로 인해  setter 메소드가 없다`는 차이가 있다

> class에 선언하면 `@Getter @AllArgsConstructor @ToString @EqualsAndHashCode @FieldDefaults(makeFinal=true,level=AccessLevel.PRIVATE)` 어노테이션이 기본적으로 포함된다

---
### @Builder
해당 객체를 Builder 패턴으로 사용할 수 있게 한다

> Builder 패턴 : 복잡한 객체를 생성하는 방법을 정의하는 클래스와 표현하는 방법을 정의하는 클래스를 별도로 분리하여, 서로 다른 표현이라도 이를 생성할 수 있는 동일한 절차를 제공하는 패턴
---
### @Log
말 그대로 `로그를 남겨주는 기능`을 한다
@Log를 사용해도 되지만 @Log4j, @Log4j2,@Slf4j 등등 지원되는 다른 로그 라이브러리를 사용할 수도 있다

---
### @With
@Setter와 유사해 보이지만`객체를 리턴`한다 
만약 파라미터로 받은 값이 이미 `변수에 저장된 값과 동일하면 자기 자신(this)를 리턴`하고, 다르면 파라미터로 받은 값을 `제외한 모든 변수가 동일한 객체를 리턴`한다