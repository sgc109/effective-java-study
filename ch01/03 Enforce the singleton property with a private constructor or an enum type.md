## Item 3. Enforce the singleton property with a private constructor or an enum type
<br/>

* ### 구현 방법
  - Singleton 을 구현하는 방법은 크게 두가지가 있다. **Public field Approach** 와 **Static factory approach** 이다.
  - **Public field Approach** 는 INSTANCE field 를 public static final 로 선언하고 직접 접근하여 사용하는 방식.
  - 장점은 Singleton 이라는 것을 명확히하고, 구현이 단순하다는 것이다.
  - **Static factory approach** 는 INSTANCE field 를 private static final 로 선언하고 static factory method 로 객체를 받는 방식.
  - 장점은 flexibility. 예를 들어 접근하는 스레드에 따라 다른 instance 를 줌으로서, API 를 변경하지 않고도 singleton 여부가 런타임에 결정될 수가 있다. API 를 변경하지 않아도 된다는 것은 이 Class 를 사용하는 Client 의 코드가 변경되지 않아도 된다는것이다.
  - 

* ### 장점
  - 

* ### 단점
  -   

* ### 특징
  - 
