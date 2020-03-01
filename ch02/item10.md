## Item 10. Obey the general contract when overriding equals
<br/>

### equals 를 오버라이드 하지 않는게 더 좋은 경우
* 각 인스턴스가 태생적으로 유일한 경우(e.g. Thread)
* 굳이 인스턴스의 내용물이 같은지 확인할 필요가 없는 경우
* superclass 에서 이미 equals 을 제대로 오버라이드한 경우(e.g. Set & AbstractSet, ...)
* equals 이 절대 실행되지 않음을 확신할 수 있는 경우
