### TIL(2019-05-22) String.matches와 Matcher.matches

---

####  String.matches와 Matcher.matches

- String.matches는 내부적으로 Pattern.matches(regex, str)를 호출해 사용한다.
- String.matches는 `매번` 호출할 때마다 `패턴을 다시 컴파일`하는 낭비가 발생한다.
- Pattern.compile은 pattern을 컴파일하기 때문에 Matcher.matches를 사용하면 매번 pattern을 다시 컴파일하는 것을 피할 수 있다.

```java
 String.matches
 
 2110       public boolean matches(String regex) {
 2111           return Pattern.matches(regex, this);
 2112       }
```



```java
java.util.regex.Pattern.matches

public static boolean matches(String regex, CharSequence input) {
    Pattern p = Pattern.compile(regex);
    Matcher m = p.matcher(input);
    return m.matches();
}
```



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



```java
java.util.regex.Pattern.compile

public static Pattern compile(String regex) {
    return new Pattern(regex, 0);
}
```



```java
java.util.regex.Matcher.matches

public boolean matches() {
    return match(from, ENDANCHOR);
}
```



- 즉, 여러 번 사용할 때는 **Matcher.matches**를 사용하자!

```java
Pattern p = Pattern.compile(regex);
Matcher m = p.matcher(input);
return m.matches();
```



- 여담이지만, 정규표현식을 따로 모아두는 클래스를 만드는 것보다는 정규표현식이 실제로 사용되는 곳에 있는 것이 좋다고 한다. 그렇게 해야 유지보수하기가 쉽다,고 한다.

---

참고

- <https://stackoverflow.com/questions/2469244/whats-the-difference-between-string-matches-and-matcher-matches/2469275>

