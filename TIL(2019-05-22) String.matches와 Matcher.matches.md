### TIL(2019-05-22) String.matches와 Matcher.matches

---

####  String.matches와 Matcher.matches

- String.matches는 내부적으로 Pattern.matches(regex, str)를 호출해 사용한다.
- String.matches는 `매번` 호출할 때마다 `패턴을 다시 컴파일`하는 낭비가 발생한다.
- Pattern.compile은 pattern을 컴파일하기 때문에 Matcher.matches를 사용하면 매번 pattern을 다시 컴파일하는 것을 피할 수 있다.



String.matches는 내부적으로 Pattern.matches를 사용하고 있다.

```java
 String.matches
 
 2110       public boolean matches(String regex) {
 2111           return Pattern.matches(regex, this);
 2112       }
```



Pattern.matches는 매번 실행될 때마다 Pattern.compile을 호출해 컴파일을 실행한다.

즉, String.matches를 실행할 때마다 Pattern.matches가 실행되고, 따라서 매번 re-compile된다. 이러면, 안 된다. 

```java
java.util.regex.Pattern.matches

public static boolean matches(String regex, CharSequence input) {
    Pattern p = Pattern.compile(regex);
    Matcher m = p.matcher(input);
    return m.matches();
}
```



pattern.matches에서 Pattern.matcher를 사용하길래 Pattern.matcher는 뭔지 따라가봤는데, 뭐. 모르겠다.

```java
java.util.regex.Pattern.matcher

public Matcher matcher(CharSequence input) {
    if (!compiled) {
        synchronized(this) {
            if (!compiled)
                compile();
        }
    }
    Matcher m = new Matcher(this, input);
    return m;
}
```



Pattern.compile은 이렇다.

```java
java.util.regex.Pattern.compile

public static Pattern compile(String regex) {
    return new Pattern(regex, 0);
}
```



Matcher.matches는 요렇게 되어있다. matches()도 더 파고 들어가보려다가 어려워서 여기까지만.

```java
java.util.regex.Matcher.matches

public boolean matches() {
    return match(from, ENDANCHOR);
}
```



그래서 뭘 어떻게 사용하는 게 좋은 것인가?

한 번만 할 때는 String.matches나 Matcher.matches나 효율면에서 큰 차이가 없지만 여러 번 사용할 때는 **Matcher.matches**를 사용하자!

```java
Pattern p = Pattern.compile(regex);
Matcher m = p.matcher(input);
return m.matches();
```



- 여담이지만, 정규표현식을 따로 모아두는 클래스를 만드는 것보다는 정규표현식이 실제로 사용되는 곳에 있는 것이 좋다고 한다. 그렇게 해야 유지보수하기가 쉽다,고 한다.

---

참고

- <https://stackoverflow.com/questions/2469244/whats-the-difference-between-string-matches-and-matcher-matches/2469275>

