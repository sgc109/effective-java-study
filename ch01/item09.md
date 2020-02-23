## Item 9. Prefer try-with-resources to try-finally
<br/>

꼭 close 되어야하는 resource 를 생성하여 사용할 때 *try-finally* statement 가 아니라, *try-with-resources* statement 를 사용해라

### 문제인식
* 여러개의 resource 를 사용할 경우 중첩된 *try-finally* 문을 작성해야함
* 이런경우 가독성이 좋지않으며, 매번 명시적으로 close 를 해줘야한다
* *try* block 뿐만 아니라 *finally* block 에서도 Exception 이 발생할 수 있으며
* 여러개의 예외가 발생할 경우 가장 궁금한 것은 맨 처음 발생한 예외인데도 불구하고 마지막에 발생한 예외만 stacktrace 에 나타나 디버깅이 어려워진다
* 뒤에 발생하는 예외들을 suppress 하도록 코드를 작성할 수 있으나 verbose 해진다

### try-with-resources 장점
* *try-with-resources* 문의 try() 안에 선언된 AutoClosable 을 구현하는 object 들은 statement 가 끝날 때 자동으로 close() 메소드가 호출됨
* 여러개의 예외가 발생하는 경우 앞서 발생한 예외들을 suppress 하여 갖고있다가 stacktrace 에서 보여준다
* *Throwable.getSuppressed* 메소드를 통해 suppress 된 예외들에 접근할 
