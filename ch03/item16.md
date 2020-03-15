## Item 16. In public classes, use accessor methods, not public fields
<br/>

* public class 는 item 15 처럼 public field 를 가지면 안되고 accessor 를 둬야한다
* package-private 이거나 private nested class 는 public field 를 가져도 큰 문제가 되진 않는다
* public field 여도 immutable object 의 reference 라면 덜 해롭다
  - 그러나 추후에 이 부분이 변경된다면 이것을 사용하는 코드들도 변경되어야하므로 유지보수에 좋지 않다
