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
* 일관성(Consistent)
  - equals 에서 사용되는 정보가 변경되지 않는 한, x.equals(y) 는 항상 같은 결과는 내야함
* x.equals(null) 은 false 여야함

### 규칙을 지키는것이 중요한 이유
* 안지키면 프로그램이 비정상적으로 동작하거나 Crash 가 발생할 것임
* equals 에 의존하는 클래스들이 많기 때문에 잘못 구현할 경우 원인을 찾기가 매우 어려울 것임

