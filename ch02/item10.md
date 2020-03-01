## Item 10. Obey the general contract when overriding equals
<br/>

* equals 를 오버라이딩할 땐 꼭 지켜야할 5가지 필수 규칙이 있다
* Object 의 equals 는 같은 reference 인지를 체크하도록 구현되어있다
* **꼭 해야되는 경우가 아니라면 equals 를 override 하지 마라! 대부분의 경우 Object 로부터 상속받은 equals 는 우리가 원하는 대로 동작할것이다**

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

### 필수 규칙(general contract)
* 반사(Relexive)
  - x.equals(x) 는 true
  - 실수로 위반하기 힘듬
  - 위반할 시, collection 에 이 클래스의 인스턴스를 삽입해도 존재하지 않다고 인식할것
* 대칭(Symmetric)
  - x.equals(y) 는 y.equals(x) 과 같아야함
  - 실수로 위반하기 어렵지 않음
  ```java
  final class CaseIntensitiveString {
    private final String s;

    public CaseIntensitiveString(String s) {
        this.s = Objects.requireNonNull(s);
    }

    @Override
    public boolean equals(Object o) {
        if (o instanceof CaseIntensitiveString)
            return s.equalsIgnoreCase(
                    ((CaseIntensitiveString) o).s);
        if (o instanceof String) // 이 클래스만 대소문자를 무시하고, String 의 인스턴스는 대소문자를 구분함
            return s.equalsIgnoreCase((String) o);
        return false;
    }
  }
  ```
  - 만약 아래와 같은 코드를 실행한다면 어떻게 될까?
  ```java
  CaseIntensitiveString cis = new CaseIntensitiveString("Polish");
  String s = "polish";

  List<CaseIntensitiveString> list = new ArrayList<>();
  list.add(cis);

  System.out.println(list.contains(s));  
  ```
  - true, false, 혹은 runtime exception. JDK 구현에 따라 달라질 것이다
  - 이를 해결하려면 그냥 String 과도 함께 동작하게 하려는 시도를 하지 말아야 한다
  ```java
  return o instanceof CaseInsensitiveString && ((CaseInsensitiveString) o).s.equalsIgnoreCase(s);
  ```
* 추이(Transitive)
  - x.equals(y) 가 true, y.equals(z) 가 true 면 x.equals(z) 는 true
  - 상속 관계인 두 클래스를 equals 로 비교할 때 문제가 발생하기 쉽다
  - 상속 대신 composition 을 사용하면 임시방편으로 해결가능하다
  - Java platform libraries 중에서도 상속을 받아 value component 를 추가한 클래스들이 있다
  - java.sql.Timestamp 는 java.util.Date 를 상속받아 nanoseconds 필드를 추가한것이다
  - 이 둘을 같은 collection 에 넣고 사용하면 문제가 발생할 수 있다(Timestamp 의 이러한 동작은 잘못 구현된것이며, 실행되어선 안된다)
  - 하지만 만약 superclass 가 abstract class 라면 인스턴스화 될 수 없기에 위의 문제가 없다
* 일관성(Consistent)
  - equals 에서 사용되는 정보가 변경되지 않는 한, x.equals(y) 는 항상 같은 결과는 내야함
  - Immutable object 라면 일관성이 보장되기 때문에 가능한한 Immutable 을 고려해라
  - Immutable 이던 아니던 unreliable 한 리소스에 의존하는 equals 메소드를 구현하지 마라
  - java.net.URL 의 equals 는 host name 을 IP 주소로 변환되는 과정에서 network 접근이 발생하기때문에 일관성이 보장되지 못한다
  - URL 의 equals 는 잘못 구현된것이며, 실행되어선 안된다
  - 고로, equals 는 메모리에 존재하는 객체에 대한 deterministic 한 computation 만 수행해야한다
* Non-nullity
  - x.equals(null) 은 false 여야함
  - *instance of* 의 첫번째 operand 가 null 이라면 두번째 operand 와 상관없이 false 를 반환하므로 맨처음에 명시적인 널체크는 필요없이 타입체크부터 하면된다

