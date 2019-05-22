### TIL(2019-05-22) Arrays.asList()

---

#### Arrays.asList()

다음과 같은 피드백을 받고, Arrays.asList()에 대해서 조금 찾아보았다.

![20190522204207](https://github.com/soojinroh/Today_I_Learned/blob/master/img/20190522204207.png)



1. Arrays.asList()는 **java.Arrays.ArrayList** 클래스를 리턴하는 것으로 **java.util.ArrayList** 클래스와는 다르다.



2. java.util.Arrays.ArrayList는 원소를 추가하는 메서드를 가지고 있지 않기 때문에 **Arrays.asList()가 리턴한 ArrayList는 사이즈를 바꿀 수 없다.**

```java
String[] arr = {"가", "나", "다"};
List<String> strList = Arrays.asList(arr);
		
strList.add("우와우와");
		
System.out.println(strList);


Exception in thread "main" java.lang.UnsupportedOperationException
	at java.util.AbstractList.add(Unknown Source)
	at java.util.AbstractList.add(Unknown Source)
	at practice.abc.main(abc.java:12)
```



3. 아래와 같은 방법을 사용하면 배열을 요소를 추가할 수 있는 리스트로 변환하여 사용할 수 있다.

```List<String> newStrList = new ArrayList<>(Arrays.asList(arr));```



---

참고

- <https://bestalign.github.io/2015/08/31/top-10-mistakes-java-developers-make-1/>
