## Item 26. Don’t use raw types
<br/>

* raw type 은 migration compatibility 떄문에 있는것이다
* 그니까 쓰지마라
* raw type 쓰면 아래처럼 가능해져서 runtime error 발생 가능성 있음

```java
List list = new ArrayList();
list.add(1);
list.add('a');
```

* 제네릭 타입은 raw 타입의 서브타입이다
* 용어정리

￼![image](https://user-images.githubusercontent.com/7943694/79069633-b5b67500-7d0a-11ea-8d1e-048761819b0b.png)


<> : diamond operator