### 규칙을 지키는것이 중요한 이유
* 안지키면 프로그램이 비정상적으로 동작하거나 Crash 가 발생할 것임
* equals 에 의존하는 클래스들이 많기 때문에 잘못 구현할 경우 원인을 찾기가 매우 어려울 것임

### equals 메소드 레시피
* 첫째, 우선 *==* operator 로 같은 객체에 대한 참조인지 확인해라
  - 비교가 비싼 객체라면 성능 최적화로 좋음
* 둘째, *instance of* operator 로 적절한 타입인지 체크해라
  - 아니라면 return false
  - 클래스가 interface 를 구현한 경우엔 이를 이용해 비교하자
* 셋째, 클래스를 적잘한 타입으로 변환해라
  - 앞서 타입 체크를 해서 문제 없다
* 넷쨰, 비교하고자 하는 각각의 필드가 모두 일치하는 지를 체크해서 그렇다면 true, 아니면 false 를 리턴해라
  - 만약 interface 라면 method 를 통해 필드에 접근해라
  - field 가 float 과 double 이 아닌 primitive 타입이라면 == operator 를 사용해라
  - object reference 라면 재귀적으로 equals 를 호출해라
  - float 라면 static Float.compare(float, float) 를 사용해라
  - double 이라면 Double.compare(double, double) 를 사용해라
  - 만약 null 일 수 있는 object reference 는 NPE 가 발생할 수 있으므로 Object.equals(Object, Object) 를 사용해라
* 참고사항
  - 성능을 위해, 다를 가능성이 높은 field 일수록, 비교 비용이 적은 field 일 수록 먼저 비교하자(둘다라면 가장 먼저해야한다)
  - 다른 field 들을 통해 계산되는 field 까지 비교할 필요는 없으나 연산을 줄여줄 수도 있다
  - 예를 들어, 두 다각형 객체 넓이가 다르다면 굳이 선분과 꼭지점까지 비교할 필요도 없다
  - **equals 메소드의 작성은 스스로 세 가지 질문을 묻고 끝낸다. symmetric 한가? transitive 한가? consistent 한가? 그리고 유닛 테스트도 작성해라**
  - 물론 reflexitivy 와 non-nullity 도 만족돼야하지만 대체로 알아서 만족된다

### 올바른 equals() 예시
```java
final class PhoneNumber {
    private final short areaCode, prefix, lineNum;

    public PhoneNumber(int areaCode, int prefix, int lineNum) {
        this.areaCode = rangeCheck(areaCode, 999, "area code");
        this.prefix = rangeCheck(prefix, 999, "prefix");
        this.lineNum = rangeCheck(lineNum, 9999, "line num");
    }

    private static short rangeCheck(int val, int max, String arg) {
        if (val < 0 || val > max)
            throw new IllegalArgumentException(arg + ": " + val);
        return (short) val;
    }

    @Override
    public boolean equals(Object o) {
        if (o == this)
            return true;
        if (!(o instanceof PhoneNumber))
            return false;
        PhoneNumber pn = (PhoneNumber) o;
        return areaCode == pn.areaCode &&
                prefix == pn.prefix &&
                lineNum == pn.lineNum;
    }
}
```
### 추가 사항
* *equals* 를 Override 할 땐 항상 *hashCode* 도 Override 해라
* *equals* 메소드의 argument type 은 꼭 **Object** 여야한다.
  - 다른 타입으로 선언했다면 사실은 **override** 한것이 아니라 **overload** 를 한것이다
  - @Override annotation 을 써서 실수를 줄여라
* *equals* 를 작성하고 테스트하는 것을 대신해주는 *Google 의 Framework 인 AutoValue* 를 쓰면 된다
  - annotation 하나만 붙여주면 자동 생성해준다
  - 대부분의 경우 직접 작성한 
 
