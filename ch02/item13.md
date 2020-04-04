## Item 13. Override clone judiciously
<br/>

#### Cloneable 과 clone() 으로 copy 를 구현하는 것은 단점이 매우 많기 때문에 copy constructors 나 copy factories 를 사용하라

* mixin interface 로 의도된 인터페이스
* Cloneable interface 에는 clone 메서드가 없다
* 단순히 복제를 허용한다는 것을 나타내는 용도로 쓰이기 때문
* Object 의 clone() 은 protected 다
* 고로 단순히 Cloneable 을 구현한다고 clone 을 호출할 수 있는건 아니다
* 그럼에도 불구하고 많은 곳에서 쓰이므로 잘 이해해야한다
* Cloneable 인터페이스를 구현하는 클래스는 적절한 public clone() 를 제공해야한다. 
* Cloneable/clone 은 복잡하고, 문서화도 잘 되어있지 않은 규칙을 지켜야하기 때문에 위험하고 매우 좋지 않다
* 슈퍼 클래스에 정의된 메소드의 접근 제어자보다 좁은 접근으로는 선언할 수 없지만, 넓은 접근으로는 선언할 수 있다.
* 예를 들어 슈퍼 클래스에 protected 로 선언 되어있다면, package-private 으로는 선언할 수 없지만 public 으로는 선언할 수 있다.
* super.clone() 을 호출하지 않는 final class 는 Cloneable 을 구현하지 않아도 된다
* immutable class 에는 절대 clone 메소드를 만들지 마라. 낭비일 뿐
* clone() 은 생성자처럼 동작하지만서도, 기존의 object 에 영향을 줄 수 있기 때문에 주의 해야한다.
* mutable object 의 reference 를 들고있기 때문
* 재귀적으로 해당 object 의 clone() 을 호출하여 reference 를 바꿔준다
* array field 의 경우에 위와 같이 해야한다.
* 하지만 mutable object 의 reference 를 가진 field가 final 로 선언되어있다면 문제가 발생한다.
* 고로, cloneable 하게 만들고싶다면 final field 를 non-final 로 만들어야한다.
* Hashtable 을 복제하는 경우, 링크드리스트를 들고있는 bucket 의 array 를 clone 해도 같은 링크드리스트를 가리키게 된다.
* 이 경우는 직접 bucket 의 array 를 생성하여 각각의 bucket 에 대해 링크드리스트의 각 노드를 따라가면 직접 clone() 을 해줘야 한다.
* **Object copy 를 하는 더 좋은 방법은 copy constructor 또는 copy factory 이다**
* 같은 타입의 객체를 단 하나의 argument 로 받아서 복사함
* interface 타입을 받아서 복사도 가능하다는 장점이 있음
* 대부분의 collection 클래스들은 Collection 이나 Map 을 인자로 받는 constructor 가 있음
* 이를 보통 conversion constructors 혹은 conversion factories 라고 부름
* 예를들어 HashSet 을 TreeSet 형태로 복사할 수도 있음(new TreeSet<>(s) 와같은 식으로)
* **Clonable 에는 여러 문제가 있기 때문에 새로 만드는 interface 는 이를 상속받으면 안되며, 새로 만드는 상속가능한 class 들은 이를 구현하면 안됨**
* **복사 기능은 생성자나 팩토리 메소드로 하는 것이 국룰이다**
* 유일한 예외는 Array. 배열은 clone 으로 복사하는것이 최고다
