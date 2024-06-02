**인터페이스**는 일종의 **추상 클래스**이다. **인터페이스**는 **추상 클래스처럼 추상 메서드를 갖지만 추상 클래스 보다**

**추상화 정도가 높아서 추상 클래스와 달리 몸통을 갖춘 일반 메서드 또는 멤버변수를 구성원으로 가질 수 없다.**

**오직 추상 메서드와 상수만 멤버로 가질 수 있으며**, 그외에 다른 어떠한 요소도 허용하지 않는다.

**추상 클래스를 부분적으로만 완성된 ‘미완성 설계도’**라고 한다면, **인터페이스는 구현된 것은 아무 것도 없고**

**밑그림만 그려져 있는 ‘기본 설계도’**라고 할 수 있다.

인터페이스도 추상 클래스처럼 완성되지 않은 불완전한 것이기 때문에 그 **자체만으로는 사용 되기 보다는**

**다른 클래스를 작성하는데 도움 줄 목적으로 작성된다.**

인터페이스 작성법은 class를 작성하는 것과 같으며 **접근 제어자로 public, default를 사용할 수 있다**.

일반적인 클래스의 멤버들과 달리 인터페이스의 멤버들은 다음과 같은 **제약사항**이 있다.

- 모든 멤버변수는 **public static final** 이어야 하며, 이를 생략할 수 있다.
- 모든 메서드는 **public abstract** 이어야 하며, 이를 생략할 수 있다. 단 static메서드와 default 메서드는 예외

인터페이스에 정의된 모든 멤버에 예외없이 적용되는 사항이기 때문에 제어자를 생략할 수 있는 것이며 편의상

생략하는 경우가 많다. 생략된 제어자는 컴파일 시에 컴파일러가 자동적으로 추가 해준다.

JDK1.8부터 인터페이스에 static 메서드와 default method의 추가를 허용하는 방안으로 변경 되었다.

```java

public interface InterfaceConstraints {
    public static final int SPADE = 4; // public static final int DIAMOND = 4
    final int DIAMOND = 3; // public static final int DIAMOND = 3
    static int HEART = 2; // public static final int HEART = 2
    int CLOVER = 1; // public static final int CLOVER = 1

    public abstract string getCardNumber();
    String getCardKind(); // public abstract String getCardKind();
}

```