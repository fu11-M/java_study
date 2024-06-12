객체 지향 개념에서 다형성이란 ‘여러 가지 형태를 가질 수 있는 능력’ 을 의미하며, 자바에서는 한 타입의 참조 변수로 여러 타입의 객체를 참조할 수 있도록 함으로써

다형성을 구현하였다. 이를 좀 더 구체적으로 말하자면, 조상 클래스 타입의 참조 변수로 자손 클래스의 인스턴스를 참조할 수 있도록 하였다는 것이다.

```java
//상속 관계라고 가정
Tv t = new Tv();

captionTv c = new CaptionTv();
```

지금까지는 생성된 인스턴스를 다루기 위해서, 인스턴스의 타입과 일치하는 타입의 참조 변수 만을 사용했다.

이처럼 인스턴스의 타입과 참조 변수의 타입이 일치하는 것이 보통이지만 **상속 관계에 있을 경우, 다음과 같이 조상 클래스 타입의 참조 변수로 자손 클래스의**

**인스턴스를 참조하도록 하는 것도 가능하다.**

```java
//상속 관계라고 가정
captionTv c = new CaptionTv()
Tv t = new captionTv()
```

위의 코드에서 CaptionTv인스턴스 2개를 생성하고, 참조 변수 c와 t가 생성된 인스턴스를 하나씩 참조하도록 하였다.

이 경우 **실제 인스턴스가 CaptionTv타입이라 할지라도, Tv타입의 참조 변수 t로는 CaptionTv 인스턴스의 모든 멤버를 사용할 수 없다.**

Tv타입의 참조 변수로는 CaptionTv 인스턴스 중에서 **Tv클래스의 멤버들(상속받은 멤버 포함)만 사용할 수 있다.**

따라서, **생성된 CaptionTv 인스턴스 중에서 Tv클래스에 정의 되지 않은 멤버는 tv타입의 t참조 변수로는 사용이 불가능하다.**

결국 둘 다 같은 타입의 인스턴스지만 **참조 변수의 타입에 따라 사용할 수 있는 멤버의 개수가 달라진다.**

반대로 자손 타입의 참조 변수로 조상 타입의 인스턴스를 참조하는 것은 불가능하다.

그 이유는 실제 인스턴스인 Tv의 멤버 개수보다 참조 변수 c가 사용할 수 있는 멤버 개수가 더 많기 때문에 참조를 허용하지 않는다.

**이유는 자손 타입의 참조 변수로 조상 타입의 인스턴스를 참조하는 것은 존재하지 않는 멤버를 사용하고자 할 가능성이 있으므로**

**허용하지 않는 것**이다. 즉, 참조 변수가 사용할 수 있는 멤버의 개수는 인스턴스의 멤버 개수보다 같거나 적어야 한다.

**클래스는 상속을 통해서 확장될 수는 있어도 축소될 수는 없기에** 조상 인스턴스의 멤버 개수는 자손 인스턴스의 멤버 개수보다 항상 적거나 같다.

인스턴스 타입과 일치하는 참조 변수를 사용하면 인스턴스의 멤버들을 모두 사용할 수 있는데 굳이 왜 조상 타입의 참조 변수를 사용해서 인스턴스의 일부 멤버만을

사용하도록 하는지는 뒤에 나온다.

## 참조 변수의 형 변환

기본형 변수와 같이 **참조 변수도 형 변환이 가능하다**. 단, **서로 상속 관계에 있는 클래스 사이에서만 가능하기**

**때문에** **자손 타입의 참조 변수를 조상 타입의 참조 변수로**

**조상 타입의 참조 변수를 자손 타입의 참조 변수로의 형 변환만 가능**하다.

(자바에서는 조상과 자식 관계만 존재하기 때문에 **형제 개념은 없다.** )

**기본형 변수의 형 변환은 작은 자료형에서 큰 자료형의 형 변환은 생략이 가능하듯이**, **참조형 변수의 형 변환에서는 자손 타입의 참조 변수를 조상 타입으로 형 변환하는 경우에는 형 변환을 생략할 수 있다.**

