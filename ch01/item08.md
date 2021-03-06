## Item 8. Avoid finalizers and cleaners
<br/>

**Finalizer** 와 **Cleaner** 는 C++ 의 *Destructor* 와 비슷한 것이라고 보면된다. 
하지만 직접 메모리 관리를 해줘야하는 C++ 과는 달리 Java 는 GC 가 메모리를 관리 하기 때문에 C++ 의 Destructor 와는 다르게 동작한다.
<br/><br/>

### finalizer 와 cleaner 의 특징
* finalizer 는 Java 9 부터 deprecated 됐다. 그 대신 cleaner 가 이를 대체한다
* 둘 다 예측불가능하고, 느리고, 일반적으로 불필요하다
<br/>

### 문제점

* 바로 호출된다는 보장이 없다
  - finalizer 와 cleaner 는 object 가 unreachable 하게 되자마자 호출된다는 보장이 없다.
  - 파일을 finalizer/cleaner 에서 닫는건 매우 좋지 않다. file descriptor 는 제한된 리소스이기 때문
  - 만약 여러 파일을 finalizer/cleaner 에서 닫도록 해, 제때 닫히지 않는다면 더이상 파일을 못열게 된다
  - finalizer/cleaner 이 호출되는 시기는 JVM 의 구현체에 따라 다르기 때문에 특정 JVM 에서는 잘 동작해도, 다른 JVM 에서는 아닐 수 있다
  - finalizer thread 는 낮은 우선순위를 가져서 제 때 finalizer 가 실행되지 않을 수 있는것
  - 게다가 어떤 스레드에서 실행시킬지도 보장되지 않으므로 그냥 쓰지 않는 것외엔 별 수가 없다
  - cleaner thread 는 컨트롤 할 수 있다는 점에서는 좀 더 낫지만, 여전히 백그라운드에서 GC 의 통제 아래 있기때문에 즉시 실행된다는 보장이 없다
  - 심지어 finalizer/cleaner 는 단순히 늦게 실행되는 것이 아니라 아예 실행되지 않을 수도 있다. 실행되기 전에 프로그램이 종료할경우.
  - 그러므로 persistent lock 의 release 를 finalizer 에서 하게되면 distributed system 이 모두 멈출 수 있다

* 느리다
  - 객체를 하나 생성하고 닫는데 걸리는 시간이, finalizer 에서는 약 50배, cleaner 에서는 약 5배 느리다

* 심각한 보안 문제가 있다
  - finalizer attack 에 취약하다
  - 생성자나 readObject/readResolve 에서 예외가 발생하면 악의적인 subclass 는 생성되다 만 객체로 실행되는데
  - finalizer 는 static field 에 객체의 참조를 저장하여 객체가 GC 되지 않게 할 수 있다.
  - 이렇게되면 이 객체의 임의의 메소드를 호출할 수 있게된다.
  - 생성자에서 예외를 throw 하면 충분하지만, finalizer 가 있을땐 아니다
  - final class 는 상속받을 수 없으므로 안전하다. finalize 메소드를 final 로 선언하는 것도 안전하다.
<br/>

### 해결책

* AutoCloseable 을 구현해라
  - close 메소드를 정의하고, 더이상 object 가 필요없어 지면, client 에서 이를 호출해라
  - 예외가 발생할 때를 위해 try-with-resources 를 함께 사용해라
<br/>

### 그럼에도 사용하는 이유

* Client 에서 실수로 *close* 를 호출하지 않았을 때 보험(safety nets)용으로 좋음. 메모리 반환을 안하는 것보단 늦게라도 하는게 나으니까
* FileInputStream, FileOutputStream, ThreadPoolExecutor, java.sql.Connection 등은 보험용으로 finalizer 를 갖고있다
* Java 의 delegate 역할을 하는 Native peer(non-Java object)를 사용하는 경우, Java peer 가 GC 되어도 Native peer 는 GC 되지 않으므로 finalizer 를 사용하면 safety net 의 역할을 할 수 있다
<br/>

참고로 try-with-resources 는 
```java
try(Room myRoom = new Room()) {...}
```
형태의 구문이며, try-catch 구문이 종료되면서 자동으로 close 메소드를 호출해준다. AutoClosable 과 함께 JDK 1.7 부터 지원된다.
