추상 클래스란 클래스를 설계도에 비유한다면, **추상 클래스는 미완성 설계도에 비유**할 수 있다.

미완성 설계도란, 단어의 뜻 그대로 완성되지 못한 채로 남겨진 설계도를 말한다.

클래스가 미완성이라는 것은 **멤버의 개수에 관계된 것이 아니라, 단지 미완성 메서드(추상메서드)**

**를 포함하고 있다는 의미이다.**

미완성 설계도로 완성된 제품을 만들 수 없듯이 **추상 클래스로 인스턴스는 생성할 수 없다.**

**추상 클래스는 상속을 통해서 자손클래스에 의해서만 완성될 수 있다.**

추상 클래스 자체로는 클래스로서의 역할을 다 못하지만, **새로운 클래스를 작성하는데 있어서**

**바탕이 되는 조상 클래스로서 중요한 의미를 갖는다.**

새로운 클래스를 작성할 때 아무 것도 없는 상태에서 시작하는 것보다는 완전하지는 못하더라도

어느정도 틀을 갖춘 상태에서 시작하는것이 좋다.

추상클래스를 사용하려면 class name 앞에 ‘abstract’를 사용하면 된다.

이렇게 함으로써 이 클래스를 사용할 때, **클래스 선언부의 abstract를 보고 이 클래스에는**

**추상 메서드가 있으니 상속을 통해서 구현해주어야 한다는 것을 쉽게 알 수 있다.**


```java
abstract class Player {
    abstract void play(int pos);
    abstract void stop();
}

class Audioplayer extends Player {
	//추상 메서드 구현
    void play(int pos) {
    
    //내용 생략
    }
    
	//추상 메서드 구현
    void stop() {
    //내용 생략
    }

}

abstract class AbstractPlayer extends Player {
    void play(int pos) {
        //내용 생략
    }
}
```