자손 타입 → 조상 타입(Up-castring) : 형 변환 생략 가능

자손 타입 ← 조상 타입(Down-castring) : 형 변환 생략 불가

자손 타입으로의 형 변환은 생략할 수 없으며 형 변환을 수행하기 전에 **instanceof연산자를 사용해서 참조 변수가 참조하고 있는 실제 인스턴스의 타입을 확인하는 것이 안전하다.**

참조 변수간의 형 변환은 캐스트 연산자를 사용하여 괄호( ) 안에 변환하고자 하는 타입의 이름을 적어주면 된다.

```java
package ch07;

public class CastingTest1 {

	public static void main(String[] args) {
		Car car = null;
		FireEngine fe = new FireEngine();
		FireEngine fe2 = null;
		
		fe.water();
		
		car = fe; //부모 클래스에 형변환을 하기 때문에 형변환을 생력가능하다.
		//car.water(); Car타입의 참조 변수로는 water()를 호출할 수 없다.
		fe2 = (FireEngine)car;
		fe2.water();
	}

}

class Car{
	String color;
	int door;
	
	void drive() {
		System.out.println("drive");
	}
	
	void stop() {
		System.out.println("stop");
	}
}

class FireEngine extends Car{
	void water() {
		System.out.println("water!!");
	}
}
```

```java
water!!
water!!
```

형 변환은 참조 변수의 타입을 변환하는 것이지 인스턴스를 변환하는 것이 아니기 때문에 참조 변수의 형변환은 인스턴스에 아무런 영향을 미치지 않고

단지 참조 하고 있는 인스턴스에서 사용할 수 있는 멤버의 범위(개수)를 조절하는 것 뿐이다.

```java
package ch07;

public class CastingTest2 {

	public static void main(String[] args) {
		Car car = new Car();
		Car car2 = null;
		FireEngine fe = null;
		
		car.drive();
		fe = (FireEngine)car; // 컴파일은 가능하지만 실행시 에러가 발생함.
		fe.drive();
		car2 = fe;
		car2.drive();
	}
}

class Car{
	String color;
	int door;
	
	void drive() {
		System.out.println("drive");
	}
	
	void stop() {
		System.out.println("stop");
	}
}

class FireEngine extends Car{
	void water() {
		System.out.println("water!!");
	}
}
```

```java
drive()
java.lang.ClassCastException: Car
			at CastingTest2.main(CastingTest2.java:8)
```

CastingTest1의 fe2 = (FireEngine)car; 코드는 형 변환이 가능하지만 Castring2의 fe = (FireEngine)car; 코드는 형 변환이 불가능한 이유는

CastingTest1의 fe2 = (FireEngine)car; 코드는 참조 변수 car가 이와 같이 작성되어 있어 Car car = null; 참조하고 있는 인스턴스가 없고

Castring2의 fe = (FireEngine)car; 코드는 참조 변수 car가 Car car = new Car();와 같이 Car의 인스턴스를 참조 하고 있어

조상 타입의 인스턴스를 자손 타입의 참조 변수로 참조하는 것은 허용되지 않기 때문이다.

컴파일 시에는 참조 변수 간의 타입만 체크하기 때문에 실행 시 생성될 인스턴스의 타입에 대해서는 전혀 알지 못하기 때문에 컴파일 시에는 문제가 없지만 실행 시에 에러가 발생하여 비정상적으로 종료된다.

조상 타입의 인스턴스를 자손 타입의 참조 변수로 참조하는 것은 허용되지 않는다.

서로 상속 관계에 있는 타입 간의 형 변환의 형 변환은 양방향으로 자유롭게 수행될 수 있으나, 참조 변수가 가리키는 인스턴스의 자손 타입으로 형 변환은 허용되지 않기 때문에 참조 변수가 가리키는 인스턴스의 타입이 무엇인지 
instanceof 연산자를 사용하여 확인하는 것이 중요하다.