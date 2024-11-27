## interface : 
interface는 Java에서 클래스 간의 계약(Contract)을 정의하는 추상 타입이며 클래스가 구현해야 할 메서드의 집합을 정의하고, 
이 메서드들은 반드시 해당 클래스에서 구현되어야 한다. 
즉, 인터페이스는 추상 메서드의 집합이며, 선언된 메서드는 기본적으로 abstract이다.
(Java 8부터는 디폴트 메서드와 정적 메서드를 포함할 수 있다.)

Java는 클래스의 다중 상속을 지원하지 않지만, 인터페이스는 여러 개를 구현할 수 있어 다중 상속의 유연성을 제공한다.
인터페이스는 public static final 상수만 포함할 수 있다.

추상 클래스와의 주요 차이로는, 추상 클래스는 abstract 메서드와 구체 메서드(구현된 메서드)를 모두 가질 수 있지만, 인터페이스는 기본적으로 메서드 구현을 가지지 않는다는 점이 있다.
___


- 클래스를 사용하는 쪽(User)과 클래스를 제공하는 쪽(Provider)이 있다.
- 메서드를 사용(호출)하는 쪽(User)에서는 사용하려는 메서드(Provider)의 선언부만 알면 된다.

```java
package ch07;

public class InterfaceTest {

	public static void main(String[] args) {
		A a = new A();
		a.methodA(new B());
	}
}

class A{
	public void methodA(B b) {
		b.methodB();
	}
}

class B{
	public void methodB() {
		System.out.println("methodB()");
	}
}
```
___

클래스 A를 User, 클래스 B를 Provider라고 가정하였을 때 클래스 A(User)는 클래스 B(Provider)의 인스턴스를 생성하고 메서드를 
호출하기 때문에 이 두 클래스는 서로 직접적인 관계에 있다.

이런 경우는 클래스 A를 작성하려면 클래스 B가 이미 작성되어 있어야 하며 클래스 B의 methodB()의 선언부가 변경되면, 이를 사용하는 클래스 A도 변경되어야 한다.

이와 같이 직접적인 관계의 두 클래스는 한 쪽(Provider)이 변경되면 다른 한 쪽(User)도 변경되어야 한다는 단점이 있다.

이런 단점을 극복하기 위해서 인터페이스를 매개체로 해서 클래스 A가 클래스 B를 직접 호출하지 않고 클래스 A가 인터페이스를 통해서 클래스 B의 메서드에 접근하도록 하면, 클래스 B에 변경 사항이 생기거나 클래스 B와 같은 기능의 다른 클래스로 대체 되어도 클래스 A는 전혀 영향을 받지 않도록 하는 것이 가능하다.
___

```java
package ch07;

public class InterfaceTest {
	public static void main(String[] args) {
		A a = new A();
		a.methodA(new B());
	}
}

class A{
	public void methodA(I i) {
		i.methodB();
	}
}

class B implements I {
	public void methodB() {
		System.out.println("methodB in B class");
	}
}

interface I{
	public abstract void methodB();
}
```
___

클래스 B에 정의된 메서드를 추상메서드로 정의하는 인터페이스 I를 정의한다. 그 다음에는 클래스 B가 인터페이스 I를 구현하도록 한다.

이제 클래스 A는 클래스 B대신 인터페이스 I를 사용해서 작성할 수 있으며 클래스 A를 작성하는데 있어서 클래스 B를 사용하지 않게 되었기 때문에 A클래스와 B클래스는 직접적인 관계에서 간접적인 관계로 된것이다.