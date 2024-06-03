다형성에 대해 학습할 때 자손 클래스의 인스턴스를 조상 타입의 참조 변수로 참조하는 것이 가능

하다는 것을 배웠다. 인터페이스 역시 이를 구현한 클래스의 조상이라 할 수 있으므로 해당

인터페이스 타입의 참조 변수로 이를 구현한 클래스의 인스턴스를 참조 할 수 있으며, 인터페이스

타입으로의 형 변환도 가능하며 메서드의 매개변수의 타입으로 사용될 수 있다.

인터페이스 타입의 매개변수가 갖는 의미는 메서드 호출 시 해당 인터페이스를 구현한 클래스의

인스턴스를 매개변수로 제공해야 한다는 것이다.

리턴 타입으로 인터페이스를 사용한다면 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를

반환한다는 것을 의미한다.

```java
package ch07;

public class ParserTest {

	public static void main(String[] args) {
		Parseable parser = ParserManager.getParser("XML");
		parser.parse("document1.xml");
		
		parser = ParserManager.getParser("HTML");
		parser.parse("document2.html");
	}

}

interface Parseable{
	public abstract void parse(String fileName);
}

class ParserManager{
	public static Parseable getParser(String type) {
		if(type.equals("XML")) {
			return new XMLParser();
		} else {
			Parseable parseable = new HTMLParser();
			return parseable;
		}
	}
}

class XMLParser implements Parseable{
	public void parse(String fileName) {
		System.out.println(fileName + "- XML parsing completed.");
	}
}

class HTMLParser implements Parseable{
	public void parse(String fileName) {
		System.out.println(fileName + "- HTML parsing completed.");
	}
}


```


Parseable 인터페이스는 구문 분석(parsing)을 수행하는 기능을 목적으로 추상 메서드

‘parse(String fileName)’을 정의 그리고 XMLParser클래스와 HTMLParser클래스는

Parseable인터페이스를 구현 하였고 ParserManager클래스의 getParser메서드는 매개변수로

넘겨받는 type의 값에 따라 XMLParser 인스턴스 또는 HTMLParser인스턴스를 반환 한다.

getParser메서드의 수행결과로 참조 변수 parser는 XMLParser 인스턴스의 주소 값을 갖게된다.

마치 ‘Parseable parser = new XMLParser();’ 이 수행된것과 같다.

참조 변수 parser를 통해 parse()를 호출하면, parser가 참조하고 있는 XMLParser인스턴스의

parse메서드가 호출된다.

만일 나중에 새로운 종류의 XML구문 분석기 NewXMLPaser클래스가 나와도 ParserTest클래스는 변경할

필요 없이 PaserManger클래스에의 getParser메서드에서 ‘return new XMLParser();’ 대신

‘return new NewXMLParser();’로 변경하기만 하면된다.(interface를 사용한 장점)















