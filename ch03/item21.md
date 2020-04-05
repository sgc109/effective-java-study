## Item 21. Design interfaces for posterity
<br/>

* interface 에 추후에 메소드를 추가하지마라
* default 구현이 없으면 컴파일에러가 나고
* default 구현이 있어도 문제가 될 수 있음(Apache SynchronizedCollection 의 경우)
* 기존에 interface 의 모든 메소드에 대해 synchronize 를 했던 경우, 새로운 메소드가 추가 되는 경우 locking 없이 호출될 수 있으므로 기존의 의도와 다르게 동작
* default method 로 추가되면 오히려 compile 에러가 아닌 runtime 에러가 발생할 수가 있음
