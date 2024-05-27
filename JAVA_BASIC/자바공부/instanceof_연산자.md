# instanceof연산자

참조 변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 instanceof 연산자를 사용한다.
주로 조건문에서 사용되며, instanceof의 왼쪽에는 참조 변수를 오른쪽에는 타입(클래스명)이 피연산자로 위치하며 
연산 결과로는 boolean값인 true와 false 중의 하나를 반환한다. true가 나온다면 참조 변수가 instanceof 연산을 통한
검사해본 타입으로 형 변환이 가능하다는 것을 뜻한다.

```java
package ch07;

public class InstanceofTest {

	public static void main(String[] args) {
		FireEngine fe = new FireEngine();
		
		if(fe instanceof FireEngine) {
			System.out.println("This a FireEngine instance.");
		}
		
		if(fe instanceof Car) {
			System.out.println("This is a Car instance");
		}
		
		if(fe instanceof Object) {
			System.out.println("This is an Object instance");
		}
		
		System.out.println(fe.getClass().getName());
		
	}

}

class Car {}
class FireEngine extends Car{}
```

