## Item 17. Minimize mutability
<br/>

* Class 를 Immutable 하게 하려면
    * object 의 state 를 변경하는 메소드(mutator)를 두지 말아라
    * 클래스가 상속되지 않도록 해라(final class)
    * 모든 field 를 final 로 만들어라
    * 모든 field 를 private 으로 만들어라
    * mutable 한 object 로의 reference 를 외부로 반환하거나, 외부에서 만들어진 object 를 field 에 저장하지 말아라
* Immutable 클래스는 장점이 많다
    * 단순하다
    * 스레드 세이프하다
    * 공짜로 공유될 수 있다
    * 다른 객체를 이루는 빌딩 블록의 역할
* 단점은 가끔 성능 이슈가 있을 수 있다
    * field 하나만 바꾸려해도 매번 새로운 객체를 생성해야한다
* 정말 특별한 이유가 없다면 클래스는 Immutable 하게 만들어라
* 만약 Immutable 하게 만들 수 없더라도 mutable field 를 최대한 줄여라
