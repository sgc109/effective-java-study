## Item 2. Consider a builder when faced with many constructor parameters
<br/>

* ### 문제점
  - 생성자 파라미터가 많고, 특히 Optional 한 파라미터가 많은 경우 모든 경우에 대해 생성자를 만들 순 없음
  - 그래서 예전엔 **Telescoping constructor pattern** 혹은, **JavaBeans pattern** 가 사용되기도 했는데, 문제점이 있음.

* **Telescoping constructor pattern**
  - public MyClass(int a) { ... }
  - public MyClass(int a, int b) { ... }
  - public MyClass(int a, int b, int c) { ... }
  - 이런식으로 순차적으로 하나씩 파라미터가 추가되는식으로 N개의 생성자를 만드는 방식
  - 뒷쪽에 있는 파라미터를 넘기기 위해서는 중간에 굳이 필요하지 않은 파라미터들도 모두 넘겨주어야함
  - 생성자에서 파라미터를 너무 많이 넘기게 되는 경우 가독성이 좋지 않고, 수정시 개수를 잘 세어야 하며, 실수로 인자의 순서를 잘못 줄 확률이 있음

* **JavaBeans pattern**
  - 모든 fields 에 대해 setter 를 만들고, 기본 생성자로 객체를 생성한 뒤, 필요한 변수들만 값을 set 해주는 방식
  - 여러 setter 의 호출에 의해 최종 객체가 만들어 지기 때문에 값을 셋팅하는 도중에 객체의 사용을 시도할 경우 문제가 발생할 수가 있음
  - 이런 경우 디버깅하기가 힘들다
  - Thread safety 를 위해 좀 더 많은 노력이 필요하다
  - Setter 가 있기때문에 Immutable 하게 하지 못한다
  - Builder pattern 은 final 로 property 가 선언되어 있기 때문에 object 를 사용하는 순간엔 값을 변경할 수 없지만, JavaBeans pattern 은 property 들을 세팅해주는 중간에 object 를 사용할 수 있기 때문에 문제가 생길 수 있다.
  

* ### 장점
  - Class hierarchies 에 잘 맞는다 (Build 하려는 Class 와 그 내부의 Builder Class 를 같이 상속 받는다. 즉, 자식 클래스의 빌더도 부모 클래스의 빌더를 상속받는다)
  - Parameter 를 셋팅해주는 각 메서드들이 자기자신(this)를 반환하기 때문에 chaining 으로 구현하기 좋다.
  - 많은 수의 생성자가 필요하지 않다.(필수 parameters 로 구성된 생성자와 Builder 를 받는 생성자, 이렇게 두개면 된다.)

* ### 단점
  - 객체를 생성하기 위해서는 항상 빌더를 생성해야하기 때문에 Performance-critical 한 상황에서는 문제일 수가 있다.
  - Telescoping constructor pattern 보다 소스코드가 장황해 질 수 있다.(생성자 파라미터가 적당히 많을 때 써라. 예를 들면 4개 이상. 하지만 파라미터가 추후 늘어날 수가 있기 때문에 시작부터 빌더 패턴을 쓰는것이 좋은 경우가 많다.)
  

* ### 특징
  - Build 하려는 Object 는 보통 Immutable 임(fields 가 final 로 선언되고, build() 호출 시 값을 셋팅해주기 때문)
  - 부모 클래스 내부의 빌더 클래스를 정의할 땐, **Generic type with a recursive type parameter** 를 사용한다.
  - 하나의 빌더가 여러개의 객체를 생성하는데 사용될 수 있다.
  - Property 를 설정해주는 함수는 모두 this 를 return 한다.(subclass 의 Builder class 에서는 Factory method pattern 으로)
  - build() 메서드는 new MyClass(Builder) 로 Constructor Parameter 로 Builder 를 넘겨주며 객체를 생성하고 이를 반환한다.
  - MyClass 의 생성자에서는 parameter 로 받은 Builder 의 각 fields 들을 자신의 fields 로 복사한다.
