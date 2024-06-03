
인터페이스는 인터페이스로부터만 상속 받을 수 있으며, 클래스와는 달리 다중 상속, 즉 여려 개의

인터페이스로부터 상속을 받는 것이 가능하다.

클래스의 상속과 마찬가지로 자손 인터페이스는 조상 인터페이스에 정의된 멤버를 모두 상속 받는

다.

인터페이스도 추상 클래스처럼 그 자체로는 인스턴스를 생성할 수 없으며, 추상 클래스가 상속을

추상 메서드를 완성하는 것처럼, 인터페이스도 자신에 정의된 추상 메서드의 몸통을 만들어주는

클래스를 작성해야 하며 인터페이스를 구현할 class에는 구현한다는 의미의 키워드 implements를

사용한다.

만약 구현하는 인터페이스의 메서드 중 일부만 구현한다면, abstract를 붙여서 추상 클래스로 선언

해야 하며 상속과 구현을 동시에 할 수도 있다.

```java
package ch07;

public class FighterTest{
	public static void main(String[] args) {
		Fighter fighter = new Fighter();
		if (fighter instanceof Unit) {
			System.out.println("fighter는 Unit 클래스의 자손 입니다.");
		}
		
		if (fighter instanceof Fightable) {
			System.out.println("fighter는 Fightable 인터페이스를 구현했습니다.");
		}
		
		if (fighter instanceof Movable) {
			System.out.println("fighter는 Movable 인터페이스를 구현했습니다.");
		}
		
		if(fighter instanceof Attackable) {
			System.out.println("fighter는 Attackable 인터페이스를 구현했습니다.");
		}
		
		if(fighter instanceof Object) {
			System.out.println("fighter는 Object 클래스의 자손 입니다.");
		}
		
	}
}

class Fighter extends Unit implements Fightable{
	public void move(int x, int y) {}
	public void attack(Unit u) {}
}

class Unit{
	int currentHP; //유닛의 체력
	int x; //유닛의 위치(x좌표)
	int y; //유닛의 위치(y좌표)
}

interface Fightable extends Movable, Attackable{}

interface Movable{
	void move(int x, int y);
}

interface Attackable{
	void attack(Unit u);
}
```


```java
fighter는 Unit 클래스의 자손 입니다.
fighter는 Fightable 인터페이스를 구현했습니다.
fighter는 Movable 인터페이스를 구현했습니다.
fighter는 Attackable 인터페이스를 구현했습니다.
fighter는 Object 클래스의 자손 입니다.
```

```java
	 	+-----------------+
       |     Object      |
       +-----------------+
               |
       +-----------------+
       |      Unit       |
       +-----------------+
       |  - int currentHP|
       |  - int x        |
       |  - int y        |
       +-----------------+
               |
       +-----------------+
       |    Fighter      |
       +-----------------+
       | + move(int x, int y) |
       | + attack(Unit u)     |
       +-----------------+
               |
+---------------------------+
|       Fightable           |
| <<interface>>             |
| + move(int x, int y)      |
| + attack(Unit u)          |
+---------------------------+
        /      \
       /        \
+--------------+ +-------------+
|   Movable    | |  Attackable |
| <<interface>>| | <<interface>>|
| + move(int x,| | + attack(Unit|
|    int y)    | |   u)         |
+--------------+ +-------------+
```


실제로 Fighter클래스는 Unit클래스로부터 상속 받고 Fightable 인터페이스만을 구현했지만,

Unit클래스는 Object클래스의 자손이고, Fightable인터페이스는 Attackable과 Movable 인터페이스

의 자손이므로 Fighter클래스는 이 모든 클래스와 인터페이스의 자손이 되는 셈이다.

인터페이스는 상속 대신 구현이라는 용어를 사용하지만, 인터페이스로부터 상속 받은 추상메서드를

구현하는 것이기 때문에 인터페이스도 다른 의미의 조상이라고 할 수 있다.

여기서 주의 깊게 봐두어야 할 것은 Movable인터페이스에 ‘void move(int x, int y)’와 같이 정의되어

있지만 사실 ‘public abstract’가 생략된 것이기 때문에 실제로 ‘public abstract void move(int x, int y)’

이다. 그래서, 이를 구현하는 Fighter클래스에서는 ‘void move(int x, int y)’의 접근 제어자를 반드시

public으로 해야 하는 것이다.

왜냐하면 Movable 인터페이스의 move 메서드가 public 이기 때문에, Fighter 클래스에서 move

메서드를 public으로 선언하지 않으면 "인터페이스의 move 메서드가 public인데, 왜 구현 클래스

에서는 public이 아니지?"라고 인식하여 컴파일 오류가 발생한다.










