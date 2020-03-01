## Item 10. Obey the general contract when overriding equals
<br/>

* equals 를 오버라이딩할 땐 지켜야할 규칙이 있다
* equals 는 기본적으로 같은 reference 인지를 체크하도록 구현되어있다

### equals 를 오버라이드 하지 않는게 더 좋은 경우
* 각 인스턴스가 태생적으로 유일한 경우(e.g. Thread)
* 굳이 인스턴스의 내용물이 같은지 확인할 필요가 없는 경우
* superclass 에서 이미 equals 을 제대로 오버라이드한 경우(e.g. Set & AbstractSet, ...)
* equals 이 절대 실행되지 않음을 확신할 수 있는 경우

### 오버라이드 해야하는 경우
* Value class 인 경우(e.g. Integer, String, ...)
* 이 경우엔 프로그래머도 같은 객체를 참조하는지를 보고싶어하는 것이 아니라 logically equivalent 한지가 궁금하기 때문
* 게다가 map key, set element 의 역할을 하기도 하므로
* 단, Enum 은 예외적으로 안해도 됨

### 필수 규칙
* 반사(Relexive)
  - x.equals(x) 는 true
* 대칭(Symmetric)
  - x.equals(y) 는 y.equals(x) 과 같아야함
* 추이(Transitive)
  - x.equals(y) 가 true, y.equals(z) 가 true 면 x.equals(z) 는 true
* 일관성(Consistent)
  - equals 에서 사용되는 정보가 변경되지 않는 한, x.equals(y) 는 항상 같은 결과는 내야함
* x.equals(null) 은 false 여야함
