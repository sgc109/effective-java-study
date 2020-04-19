## Item 32. Combine generics and varargs judiciously
<br/>

* 제네릭과 가변인자를 함께 사용할 땐 신중하게 사용해라
* varargs 는 내부적으로 array 를 만드는 식으로 동작하기 때문에 generic 과 varargs 를 같이쓰면 heap pollution 이 발생할 수 있다([item 28](item28.md))
* 그럼에도 불구하고 컴파일 에러가 나지 않는 이유는, 때때로는 이것이 매우 유용하기 때문이다
* 하지만 사용하더라도 조심해야한다
* 2가지 조건을 만족하면 type safe 하다고 보장할 수 있다
    * varargs 파라미터에 새로운 값을 저장하지 않는다
    * array 가 외부에서 visible 하지 않다
* type safe 하다는 확신이 있을때만 @SafeVarargs 어노테이션을 붙여라
* 만약 해당 warning 이 떴다면 type safe 한지 체크하고나서 warning 을 suppress 해라
