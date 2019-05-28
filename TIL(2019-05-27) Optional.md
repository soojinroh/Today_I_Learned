### TIL(2019-05-27)

---

JAVA8을 알아보자!



#### Optional

---

Java8에 Optional 클래스라는 것이 도입되었다고 하는데 왜 도입되었고 언제 쓰고 어떻게 쓰는 건지 알아보자. 



##### Optional 클래스는 무엇인가?

먼저 oracle에서 [Optional 클래스에 대해서 소개](<https://www.oracle.com/technetwork/articles/java/java8-optional-2175753.html>)하기를 

`NullPointerException에 지치셨나요? 그러면 Java8의 Optional을 사용하세요!`라고 한다.

Null Pointer Exception을 방지하려는 기본적인 방법은 다음과 같이 if 방어막을 치는 것이다. 그러나 다음과 같이 if문으로 Null Pointer Exception을 방어하려는 것은 다음과 같은 문제가 발생한다.

1. 가독성이 나빠짐. 
2. if문 하나 빼먹을 확률이 높음
3. error 발생 가능성이 높음

```java
String lunch = "UNKNOWN";

if(starField != null){
  FoodCourt foodCourt = starField.getFoodCourt();
  if(foodCourt != null){
    ChineseFood chineseFood = FoodCourt.getChineseFood();
    if(chineseFood != null){
      lunch = chineseFood.get마라탕();
    }
  }
}
```

 

그래서 Optional이 탄생했다고 한다. 일단 Null 처리를 잘 하기 위해 Optional이 생겼구나라고 생각하면서 Optional에 대해서 알아보자. 



Optional을 사용하면 위의 코드를 다음과 같이 수정해볼 수 있다. 다음과 같이 Optional을 사용해 코드를 수정하면 StarField는 FoodCourt가 있을 수도, 없을 수도 있고 FoodCourt에는 ChineseFood가 있을 수도, 없을 수도 있고, ChineseFood에는 마라탕이 있을 수도, 없을 수도 있게 된다.  즉, 데이터의 존재 유무가 Optional(선택적)하게 되는 것이다. 

```java
public class StarField {
    private Optional<FoodCourt> foodCourt;
    public Optional<FoodCourt> getFoodCourt() {...}
}

public class FoodCourt {
    private Optional<ChineseFood> chineseFood;
    public Optional<ChineseFood> getChineseFood() {...}
}

public class ChineseFood {
    private Optional<마라탕> 마라탕;
    public Optional<마라탕> get마라탕() {...}
}
```

Optional 클래스를 사용하면 개발자는 값이 존재하지 않는 경우에 대해 생각해봐야 한다. 

Optional 클래스를 쓰기만 하면 Null Pointer Exception이 저절로 해결되는 게 아니라 의도하지 않은 null pointer exception을 방지해주는 데에 Optional 클래스의 쓰임이 있는 것이다.



##### Optional 객체를 생성하는 3가지 방법

*Optional 클래스는 `new Optional()`로 객체를 생성하지 않는다!*

1. **empty()** : 데이터가 없는 Optional 객체 생성

2. **ofNullable()** : null이 추가될 수 있는 Optional 객체 생성

3. **of()** : 반드시 데이터가 들어가는 Optional 객체 생성



- **isPresent()** : Optional 클래스가 비어있는지 확인

```java
Optional<String> StarField = Optional.empty();

String starField = null;
Optional<String> sf = Optional.ofNullable(starField);

starField = "starField";
Optional<String> sf = Optional.of(starField);


System.out.println(emptyStr);     // Optional.empty
System.out.println(nullableStr);  // Optional.empty
System.out.println(targetStr);    // Optional[starField]

System.out.println(emptyStr.isPresent());      // false
System.out.println(nullableStr.isPresent());   // false
System.out.println(targetStr.isPresent());     // true


// sf가 null이라면 sf에 접근하지 않더라도 NullPointerException을 던지게 된다. 
starField = null;
Optional<String> sf = Optional.of(starField);

Exception in thread "main" java.lang.NullPointerException
	at java.util.Objects.requireNonNull(Unknown Source)
```



---

공부하다 보니 Lambda, Stream에 대한 이야기가 나와 그것들부터 공부하고 다시 봐야겠다는 생각이 들었다. 

