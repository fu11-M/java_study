Enum(열거형)은 서로 관련된 상수를 편리하게 선언하기 위한 것으로 여러 상수를 정의할 때 사용하면 유용하다.
자바에서의 열거형은 열거형이 갖는 값 뿐만 아니라 타입도 관리하기 때문에 보다 논리적인 오류를 줄일 수 있다.

```java
class Card{
	static final int CLOVER = 0;
	static final int HEART = 1;
	static final int DIAMOND = 2;
	static final int SPADE = 3;
	
	static final int TWO = 0;
	static final THREE = 1;
	static final FOUR = 2;
	
	final int kind;
	final int num;
}
```

일반적인 클래스 변수를 사용하면 위와 같이 표현해야 하지만 Enum(열거형)은 서로 관련된 상수들을 모아 아래와 같이 간편하게 표현할 수 있다.

```java
class Card{
	enum kind {CLOVER, HEART, DIAMOND, SPADE} // 열거형 Kind를 정의
	enum Value {TWO, THREE, FOUR} // 열거형 Value를 정의
	
	final Kind kind;
	final Value value;
}
```

기존의 C언어에서는 타입이 달라도 값이 같으면 조건식 결과가 참(true)이였으나, 자바의 열거형은 타입에 안전한 열거형(typesafe enum)이라서
실제 값이 같아도 타입이 다르면 컴파일 에러가 발생한다. 이처럼 값 뿐만 아니라 타입까지 체크하기 때문에 타입에 안전하다고 하는 것이다.

열거형은 기본적으로 첫 번째 값을 0부터 시작하는 정수 값을 부여한다.

 

```java
if(Card.CLOVER == Card.TWO) // (무늬 == 숫자) true지만 flase이어야 의미상 맞음
if(Card.Kind.CLOVER == Card.Value.TWO) // 값은 같지만 타입이 다름 (컴파일 에러)
```

원래 상수의 값이 바뀌면, 해당 상수를 참조하는 모든 소스를 다시 컴파일해야 한다는 것이다. 
하지만 열거형 상수를 사용하면, 기존의 소스를 다시 컴파일 하지 않아도 된다. 

### 열거형의 사용 방법

```java
enum Direction{ EAST, SOUTH, WEST, NORTH }
```

```java
class Unit{
	int x;
	int y;
	
	Driection dir;
	
	void init(){
		dir = Direction.EAST;
	}
}
```

열거형을 사용하기 위해서 클래스에 선언하면 열거형에 선언된 값 외에는 어떤 값도 사용할 수 없다.

 

### 열거형 상수의 비교

열거형 상수의 비교는 ==와 compareTo( )만 사용 가능하며 <, > 등 비교 연산자는 사용 불가능하다.

```java
if(dir == Direction.EAST){
	x++;
}else if (dir > Direction.WEST) { // 에러. 열거형 상수에 비교연산자 사용 불가
}else if (dir.compareTo(Direction.WEST) > 0 { // compareTo()는 사용 가능
}
```

compareTo( )를 사용하여 값이 같으면 0, 오른쪽이 크면 양수, 왼쪽이 크면 음수의 결과가 나온다.

## 열거형의 조상 - java.lang.Enum

- 모든 열거형은 Enum의 자손이며 아래의 메서드를 상속받는다.

| Class<E> getDeclaringClass( ) | 열거형의 Class 객체를 반환한다. |
| --- | --- |
| String name( ) | 열거형 상수의 이름을 문자열로 반환 |
| int ordinal( ) | 열거형 상수가 정의된 순서를 반환 |
| T valueOf(Class<T> enumType, String name) | 지정된 열거형에서 name과 일치하는 열거형 상수를 반환한다. |

이외에도 values( ), valueOf( )처럼 컴파일러가 자동적으로 추가해주는 메서드가 있다.

vlalues( )메서드는 Enum클래스의 값을 가져오고 

```java
static E values()
static E valueOf(String name)
```

valueOf 메서드는 열거형 상수의 이름으로 문자열 상수에 대한 참조를 얻을 수 있게 해준다.

```java
Directuon d = Direction.valueOf("WEST");
System.out.println(d); // WEST
System.out.println(Direction.WEST == Direction.valueOf("WEST")); // true
```

```java
package ch07;

enum Direction{ EAST, SOUTH, WEST, NORTH }

public class EnumEx {

	public static void main(String[] args) {
		Direction direction1 = Direction.EAST;
		Direction direction2 = Direction.valueOf("WEST");
		Direction direction3 = Enum.valueOf(Direction.class, "EAST");
		
		System.out.println("direction1 : " + direction1);
		System.out.println("direction2 : " + direction2);
		System.out.println("direction3 : " + direction3);
		
		System.out.println("direction1 == direction2 : " + (direction1 == direction2));
		System.out.println("direction1 == direction3 : " + (direction1 == direction3));
		System.out.println("direction1.equals(direction3) : " + direction1.equals(direction3));
		System.out.println("direction1.compareTo(direction3) : " + direction1.compareTo(direction2));
		
		switch(direction1) {
			case EAST : 
				System.out.println("The direction is EAST.");
				break;
			
			case SOUTH :
				System.out.println("The direction is SOUTH.");
				break;
				
			case WEST :
				System.out.println("The direction is WEST.");
				break;
				
			case NORTH : 
				System.out.println("The direction is NORTH.");
				break;
			
			default : 
				System.out.println("Invalid direction.");
				break;
		}
		
		Direction[] directionArr = Direction.values();
		
		for(Direction direction : directionArr) {
			System.out.printf("%s = %d %n", direction.name(), direction.ordinal());
		}
	}
}

```

```java
direction1 : EAST
direction2 : WEST
direction3 : EAST
direction1 == direction2 : false
direction1 == direction3 : true
direction1.equals(direction3) : true
direction1.compareTo(direction3) : -2
The direction is EAST.
EAST = 0 
SOUTH = 1 
WEST = 2 
NORTH = 3 
```

## 열거형 멤버 추가

Enum클래스에 정의된 ordinal( )이 열거형 상수가 정의된 순서를 반환하지만, 이 값을 열거형 상수의 값으로 사용하지 않는 것이 좋다. 이 값은 내부적인 용도로만 사용되기 위한 것이기 때문이다.
열거형 상수의 값이 불 연속적인 경우에는 열거형 상수의 이름 옆에 원하는 값을 괄호( )와 함께 적어주면 된다.

```java
enum Direction {EAST(1), SOUTH(5), WEST(-1), NORTH(10)}
```

그리고 지정된 값을 저장할 수 있는 인스턴스 변수와 생성자를 새로 추가해 주어야 한다.
열거형 상수를 모두 정의한 다음에 다른 멤버들을 추가 해야 하며 열거형 상수의 마지막에 ;를 꼭 
붙여야 한다.

```java
enum Direction{
	EAST(1), SOUTH(5),WEST(-1), NORTH(10);
	private final int value;
	
	//생성자 
	Direction(int value) {
		this.value = value;
	}
	
	public int getValue() {
		return value;
	}
}
```

열거형 Direction에 새로운 생성자가 추가되었지만, 열거형의 객체를 생성할 수 없다.
열거형의 생성자는 제어자가 묵시적으로 private이기 때문이다.

```java
Direction direction = new Direction(1); //에러 열거형의 생성자는 외부에서 호출불가
```

열겨형은 하나의 상수에 여러 값을 지정할 수 있지만 그에 맞게 인스턴스 변수와 생성자 등을 새로 
추가해주어야 한다.