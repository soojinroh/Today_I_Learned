### 정적 메소드 (Static method)

---

우아한테크코스 레벨1 두 번째 미션인 Ladder Game을 구현한 뒤 다음과 같은 피드백을 받았다.

![](https://github.com/soojinroh/Today_I_Learned/blob/master/img/20190522190156.png?raw=true)



AppController Class에서 play()메서드를 이용해 전체 게임을 진행시키는 구조인데, 굳이 `new AppController()`로 객체를 생성하지 말고 play() 메서드를 정적메서드로 구현해서 사용하는 것이 좋겠다는 피드백이었다.



아하! 하고 play() 메서드에 static 키워드를 추가하고 `new AppController().play()`를 `AppController.play()`로 바꾸려는데 '정적 메서드는 언제, 왜 때문에 사용해야하는 거지?'라는 의문이 들어 조금 알아보기로 했다. 조금만.

---

우선 정적 메서드란 무엇인가?

정적 메서드란 `클래스 객체를 생성하지 않은채로 호출이 가능하며 인스턴스에서는 호출할 수 없는 메서드`이다. 



즉, Pikachu 객체를 생성하지 않고 `Pikachu.attack();`과 같이 사용 가능하지만 `Pikachu pika = new Pikachu();`로 Pikachu 객체를 생성한 뒤에 `pika.attack();`과 같이는 사용할 수 없다는 뜻이다.



```java
public class Pikachu {
    
    private int level = 1;
    
    public static void attack() {
        System.out.println("몸통박치기!");
    }
}


public class Pocketmon {
	public static void main(String[] args) {
		Pikachu.attack();
		
		Pikachu pika = new Pikachu();
		pika.attack(); // 놉. 컴파일 에러
	}
}


```



static method는 말 그대로 정적이기 때문에 클래스가 메모리에 올라갈 때 생성된다. 이미 메모리에 올라갔기 때문에 인스턴스가 생성되지 않은 상태에서는 사용이 가능한 반면 인스턴스에서는 사용할 수 없다. (Pikachu.attack()은 되지만 pika.attack()은 안 된다.)



static method는 메모리에 올라와 있지만 인스턴스의 필드나 메서드는 인스턴스가 생성되어야 메모리에 올라가기 때문에 static method의 입장에서 인스턴스 필드와 메서드는 아직 존재하지 않는 것이나 다름없다. 



Pikachu 인스턴스가 없는데 static method가 Pikachu의 level 변수를 사용할 수는 없지 않은가. 



정적 메서드의 대표적인 특징은 이와 같은데 그러면 언제 정적 메서드를 사용하고 언제 사용하지 않는 것인가? 다음과 같은 조건을 만족하면 된다고 한다.

1. 유틸리티 클래스에서 만들어지는 경우.
2. 정적 메서드가 인스턴스의 변수를 사용하지 않는 경우.
3. 인스턴스가 없어도 되는 경우. (인스턴스 생성에 의존하지 않는 경우)
4. 오버라이딩되지 않는 경우.



음, 즉 `new Class()`로 **객체를 생성하지 않아도 되고** 오버라이딩을 하는 등 **메서드에 변화를 주지 않고** 인**스턴스의 변수를 사용하지 않는 경우**에는 정적 메서드로 만들 수 있다! 때문에 유틸리티 메서드를 만드는 데 주로 사용된다고 한다. Like Math.random(); 



- "인스턴스가 생성되지 않았는데도 해당 메서드를 호출해서 사용하는 게 괜찮은 것 같니?"라는 질문에 "넵"이라는 답이 나오면 정적 메서드로 만들어도 된다는 글을 보았다.

- 만들 수 있는 것`과 `만들어야 한다`는 차이가 있지만 사실 이부분은 잘 모르겠다.

- 정적 메서드는 상태를 가지고 있지 않기 때문에 객체 지향의 개념에 위배된다는 글을 보았다. (객체지향의 사실과 오해라는 책에서 객체는 상태와 행동, 식별자, 협력 등이 중요하다고 했다. 근데 정적 메서드는 행동만 있으니 너무나 객체지양적이다.)



> TDD왕이자 자바수호신인 포비님은 
>
> - static method가 테스트하기 어려우며 객체지향적이지 않기 때문에 사용을 최소화 하는 것이 좋으며
> - Spring과 같이 DI를 지원하는 프레임워크가 등장하면서 Singleton 패턴의 필요성이 줄어들었다고 하신다.(의존성 주입이라는 말이 얼핏 떠오르지만 역시나 무엇인지는 잘 모른다.)
> - 포비는 거의 유틸성 라이브러리인 경우에만 사용한다고 한다.
> - 상태를 가질 필요가 없는 부분에서는 static method로 구현해도 무방하다고 한다.



---

다음의 페이지를 참고해서 정리를 했다.

- <https://mygumi.tistory.com/253>
- <https://stackoverflow.com/questions/2671496/java-when-to-use-static-methods>
- <https://www.yegor256.com/2014/05/05/oop-alternative-to-utility-classes.html>
- <https://www.slipp.net/questions/58>

