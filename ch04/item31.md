## Item 31. Use bounded wildcards to increase API flexibility
<br/>

* bounded wildcard 를 써라. 왜?
* 메소드 인자에서 타입에 약간의 제한을 거는 대신(특정 타입의 서브 타입, 혹은 슈퍼 타입으로 제한)
* 타입이 조금이나마 구체화 되기 때문에 메소드 body 에서 해당 인자로 사용할 수 있는 메소드가 생긴다.
* List 를 예로 들면 add (producer 의 경우) 와 get (consumer 의 경우)
    * producer 는 인자로 받은 자료구조에 새로운 element 를 삽입하는 메소드
    * consumer 는 인자로 받은 자료구조 내의 element 를 추출하는 메소드
* Bounded wildcard vs bounded type parameter
    * Bounded wildcard 는 어떤 타입인지 알 필요가 없기 때문에(다른 곳에서 같은 타입이 사용되지 않기 때문에) 각각의 인자를 선언할 때 적어준다.
    * Bounded type parameter 는 해당 타입(i.e. <E> 의 E)이 다른 곳에서도 사용될 필요가 있을 때 사용하며, 다른 곳에서도 사용해야 하기 때문에 특정 파라미터에 적어주는 것이 아니라, 메소드 정의 부분(접근제어자와 리턴 타입 사이)에 적어 준다.
