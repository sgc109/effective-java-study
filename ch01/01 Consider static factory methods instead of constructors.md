## Item 1. Consider static factory methods instead of constructors
<br/>

* ### 한계
  - 생성자는 따로 이름을 설정할 수 없기 때문에 설명이 어려움
  - 생성되는 오브젝트는 오직 한 가지, 해당 클래스의 오브젝트만 가능
  - 매번 새로운 객체가 생성
  - **Static factory method 로 이를 해결**
* ### 장점
  - 생성자와는 다르게 메서드 이름으로 return 하는 object 를 설명 가능
  - Return 하는 object 의 type 을 다양하게 할 수 있음 (subclass 나 interface) (interface 내부에 interface 를 구현하는 private class 형태의 구현체를 두고 이를 interface type 으로 return 하도록 구현하면 encapsulation 이 가능. Collection 가 예) (참고, Interface 내 static method 는 자바8 부터 사용 가능하기 때문에 이전 버전에서는 abstract class 를 사용해야함)
  - 매번 새로운 instance 를 생성하지 않도록 구현하는것이 가능.(Singleton)
  - Input parameter 에 따라 다른 object 를 return 를 반환하는 것이 가능하다.
  - static factory method 는 같은 parameter 를 가지는 여러개의 Object 생성 method 를 가질 수가 있다.


* ### 단점
  - 만약 static factory method 만 갖고, 생성자를 갖지 않는다면 상속을 할 수가 없음(상속에는 단점도 많기 때문에 강제로 하지못하는것이 오히려 좋을 수도 있음)
  - 생성자와는 다르게 일반 함수들과 구분이 어려워 개발자가 존재를 모를 가능성이 있음(주요 naming convention 을 통해 해결)
