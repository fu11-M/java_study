# 인터페이스를 이용한 다중 상속

두 조상으로부터 상속 받는 멤버 중에서 멤버 변수의 이름이 같거나 메서드의 선언부가 일치하고

구현 내용이 다르다면 이 두 조상으로부터 상속 받는 자손클래스는 어느 조상의 것을 상속 받게

되는 것인지 알 수 없다. 어느 한쪽으로부터 상속을 포기하던가, 이름이 충돌하지 않도록

조상 클래스를 변경하는 수밖에 없다.

그래서 다중 상속은 장점도 있지만 단점이 더 크다고 판단하였기 때문에 자바에서는 다중 상속을

허용하지 않는다. 또 다른 객체 지향 언어인 C++에서는 다중 상속을 허용하기 때문에 자바는

다중 상속을 허용하지 않는다는 것이 단점으로 부각되는 것에 대한 대응으로 자바도 인터페이스를

이용하면 다중 상속이 가능하다. 라고 하는 것일 뿐 자바에서 다중 상속을 구현하는 경우는 없다.

인터페이스는 static상수만 정의할 수 있으므로 조상 클래스의 멤버 변수와 충돌하는 경우는 거의

없고 충돌 된다 하더라도 클래스 이름을 붙여서 구분이 가능하다.

그리고 추상 메서드는 구현 내용이 전혀 없으므로 조상 클래스의 메서드와 선언부가 일치하는 경우

에는 조상 클래스 쪽의 메서드를 상속받으면 되므로 문제되지 않는다.

그러나, 이렇게 하면 상속 받는 멤버의 충돌은 피할 수 있지만, 다중 상속의 장점을 잃게 된다.

만일 두 개의 클래스로부터 상속을 받아야 할 상황이라면, 두 조상 클래스 중에서 비중이 높은

쪽을 선택하고 다른 한쪽은 클래스 내부에 멤버로 포함시키는 방식으로 처리하거나 어느 한쪽이

필요한 부분을 뽑아서 인터페이스로 만든 다음 구현하도록 한다.


```java

package ch07;

public class TVCRimplement {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
	}

}

class TvImplement {
	
	protected boolean power;
	protected int channel;
	protected int volume;
	
	public void power() {};
	public void channelUp() {};
	public void channelDown() {};
	public void volumeUp() {};
	public void volumeDown() {};

}

class VCR{
	protected int counter;
	
	public void play() {
		
	}
	
	public void stop() {
		
	}
	
	public void reset() {
		counter = 0;
	}
	
	public int getCounter() {
		return counter;
	}
	
	public void setCounter(int c) {
		counter = c;
	}
}

interface IVCR{
	public void play();
	public void stop();
	public void reset();
	public int getCounter();
	public void setCounter(int c);
}

class TVCR extends TvImplement implements IVCR{
	VCR vcr = new VCR();
	
	public void play() {
		vcr.play();
	}
	
	public void stop() {
		vcr.stop();
	}
	
	public void reset() {
		vcr.reset();
	}

	
	public int getCounter() {
		return vcr.getCounter();
	}

	public void setCounter(int c) {
		vcr.setCounter(c);
	}
	
}

```


IVCR인터페이스를 구현하기 위해서는 새로 메서드를 작성해야 하는 부담이 있지만 이처럼

VCR클래스의 인스턴스를 사용하면 손쉽게 다중 상속을 구현할 수 있다.

또한 VCR클래스의 내용이 변경되어도 변경된 내용이 TVCR클래스에도 자동적으로 반영되는

효과도 얻을 수 있다.

사실 인터페이스를 새로 작성하지 않고도 VCR클래스를 TVCR클래스에 포함 시키는 것 만으로도

충분하지만, 인터페이스를 이용하면 다형적 특성을 이용할 수 있다는 장점이 있다.



















