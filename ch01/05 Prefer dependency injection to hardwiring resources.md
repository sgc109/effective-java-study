## Item 5. Prefer dependency injection to hardwiring resources
<br/>

### 문제
- 특정 리소스에 따라 Behavior 가 변하는 class 는 Singleton 이나 Static utility class 로 만들지 마라
- class 내부에서 직접 해당 리소스를 만들지도 마라
- 리소스를 외부에서 전달해줘라

### 해결
- DI(Dependency Injection) 을 사용해라
- DI 는 생성자, static factories, builders 모두에 똑같이 적용 가능하다
- 리소스 대신 리소스 Factory(특정 타입의 인스턴스를 반복적으로 생성할 수 있는 객체)를 넘겨줄 수도 있다.
- 이러한 Factory 는 *Factory Method* pattern 을 사용한다.
