

- 개발시간 단축
    
    ```
     인터페이스를 사용하여 프로그램을 작성하면 동시에 다른 한쪽에서는 인터페이스를 구현하는 클래스를 작성
    
     하고 있을 때 인터페이스를 구현하는 클래스가 작성될 때 까지 기다리지 않고 동시에 개발할 수 있다.
    ```
    
- 표준화 가능
    
    ```
     프로젝트에 사용 되는 기본 틀을 인터페이스로 작성한 다음, 개발자에게 인터페이스를 구현하여 프로그램을
    
     작성 하도록 함으로 보다 일관되고 정형화된 프로그램의 개발이 가능하다.
    ```
    
- 서로 관계 없는 클래스들에게 관계를 맺어 줄 수 있다.
    
    ```
     서로 상속관계에 있지 않고, 같은 조상클래스를 가지고 있지 않은 서로 아무런 관계도 없는 클래스들에게 
    
     하나의 인터페이스를 공통적으로 구현하도록 함으로써 관계를 맺어 줄 수 있다.
    ```
    
- 독립적인 프로그래밍이 가능하다. (종속되지 않는 프로그램 작성)
    
    ```
     인터페이스를 이용하면 클래스의 선언과 구현을 분리시킬 수 있기 때문에 실제 구현에 독립적인 프로그램을 
    
     작성 하는 것이 가능하다. 클래스와 클래스간의 직접적인 관계를 인터페이스를 이용해서 간접적인 관계로 
    
     변경하면, 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능하다.
    ```
    

**게임에 나오는 유닛을 클래스로 표현하고 이들의 관계를 class와 interface로 구현해보자**

게임에 나오는 모든 유닛들의 최고 조상은 Unit클래스이고 유닛의 종류는 지상유닛(GroundUnit)과 공중유닛

(AirUnit)으로 나누어진다.

그리고 지상유닛에는 Marine, SCV(건설인부), Tank가 있고, 공중 유닛으로는 Dropship(수송선)이 있다.

SCV에게 Tank와 Dropship과 같은 기계화 유닛을 수리할 수 있는 기능을 제공하기 위해 repair메서드를

정의한다면 다음과 같다.

```java
void repair(Tank t){} 
void repair(Dropship d){}
```

이런 식으로 수리가 가능한 유닛의 개수만큼 다른 버전의 오버로딩된 메서드를 정의해야 할 것이다.

이것을 피하기 위해 매개 변수의 타입을 이 들의 공통 조상으로 하면 좋겠지만 Dropship은 공통조상이

다르기 때문에 공통 조상의 타입으로 메서드를 정의한다고 해도 최소한 2개의 메서드가 필요할 것이다.

```java
void repair(GroundUnit gu){} 
void repair(AirUnit au){}
```

GroundUnit의 자손 중에는 Marine과 같이 기계화 유닛이 아닌 클래스도 포함될 수 있기 때문에 repair메서드의

매개변수 타입으로 GroundUnit은 부적합하다.

현재의 상속관계에서는 이들의 공통점은 없다. 이 때 인터페이스를 이용하면 기존의 상속체계를 유지하면서 이들

기계화 유닛에 공통점을 부여할 수 있다.

(현재의 상속관계에서 공통점이 없을 때 인터페이스를 사용한다면 상속 관계를 유지하면서 공통점을 부여할 수

있다.)

Repairable라는 인터페이스를 정의하고 수리가 가능한 기계화 유닛에게 이 인터페이스를 구현하도록 하면된다.

인터페이스를 통해서 3개의 클래스에는 같은 인터페이스를 구현 했다는 공통점이 생겼고 인터페이스 Repairable

에 정의된 것은 없고, 단지 인스턴스의 타입 체크에만 사용된다.

그리고 repair메서드의 매개 변수의 타입을 Repairable로 선언하면, 이 메서드의 매개 변수로 Repairable인터

페이스를 구현한 클래스의 인스턴스만 받아들여지는 것이다.

```java
import java.awt.event.TextEvent;

public class RepairableTest {

    public static void main(String[] args) {
        Tank tank = new Tank();
        Dropship dropship = new Dropship();
        Marine marine = new Marine();
        SCV scv = new SCV();

        scv.repair(tank);
        scv.repair(dropship);
        //scv.repair(Marine);
        //Marine은 Repairable 인터페이스를 구현하지 않았음으로 SCV클래스의 repair메서드의 매개변수로 Marine을 사용할 수 없다.
    }
}

interface Repairable{}

class Unit{
    int hitPoint;
    final int MAX_HP;

    Unit(int hp){
        MAX_HP = hp;
    }
}

class GroundUnit extends Unit{
    GroundUnit(int hp){
        super(hp);
    }
}
class AirUnit extends Unit{
    AirUnit(int hp){
        super(hp);
    }
}

class Tank extends GroundUnit implements Repairable{
    Tank(){
        super(150);
        hitPoint = MAX_HP;
    }

    public String toString(){
        return "Tank";
    }
}

class Dropship extends AirUnit implements Repairable{
    Dropship(){
        super(125);
        hitPoint = MAX_HP;
    }

    public String toString(){
        return "Dropship";
    }
}

class Marine extends GroundUnit{
    Marine(){
        super(40);
        hitPoint = MAX_HP;
    }
}

class SCV extends GroundUnit implements Repairable{
    SCV(){
        super(60);
        hitPoint = MAX_HP;
    }

    void repair(Repairable repairable){
        if(repairable instanceof Unit){
            Unit unit = (Unit) repairable;

            while (unit.hitPoint != unit.MAX_HP){
                unit.hitPoint++;
            }
            System.out.println(unit.toString() + "의 수리가 끝났습니다.");
        }
    }
}
```

```java
Tank의 수리가 끝났습니다. 
Dropship의 수리가 끝났습니다.
```
