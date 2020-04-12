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

* 그러므로 array를 사용할 경우 다음과 같은 실수로 인해 런타임 에러가 발생할 수 있다

```java
// Fails at runtime!
Object[] objectArray = new Long[1]; objectArray[0] = "I don't fit in"; // Throws ArrayStoreException 
```

* 하지만 list를 사용할 경우 애초에 컴파일이 안되므로 런타임 에러가 날 가능성이 사라진다

```java
// Won't compile!
List<Object> ol = new ArrayList<Long>(); // Incompatible types 
ol.add("I don't fit in"); 
```

* array 는 제네릭과는 달리 reified 하다, 즉 런타임에도 타입에 대한 정보가 남아있다
* 반면 제네릭은 erasure 라서 타입에 대한 정보가 런타임에 사라진다(List<Integer> 의 런타임 타입은 List 이다)
* 제네릭의 어레이를 만들면 컴파일이 안된다. 왜냐면 array 는 covariant 하므로 런타임에러가 날 수 있기 때문에 이러면 제네릭을 쓰는 이유가 사라짐
  
```java
// Why generic array creation is illegal - won't compile! 
List<String>[] stringLists = new List<String>[1]; // 이 줄은 애초에 컴파일이 안되지만, 만약 된다고 가정한다면 마지막 줄과같은 문제가 발생한다
List<Integer> intList = List.of(42);
Object[] objects = stringLists;
objects[0] = intList; 
String s = stringLists[0].get(0); // 여기서 문제가 발생할 수 있기 때문에 애초에 컴파일이 되지 않도록 만들어졌다.
```

* Arrays are covariant and reified; generics are invariant and erased 
