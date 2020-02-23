## Item 6. Avoid creating unnecessary objects
<br/>

* Immutable object 를 재사용해라
* new String("blah") 를 반복하는 행위는 하지말자(같은 literal 이 재사용되지 않고 매번 새로운 instance 가 생긴다)
* 생성자대신 static factory method 를 사용해서 매번 불필요한 object 를 생성하는 것을 피할 수 있다
* Mutable object 도 변경되지 않는다는 것을 아는 경우 재사용할 수 있다.
* 비싼 object 를 cache 해라
* String.matches 로 정규표현식을 사용할 때, 단순히 매번 string.matches("*&lt;regular-expression&gt;*") 과 같은 형태로 사용하지말자
* 내부적으로 매번 Pattern 객체를 생성하는데 딱 한 번만 사용하고 GC 될 수 있기 때문
* Pattern 객체를 만드는 것은 비싸다. 유한 상태 머신에 정규표현식을 추가?(compile)하기 때문에
* 그보다는 static final 로 Pattern 을 정의해놓고 **PATTERN.matcher(string).matches();** 와 같은 형태로 사용해라.
* 그럼 속도도 더 빠르고, 변수 명으로 좀 더 의미도 명확하게 할 수 있다.
* Primitive 타입과 Boxed Primitive 타입을 착각하여 매번 object 를 생성하는 실수를 하지말자(Primitive 타입을 선호하자)
* DB 연결같이 매우 무거운 객체가 아닌 이상 직접 Object Pool 을 만들어서 새로운 객체의 생성을 피하는 것은 좋은 생각이 아니다
* 오히려 가독성, 성능 면에서 좋지 않다.
* 새로운 객체를 생성하는 것 자체가 비싼것은 아니다. 생성자에서 많은 일을 하지 않는 이상 새로운 객체를 만드는 것은 값싸다
* 현대의 JVM 은 매우 최적화된 GC 를 가지고있기 때문에 명확성, 간결성 등을 위해 새롭게 객체를 생성하는 것은 오히려 좋은 선택이다
