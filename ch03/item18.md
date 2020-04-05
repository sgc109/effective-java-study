## Item 18. Favor composition over inheritance
<br/>

* 상속은 캡슐화를 위반한다
* 서브클래스는 슈퍼클래스의 구현에 의존한다
* 릴리즈마다 슈퍼클래스가 변경된다면 서브클래스의 변경이 없더라도 오류가 발생할 수 있음
* 두가지 문제가 있음
    * 슈퍼클래스의 어떤 메소드에서 또 다른 내부에 있는 메소드를 호출하는 경우(슈퍼클래스에 self-use of overridable method 가 있는 경우)
    * 슈퍼클래스에 새로운 메소드가 추가되는경우
* 슈퍼클래스에 직접 접근할 수가 있어서 문제를 야기할 수 있음(타입 체크를 해야하는 경우. Properties 와 Hashtable)
* forwarding class 를 만들어서 forwarding method 들로 composition 한 기존의 상속하려던 클래스의 객체를 유지하여 function call 을 forwarding
* forwarding class 를 상속받아서 직접 상속의 문제점을 해결
