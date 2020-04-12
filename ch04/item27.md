## Item 27. Eliminate unchecked warnings
<br/>

* 제네릭을 사용할 때 발생하는 warning 을 없애라
* typesafe 하다고 장담할 수 있으면 suppressWarnings("unchecked") 어노테이션 써라
* 하지만 가능한한 작은 scope 로 써라
* class 에는 절대 쓰지말고, 가급적 method 에, 가능하면 local variable 에 써라
* return 문에는 이 어노테이션을 달지 못하므로, 중간에 변수에 담아서 어노테이션을 붙인 뒤 return 해라
* 모든 처리되지 않은 warning 은 런타임에 잠재적인 ClassCastException 다
