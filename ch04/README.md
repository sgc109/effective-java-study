## Chapter 4. Generics

* 제네릭은 잘못된 타입의 객체를 사용했을 때 발생할 수 있는 에러를 런타임이 아닌, 컴파일 타임에 잡기위해 있는 것
* 제네릭을 쓰지 않고 raw type 으로 사용하면 Object 타입으로 인식되기 때문에 사용할 때마다 type cast 를 해줘야 함
* 만약 실수로 여러 타입의 데이터를 저장한 뒤, 추후에 사용할 때 잘못된 타입으로 변환을 시도한다면 런타임 예외가 발생
<br/>

| Item No. 	| Title                                                            	|        Done        	|
|:--------:	|------------------------------------------------------------------	|:------------------:	|
|    26    	| [Don’t use raw types](item26.md)                                	| :white_check_mark: 	|
|    27    	| [Eliminate unchecked warnings](item27.md)                        	| :white_check_mark: 	|
|    28    	| [Prefer lists to arrays](item28.md)                              	| :white_check_mark: 	|
|    29    	| [Favor generic types](item29.md)                          	      | :white_check_mark: 	|
|    30    	| [Favor generic methods](item30.md)                               	|                    	|
|    31    	| [Use bounded wildcards to increase API flexibility](item31.md)  	| :white_check_mark: 	|
|    32    	| [Combine generics and varargs judiciously](item32.md)            	| :white_check_mark: 	|
|    33    	| [Consider typesafe heterogeneous containers](item33.md)         	| :white_check_mark: 	|
