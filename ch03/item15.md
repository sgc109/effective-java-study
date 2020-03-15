## Item 15. Minimize the accessibility of classes and members
<br/>

* class 는 public static field 같은 상수를 제외하고는 public field 가 없어야한다
* 정보은닉을 잘 하면 성능 개선에 좋다
  - 다른 컴포넌트로의 파급효가가 줄어들기 때문에 성능 이슈가 있는 컴포넌트만 잘 튜닝하면 되므로
* class 의 접근성은 2가지
  - private
  - package-private
* API 로 제공할거아니면 class 는 package-private 으로 해라
* package-private 인데, 이를 사용하는 class 가 단 하나뿐이라면, private static nested class 로 만들어버려라
* field 의 접근성은 4가지
  - private
  - package-private
  - protected
  - public
* 오버라이딩한 subclass 의 메소드는 superclass 의 메소드보다 낮은 접근성을 부여하지 못한다
* 테스트를 위해 private field 를 package-private 으로 바꾸는것은 괜찮지만, 그 이상으로는 바꾸지 말아라
  - 즉, 테스트 코드를 외부로 export 하지 마라
* public 으로 field 를 선언하는 딱 하나 예외가 있다면 public static final fields 인데, primitive 거나 immutable object 의 reference 여야한다
* 배열은 mutable object 이므로 외부로 노출시키지 마라
  - 혹은 immutable List 로 제공하라
* 자바 9 부터는 module-info.java 라는 파일을 통해 추가적인 접근제어가 가능하다.
* module 은 package 의 모음인데, module-info.java 에서 unexported 한다고 하면 public 이나 protected 도 외부에 노출되지 않는다
* 하지만 module 은 JDK 밖에서는 권장되지 않는다
