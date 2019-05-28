### TIL(2019-05-28)

---

- 인스턴스 변수는 가능한 private으로 선언하자. 
- 메서드를 이용해서 인스턴스 변수에 접근하자. 



- method().method().method()...
  - method를 계속 연결해서 코드를 구현하게 되면 무언가 잘못하고 있는 것이다. '.'을 최대 한 번만 사용하게끔 제약을 걸고 개발하는 연습을 하자.
  - 데이터를 가져와서 사용하려고 하니까 이런 일이 생긴다. 
  - 디미터 법칙
    - 옆에 있는 객체와만 협력하며 일 하자.



- 상속보다는 조합을 이용해 구현하는 것이 유지보수에 유리하다. 
  - `조합은 뭐지?`



- `추상 클래스와 인터페이스를 언제 사용해야 하는지 아직 모르겠다. `



- 객체를 쪼개다보면 via pass만 하는 메서드가 많이 생기는데 거부감을 느끼지 말자. 



- 다형성을 이용해 if문을 제거하면 좋은 점. 새로운 클래스가 추가되었을 때 로직 변경 없이 map에만 클래스를 추가하면 된다. 즉, 다른 로직에 영향을 미치지 않으면서 기능을 확장할 수 있다. 



- `포비 코드 보며 다형성 공부해보기`



```java
class LineCreator implements FigureCreator {
    @Override
    public Figure create(List<Point> points) {
        return new Line(points);
    }
}
    
// 아래의 세 가지는 같은 동작을 하는 코드다.

// 익명 클래스
creators.put(2, new FigureCreator() {
    @Override
    public Figure create(List<Point> points) {
        return new Line(points);
    }
});


// 람다
// 람다로 대체할 수 있는 인터페이스는 메서드가 하나여야 한다. 메서드가 하나인 인터페이스만 람다로 대체해 사용할 수 있다. 함수형 인터페이스?
creators.put(2, (List<Point> points) -> {
    return new Line(points);
});


// ?
// create를 호출하는 것이다. :: 좌측과 같은 값을 반환하는 method를 찾아서 호출하는 것이다. 
creators.put(3, Triangle::new);
```



- static으로 되어있는 클래스 변수는 메모리에 올라오는 순간 초기화가 됨. static 구문은 static 변수가 초기화된 뒤 바로 실행이 됨. 



- 상수값들이 서로 관련되어 있을 경우 enum으로 구현하는 것이 좋다. 

- enum과 class의 차이점. enum인 인스턴스가 하나만 만들어지는 것을 보장한다. class는 여러 개 만들어질 수 있음. 인스턴스가 하나만 만들어지게끔 강제한다. 

- Exception. runtime과 compile exception을 구분할 줄 알아야 하고, 나만의 exception을 만들 줄 알아야 한다. 



- test code에서 throws Exception을 해주면 test를 실행할 수 있음
- exception을 계속 throw해줘서 main같이 바깥 부붙에서 exception 처리를 해주는 것이 일반적이다. 

- RuntimeException도 throws를 해주기도 한다. 생성자를 사용할 때 어떤 exception을 사용하는지 알 수 있기 때문에.





- exception을 중간에 catch를 한 뒤 아무것도 하지 않으면 나중에 왜 에러가 발생하는지 알 수가 없다. 아래와 같이 catch를 해놓고 아무런 처리를 해주지 않으면 안 됨.

```
try {
	// exception이 발생할 수 있는 코드
} catch (IllegalArgumentExcception e) {
	// 아무것도 구현하지 않음.
}
```



- Compile Exception이 좋은가 Runtime Exception이 좋은가?
  - Compile type으로 예외처리를 하다보면 코드가 너무 지저분해진다. 계속 throws 해주니까.
  - 그리고 catch를 했는데도 할 일이 없는 경우가 많이 생긴다.
  - 그러다보니 최근에는 Compile type Exception은 정말 필요할 때만 사용하고 일반적으로는 Runtime Exception을 사용하고 있다. 



