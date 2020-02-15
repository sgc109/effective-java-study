## Item 4. Enforce noninstantiability with a private constructor.md
<br/>

가끔 static methods 와 static fields 를 grouping 하는 class 를 만들고 싶을 것이다.
이런 class 들은 사람들이 남용해왔기 때문에 좋지않은 평판을 가지고 있지만, 이러한 class 는 적절한 사용처가 있다.

- Primitive 값이나 Array 에 대해 서로 관련이 있는 method 들끼리 grouping 할 때
  * 예) java.lang.Math, java.util.Arrays
- Factory 를 포함한 static methods 들을 grouping 할 때
  * 예) java.util.Collections
- Final class 의 method 들을 grouping 할 때

### 문제
이러한 Utility class 들은 인스턴스화 하기 위해 설계되는 것이 아니다.
Abstract class 로 선언해도 인스턴스화를 막을 수 있지만, 다음과 같은 문제가 있다.
- 상속받으면 서브클래스가 인스턴스화 될 수 있다.
- 사용자가 상속을 위해 설계되었다고 착각하게 만들 수 있다.

### 해결책
**private constructor 를 선언한다.**
- invoke 되지 않게하기 위해 constructor 를 정의한다는 것이 역설적일 수 있기 때문에 주석을 다는것이 좋다
