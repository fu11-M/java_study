**선언부만 작성하고 구현부는 작성하지 않은 채로 남겨둔 것**이 **추상 메서드이**다. 즉, **설계만 해놓고 실제 수행될**

**내용은 작성하지 않았기 때문에** **미완성 메서드**인것이다.

**메서드를 이와 같이 미완성 상태로 남겨 놓는 이유는 메서드의 내용이 상속받는 클래스에 따라 달라질 수 있기**

**때문에** **조상 클래스**에서는 **선언부만을 작성**하고, 주석을 덧붙여 어떤 기능을 수행할 목적으로 작성 되었는지

알려 주고, **실제 내용은 상속받는 클래스에서 구현하도록 비워 두는 것이다.**

그래서 추상클래스를 상속받는 **자손 클래스**는 **조상의 추상 메서드를 상황에 맞게 적절히 구현**해주어야 한다.

구현부가 없는 메서드가 무슨 의미가 있을까 싶기도 하겠지만, **메서드의 이름과 메서드의 작업에 필요한**

**매개변수, 그리고 작업의 결과로 어떤 타입의 값을 반환할 것 인가를 결정하는 것은 쉽지 않은 일이다.**

메서드를 사용하는 쪽에서는 메서드가 실제로 어떻게 구현되어 있는지 몰라도 **메서드의 이름과 매개변수,**

**리턴타입, 즉 선언부만 알고 있으면** **되므로** **내용이 없을 지라도 추상메서드를 사용하는 코드를 작성하는 것이**

**가능**하며, 실제로는 자손클래스에 구현된 완성된 메서드가 호출되도록 할 수 있다.

**추상메서드는 여러 클래스에 공통적으로 사용될 수 있는 클래스를 바로 작성하기도 하고**, **기존의 클래스의**

**공통적인 부분을 뽑아서 추상클래스로 만들어 상속하도록 하는 경우도 있다.**

**상속과 추상화의 차이점**으로 **상속**은 **자손 클래스를 만들어 조상 클래스를 상속 받아 구현, 확장하는 것이며**

**추상화**는 **기존의 클래스의 공통 부분을 찾아내서 자손클래스에 상속할 공통 조상클래스를 만드는 것이다.

```java
public class StarCraft {  
  
    public static void main(String[] args) {  
        Marine mr = new Marine();  
        Tank tk = new Tank();  
        DropShip ds = new DropShip();  
  
        mr.move(10,30);  
        mr.stop();  
        mr.stimPack();  
  
        tk.move(20, 50);  
        tk.stop();  
        tk.changeMode();  
  
        ds.move(10,30);  
        ds.stop();  
        ds.load();  
        ds.stop();  
        ds.unload();  
    }  
}  
  
abstract class Unit{  
    int x, y;  
    abstract void move(int x, int y);  
    void stop(){  
        //현재 위치에서 정지  
    }  
}  
class Marine extends Unit{  
    int x, y;  
  
    void move(int x, int y){  
        this.x = x;  
        this.y = y;  
        System.out.println("좌표 " + x + "," + y + " 쪽으로 Marine을 이동 시킵니다.");  
    }  
    void stimPack(){  
        System.out.println("Marine이 stimPack을 사용합니다. \n");  
    }  
  
    @Override  
    void stop() {  
        System.out.println("현재 위치에서 정지");  
    }  
}  
  
class Tank extends Unit{  
    int x, y;  
  
    void move(int x, int y){  
        this.x = x;  
        this.y = y;  
        System.out.println("좌표 " + x + "," + y + " 쪽으로 Tank을 이동 시킵니다.");  
    }  
  
    void stop() {  
        System.out.println("현재 위치에서 정지");  
    }  
  
    void changeMode(){  
        System.out.println("공격모드를 변환합니다.\n");  
    }  
}  
  
class DropShip extends Unit{  
    int x, y;  
    void move(int x, int y){  
        this.x = x;  
        this.y = y;  
        System.out.println("좌표 " + x + "," + y + " 쪽으로 DropShip을 이동 시킵니다.");  
    }  
  
    void stop() {  
        System.out.println("현재 위치에서 정지");  
    }  
  
    void load(){  
        System.out.println("대상을 태웁니다.");  
    }  
  
    void unload(){  
        System.out.println("대상을 내립니다.");  
    } 
}
```