## Item 28. Prefer lists to arrays
<br/>

* list 를 array 보다 선호해라
* array 는 covariant 하다. 즉, 아래와 같은 코드가 가능하다

```java
Object[] objs = new Integer[3];
```

* 반면, 제네릭은 invariant 하다. 즉, 아래와 같은 코드는 에러가 발생한다.

```java
ArrayList<Object> list = new ArrayList<Integer>();
```
