## Item 11. Always override hashCode when you override equals
<br/>

* equal() 를 Override 했다면 동등성 비교에 사용되는 significant field 가 새롭게 설정되었다는 것이기 때문에 특정 경우(HashMap, HashSet 등)동등성 비교에 사용되는 hashCode() 메소드도 항상 오버라이드 해주어야함
* hashCode 의 리턴값이 uniformly distributed 되지 않는 다면 서로 다른 오브젝트들 간의 충돌이 자주발생하여 HashMap 의 성능이 떨어질 수 있으며, 
* 심한경우 hashCode 가 같은 값만 뱉어서 LinkedList 처럼 Linear 시간으로 동작할 수가 있다
* HashMap 은 데이터를 검색할 때 우선 hashCode() 로 bucket 의 인덱스를 정하고, 해당 버킷의 LinkedList 상의 원소들끼리 equals 로 비교한다
* 만약 logically equal 한 두 인스턴스의 hashCode 가 다르다면, 우연히 서로다른 인스턴스가 같은 bucket 저장되더라도 최적화로 인해 만약 hashCode 가 다르다면 equals 는 실행자체가 안될수도 있다
* equals 에서 사용되지 않는 field 는 hashCode 계산에서 제외해야만한다
* 각각의 field 에 대해 아래처럼 hashCode 를 계산한다
    * primitive type 이면 boxed primitive class 의 hashCode static method 를 사용한다
    * Object 면 재귀적으로 hashCode 를 호출한다
    * 배열이면, 모든 원소들이 중요하다면 Arrays.hashCode 를 사용하고, 그렇지 않다면 의미있는 원소들 각각을 별도의 field 로 생각하고 위의 법칙을 적용한다
    * null 이면 0을 써라
* 각 field 에서 계산된 hashCode 에 대해 아래의 식으로 값을 누적한다
    * result = 31 * result + c
    * c 는 현재 field 의 hashCode
* 31을 곱하는 이유는 곱하지 않고 단순히 누적하면 anagram 인경우에 모두 같다고 인식하기때문
* 31 이어야하는 이유는 홀수이면서, 소수여서
    * 짝수이면 안되는 이유는, 2를 곱하는 행위는 단순 shift 연산이기 때문에 정보가 손실된다
* 특별히 collision 을 덜 발생시키는 hash function 이 필요한것이 아니라면 Object.hash() 를 사용해라
* 하지만 Object.hash 는 Array 인스턴스를 생성해야하고, primitive 타입의 원소도 boxing/unboxing 을 하기때문에 조금 더 느린경향이 있다
* hash code 를 캐쉬해라
* lazy initialize 해라
* 성능을 위한답시고 중요한 필드를 hash code 계산에서 빼지 마라

