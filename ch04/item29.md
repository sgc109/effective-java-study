## Item 29. Favor generic types
<br/>

* 제네릭 타입을 선호해라
* client 의 코드를 바꾸지 않아도 되도록 하면서, 기존의 array 를 제네릭으로 변환하는 방법 2가지가 책에 나와있음
* 타입 파라미터의 어레이는 new 를 못한다(new E[4])

```java
class MyClass<E> {
  void fun() {
    E[] arr = new E[4];
    Object[] objs = arr;
    objs[0] = "123";
    E element = arr[0];
}
```
