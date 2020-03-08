## Item 12. Always override toString
<br/>

* 인스턴스화 하는 모든 클래스에 대해 항상 toString 을 오버라이드해라(superclass 가 하고 있지 않다면)
* Object class 의 default 구현은 "<class 이름>@<16진수 hashCode 값>" (e.g. MyClass@efefefef)
* 객체의 의미를 잘 전달할 수 있도록 해라
* 내가 직접 호출하지 않아도 다른 함수가 자동으로 호출하는 경우가 많다
* toString 의 리턴값은 객체의 중요한 정보를 모두 포함해야한다
* toString 의 리턴값으로 다시 겍체를 만들 수 있는 수단을 만들어라 생성자나 static factory 를 만들어라
* subclass 가 toString 의 구현을 공유할 수 있도록 abstract 클래스에 정의해라

