## Item 14. Consider implementing Comparable
<br/>

> Comparable 을 잘 구현해라

* 안그러면 compareTo 에 의존하는 Sorted collections(TreeSet, TreeMap) 혹은 검색이나 정렬 알고리즘을 포함하는 Arrays 가 비정상적으로 동작할 것
* compareTo 를 작성하는 방법은 equals 와 거의 똑같지만(반사, 추이 등) 타입체크할 필요없다는게 equals 와의 차이(같은 타입이 아니면 컴파일이 안되기때문에)
* new BigDecimal("1.0") 과 new BigDecimal("1.00") 을 HashSet 에 저장하면 equals 로 비교하기 때문에 서로다른 두개의 원소로 인식하지만, TreeSet 는 동등성비교도 compareTo 메소드만 사용하기 때문에 하나의 원소로 인식한다
* 그렇기 때문에 두 자료구조를 모두 사용하는 경우, 예상치 못한 결과를 예방하기 위해 동등성 비교에 있어 compareTo 와 equals 의 결과를 같도록 해야한다.(같다면 compareTo 는 0, equals 는 true)
* compareTo 메소드 내에서 '>' 와 '<' 같은 비교연산자 사용은 비추(if 문으로 참/거짓 체크하여 return -1 이런 구현이 돼서 장황해지고 실수하기 쉽다)
* object reference field 는 재귀적으로 compareTo 를 호출하고, 만약 Comparable 을 구현하고있지 않거나 자체적인 비교 기준이 필요하다면 Comparator 를 써라
* 자바8 부턴 Comparator 인터페이스의 comparing/thenComparing 을 쓰면 method chaining 을 하는 식으로 object 의 여러 field 에 대해 순차적인 비교가 쉽게 가능하다
* 오버플로우로 인해 -/+ 가 역전되는 것을 조심해야하므로, 단순 - 연산보단 boxed primitive 의 static 메소드인 compare() 를 사용해라
