## Chapter 2. Methods Common to All Objects

* Object 는 concrete class 이긴 하지만 확장을 위해 설계됐다
* Object 의 nonfinal method(equals, hashCode, toString, clone 등) 들은 정해진 규칙에 따라 오버라이딩 하지않으면 HashMap, HashSet 같이 이 규칙에 의존하는 클래스가 정상적으로 동작하지 않는다
* 챕터2 는 이러한 Object 의 nonfinal 메소드들이 언제, 그리고 어떻게 오버라이드 되어야 하는지에 대해 다룬다
<br/>

| Item No. 	| Title                                                          	|        Done        	|
|:--------:	|----------------------------------------------------------------	|:------------------:	|
|    10    	| [Obey the general contract when overriding equals](item10.md)  	|                    	|
|    11    	| [Always override hashCode when you override equals](item11.md) 	|                    	|
|    12    	| [Always override toString](item12.md)                          	|                    	|
|    13    	| [Override clone judiciously](item13.md)                        	|                    	|
|    14    	| [Consider implementing Comparable](item14.md)                  	|                    	|
