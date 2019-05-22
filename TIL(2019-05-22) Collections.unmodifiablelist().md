### TIL(2019-05-22) Collections.unmodifiablelist()

---

![20190522202935](https://github.com/soojinroh/Today_I_Learned/blob/master/img/20190522202935.png)

Collections.unmodifiablelist()는 처음들어보았고, 알아보았다.



#### Collections.unmodifiablelist()

![20190522202139](https://github.com/soojinroh/Today_I_Learned/blob/master/img/20190522202139.png)



인자로 받은 리스트를 'read-only'한 list로 return하는 메서드인 것 같다. 즉, Collections.unmodifiablelist()로 만들어진 list는 get()만 할 수 있지 add()나 remove()가 안 된다. 'read-only'하다.



아래의 코드로 테스트해보니 `Collections.unmodifiableList()로 만들어진 list2에 add를 시도`하자 `UnsupportedOperationException`이 발생하였다.

```java
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public class ListTest {
	public static void main(String[] args) {
		List<String> list1 = Arrays.asList("하나", "둘", "셋");
		List<String> list2 = Collections.unmodifiableList(list1);
		
		System.out.println(list2.get(0));
		list2.add("넷");
	}
}


하나
Exception in thread "main" java.lang.UnsupportedOperationException
	at java.util.Collections$UnmodifiableCollection.add(Unknown Source)
	at practice.Pocketmon.main(Pocketmon.java:14)

```

