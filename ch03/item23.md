## Item 23. Prefer class hierarchies to tagged classes
<br/>

* tagged class 란 특정 타입에 따라 다르게 동작하는 클래스
* 사용하지 않는 필드도 함께 선언해야 하기 때문에 메모리 효율성 안좋음
* switch 문으로 분기 해야함
* 새로운 타입 추가되는 경우 기존 코드 수정해야하므로 error prone 하고 확장성 안좋음
* 클래스 hierarchy 로 만들어라
