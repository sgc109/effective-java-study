## Item 33. Consider typesafe heterogeneous containers
<br/>

* heterogeneous container (type token) 을 쓰면 각 타입에 따라 하나의 인스턴스를 맵에 저장할 수 있다
* 삽입할 때 Class 객체의 cast() 메서드를 사용하면 이 인스턴스가 해당 타입인지 검사 할 수 있어서 만약 실수로 다른 타입을 삽입한다면
* 해당 인스턴스를 사용할 때가 아닌, 삽입할 때 런타임 에러를 발견할 수 있다
