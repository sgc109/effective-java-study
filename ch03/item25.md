## Item 25. Limit source files to a single top-level class
<br/>

* 한 소스 파일에 top-level 클래스/인터페이스를 여러개 만들지 말아라
* 같은 이름의 클래스가 여러 파일에 있을 때, 컴파일러에서 읽는 순서에 따라 다른 결과가 발생할 수 있다
* 가능한한 서로 다른 파일로 분리해라
* 여러 top-level 클래스를 한 소스 파일에 넣어야할 경우 차라리 static member class 를 고려해봐라
* private 접근제어자로 accessabiliy 도 줄일 수 있고 더 좋다
