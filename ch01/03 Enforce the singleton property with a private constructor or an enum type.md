## Item 3. Enforce the singleton property with a private constructor or an enum type
<br/>

Singleton 을 구현하는 방법은 일반적으로 두가지가 있고, 추가로 한가지가 더있다.

### Common ways
  * **Public field Approach**
    - INSTANCE field 를 public static final 로 선언하고 직접 접근하여 사용하는 방식.
    - 장점은 Singleton 이라는 것을 명확히하고, 구현이 단순하다는 것이다.
  
  * **Static factory approach**
    - INSTANCE field 를 private static final 로 선언하고 static factory method 로 객체를 받는 방식.
    - 장점은 flexibility. 예를 들어 접근하는 스레드에 따라 다른 instance 를 줌으로서, API 를 변경하지 않고도 singleton 여부가 런타임에 결정될 수가 있다. API 를 변경하지 않아도 된다는 것은 이 Class 를 사용하는 Client 의 코드가 변경되지 않아도 된다는것이다.
    - Generic singleton factory 를 만들 수 있다
    - Method reference 가 supplier 로 사용될 수 있다.
    - 위의 세가지 장점 중 한가지도 사용하지 않는다면 public field approach 가 낫다.

  * 주의할점
    - 두 가지 방식 모두 단순히 Serializable 을 구현하는 것만으로는 serializable 하게 만들 수가 없다.
    - Singleton 이라는 것을 보장하기 위해 모든 instance field 를 **transient** 로 선언하고, **readResolve** 메서드를 구현해야한다.
    
### Enum approach
  - 자동으로 serialization 을 지원한다
  - Reflection attack 에서도 하나의 instance 를 보장해준다
  - 이 방식이 조금은 부자연스럽게 느껴질 수도 있는데, single-element enum type 은 항상 싱글톤을 구현하는 최고의 방법이다.
  - Superclass 를 상속받아야하는 경우에는 사용할 수 없다
  - +Android의 경우 Object 생성시 Context 를 넘겨주어야 하는 등 꼭 런타임에 instantiation 을 해야하는 경우에는 사용할 수 없다
