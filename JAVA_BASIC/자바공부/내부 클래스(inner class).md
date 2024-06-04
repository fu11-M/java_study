내부 클래스는 클래스 내에 선언된 클래스이며 클래스에 다른 클래스를 선언하는 이유는 두 클래스가 서로 긴밀한 관계에 있기 때문이다

한 클래스를 다른 클래스의 내부 클래스로 선언하면 두 클래스의 멤버들 간에 서로 쉽게 접근할 수 있다는 장점과 외부에는 불필요한 클래스를

감춤으로써 코드의 복잡성을 줄일 수 있다는 장점을 얻을 수 있다.

## 내부 클래스의 종류와 특징

내부 클래스의 종류는 변수의 선언 위치에 따른 종류와 같다. 내부 클래스는 마치 변수를 선언하는 것과 같은 위치에 선언할 수 있으며,

변수의 선언 위치에 따라 인스턴스 변수, 클래스변수(static변수), 지역 변수로 구분되는 것과 같이 내부 클래스도 선언 위치에 따라

다음과 같이 구분되어 진다. 내부 클래스의 유효 범위와 성질이 변수와 유사하다.

|인스턴스 클래스|외부 클래스의 멤버 변수 선언 위치에 선언하며, 외부 클래스의 인스턴스 멤버처럼 다루어 진다. 주로 외부 클래스의 인스턴스 멤버들과 관련된 작업에 사용될 목적으로 선언된다.|
|---|---|
|스태틱 클래스|외부 클래스의 멤버 변수 선언 위치에 외부 클래스의 static 멤버 처럼 다루어진다. 주로 외부 클래스의 static멤버, 특히 static메서드에서 사용될 목적으로 선언된다.|
|지역(local) 클래스|외부 클래스의 메서드나 초기화 블럭 안에 선언하며, 선언된 영역 내부에서만 사용될 수 있다.|
|익명 클래스|클래스의 선언과 객체의 생성을 동시에 하는 이름 없는 클래스(일회용)|

내부 클래스도 클래스이기 때문에 abstract나 final과 같은 제어자와 멤버 변수들처럼 접근 제어자도

사용이 가능하다.
```java

public class InnerEx1 {
	
	class InstanceInner{
		int iv = 100;
		//static int cv = 100; // static변수를 선언할 수 없음
		final static int CONST = 100; // final static은 상수 허용
	}
	
	static class StaticInner{
		int iv = 200;
		static int cv = 200; // static 클래스만 static 멤버를 정의할 수 있음
	}
	
	void myMethod() {
		class LocalInner{
			int iv = 300;
			//static int cv = 300; //static 변수 사용x
			final static int CONST = 300;
		}
	}
	
	public static void main(String[] args) {
		System.out.println(InstanceInner.CONST);
		System.out.println(StaticInner.cv);
	}
}

```

내부 클래스 중에서 static 클래스만 static멤버를 가질 수 있다.

final과 static이 동시에 붙은 변수는 상수(constant)이므로 모든 내부 클래스에서 정의가 가능하다.



내부 클래스에서 외부 클래스의 변수들에 대한 접근성

```java

public class InnerEx2 {
	private int outerIv = 0;
	static int outerCv = 0;
	
	class InstanceInner{
		int iiv = outerIv; // 외부 클래스의 private멤버도 접근 가능하다.
		int iiv2 = outerCv;
	}
	
	static class StaticInner{
		//int siv = outerIv; // 스태틱 클래스는 외부 클래스의 인스턴스 멤버에 접근할 수 없다.
		static int scv = outerCv;
		
	}
	
	void myMetgod() {
		int Iv = 0;
		final int LV = 0;
		
		class LocalInner{
			int liv = outerIv;
			int liv2 = outerCv;
			int liv3 = Iv;
			int liv4 = LV;
		}
	}
}

```

인스턴스클래스(InstanceInner)는 외부 클래스(InnerEx2)의 인스턴스멤버이기 때문에

인스턴스변수 outerIv와 static변수 outerCv를 모두 사용할 수 있다. 심지어는 outerIv의

접근 제어자가 private일지라도 사용가능하다.

static 클래스(StaticInner)는 외부 클래스(InnerEx3)dml static 멤버이기 때문에 외부 클래스의

인스턴스 멤버인 outerIv와 InstanceInner를 사용할 수 없고 static 멤버인 outerCv만 사용할 수 있다.

지역 클래스(LocalInner)는 외부 클래스의 인스턴스 멤버와 static멤버를 모두 사용할 수 있으며,

지역 클래스가 포함된 메서드에 정의된 지역변수도 사용할 수 있다.

단, final이 붙은 지역변수만 접근 가능한데 그 이유는 메서드가 수행을 마쳐서 지역변수가

소멸된 시점에도, 지역 클래스의 인스턴스가 소멸된 지역 변수를 참조하려는 경우가 발생할 수 있기

때문이다.

(JDK1.8부터 지역 클래스에서 접근하는 지역 변수 앞에 final을 생략할 수 있게 바뀌었다.)





















