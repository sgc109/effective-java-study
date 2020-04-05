## Item 19. Design and document for inheritance or else prohibit it
<br/>

* overridable 한 메소드를 내부적으로 호출하는 경우 이를 문서에 명시해야한다
* 애초에 가능한한 호출을 하지 마라
* 3개의 서브 클래스를 만들어서 테스트해봐라
* 생성자에서 overridable 한 메소드를 호출하지마라
* Cloneable/Serializable 의 clone()/readObject()
* subclassing 되도록 잘 설계되고 문서화되지 않은이상 상속을 막아라
