## Item 7. Eliminate obsolete object references
<br/>

* 사용되지 않는 객체 참조를 제거하라
* Stack 을 구현한 코드를 예를 들면, pop() 할 때, 단순히 맨 윗부분을 가리키는 pointer 를 1만큼 감소시키기만 한다면 Memory Leak 생긴다
* inactive portion 에 꼭 null 값을 넣어줘야함. 안그러면 reference 를 계속 들고 있어서 GC 가 안됨
* inactive portion 이란 포인터보다 큰 인덱스에 저장된 reference 들
* null 을 넣어줬을 때 추가적인 이점은, 실수로 pop 된 reference 를 사용하는 경우 즉시 에러가 발생시켜줌(NullPointerException)
* 조용히 잘못된 동작을 하는 것보단 가능한한 빨리 에러를 탐지하는 것이 항상 이득이기 때문
* 사용되지 않는 참조를제거하는 가장 좋은 방법은 참조를 담고있는 변수의 scope 밖으로 벗어나는 것이다
* Memory Leak이 발생하는 또 다른 흔한 곳은 Cache 다
* Memory Leak이 발생하는 또 다른 곳은 Listener 와 Callback 이다
* Weak Reference 를 
