## Item 24. Favor static member classes over nonstatic
<br/>

* nested class 는 4가지가 있다
    * static member class
    * nonstatic member class (inner class)
    * anonymous class
    * local class
* 하나의 클래스에서만 사용되면 nested class 를 쓰자
* static member class
    * private static member class 의 흔한 용도는 enclosing class 의 구성요소를 나타내는 것
    * 대표적인 예로, Map 클래스 내의 Entry 는 key-value pair 인데 enclosing class 에 대해 알 필요가 전혀 없음
* nonstatic member class(inner class)
    * memory leak 의 위험이 있다.
    * private nonstatic member class 의 대표적인 예는 ArrayList 와 같은 Collection 클래스들 내부의 Iterator 들
* anonymous class 는 여러 interface 를 구현할 수 없고, 상속과 구현을 동시에 할 수 없으며, 여러곳에서 사용될 수 없다는 단점이 있다
* local class 는 local variable 을 선언할 수 있는 곳에 정의할 수 있다.
* 한 메소드 안에서 뿐만 아니라 밖에서도 사용하려고 하거나 메소드 안에 넣기엔 길이가 긴 경우 member class 를 써라
    * enclosing instance 로의 reference 가 필요하면 nonstatic 을 써라
    * 그렇지않다면 static member class 를 써라
* 클래스가 메소드 안에 있는 경우
    * 한 곳에서만 쓰려는 경우는 anonymous class
    * 그렇지 않은 경우는 local class
