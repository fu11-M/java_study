
try-catch문은 예외가 발생한 경우와 발생하지 않았을 때의 흐름(문장의 실행 순서)이 달라진다.

try블럭 내에서 예외가 발생한 경우 :

발생한 예외와 일치하는 catch블럭이 있는지 확인하고 일치하는 catch블럭을 찾게 되면,

그 catch블럭 내의 문장들을 수행하고 전체 try-catch문을 빠져나가서 그 다음 문장을 계속해서

수행한다. 만일 일치하는 catch블럭을 찾지 못하면 예외는 처리되지 못한다.

try블럭 내에서 예외가 발생하지 않은 경우:

catch블럭을 거치지 않고 전체 try-catch문을 빠져나가서 수행을 계속한다.

catch블럭은 괄호()와 블럭{} 두 부분으로 나눠져 있는데, 괄호()내에는 처리하고자 하는 예외와 같은

타입의 참조 변수를 선언해야 한다.

예외가 발생하면, 발생한 예외에 해당하는 클래스의 인스턴스가 만들어지고 위의 코드에서는

ArithmeticException이 발생했으므로 ArithmeticException 인스턴스가 생성되고 검사하게 된다.

모든 예외 클래스는 Exception클래스의 자손이므로, catch블럭의 괄호( )에 Exception클래스 타입의

참조 변수를 선언해 놓으면 어떤 종류의 예외가 발생하더라도 이 catch블럭에 의해 처리된다.

# printStackTrace()와 getMessage()

예외가 발생했을 때 생성되는 예외 클래스의 인스턴스에는 발생한 예외에 대한 정보가 담겨 있으며,

getMessage()와 printStackTrace()를 통해서 이 정보들을 얻을 수 있다.

catch블럭의 괄호( )에 선언된 참조 변수를 통해 이 인스턴스에 접근할 수 있다. 이 참조 변수는

선언된 catch블럭 내에서만 사용 가능하며, 자주 사용되는 메서드는 다음과 같다.

printStackTrace() - 예외 발생 당시의 호출 스택(Call Stack)에 있었던 메서드의 정보와 예외 메시지를

화면에 출력한다.

getMessage() - 발생한 예외 클래스의 인스턴스에 저장된 메시지를 얻을 수 있다.

```java
public class ExceptionEx2 {

	public static void main(String[] args) {
		int number = 100;
		int result = 0;
		
		for(int i = 0; i < 10; i++) {
			try {
				result = number / (int)(Math.random() * 10);
				System.out.println(result);
			} catch (ArithmeticException e) {
				System.out.println("0");
			}
		}
	}
}

```

```java
50
33
예외의 메시지:/ by zero
0
예외의 메시지:/ by zero
0
12
20
100
25
100
12
java.lang.ArithmeticException: / by zero
	at ExceptionEx2.main(ExceptionEx2.java:9)
java.lang.ArithmeticException: / by zero
	at ExceptionEx2.main(ExceptionEx2.java:9)

```

위의 코드와 같이 printStackTrace() 또는 getMessage()와 같은 메서드를 통해서 예외의 발생 원인을

알 수 있다.

# 멀티 catch블럭

JDK1.7부터 여러 catch블럭을 ‘ | ’ 기호를 이용해서, 하나의 catch블럭으로 합칠 수 있게 되었으며, 이를 ‘멀티 catch블럭’이라 한다.

‘멀티 catch블럭’을 이용하면 중복된 코드를 줄일 수 있으며 ‘ | ’ 기호로 연결할 수 있는 예외 클래스의 개수에는 제한이 없다.

만일 멀티 catch블럭의 ‘ | ’기호로 연결된 예외 클래스가 조상과 자손의 관계에 있다면 컴파일 에러가 발생한다.

그 이유는 두 예외 클래스가 조상과 자손의 관계에 있다면, 그냥 조상 클래스만 써주는 것과 똑같기 때문에 불필요한 코드는 제거하라는 의미에서 에러가 발생하는 것이다.

그리고 멀티 catch는 하나의 catch블럭으로 여러 예외를 처리하는 것이기 때문에, 발생한 예외를 멀티 catch블럭으로 처리하게 되었을 때,

멀티 catch블럭 내에서는 실제로 어떤 예외가 발생한 것인지 알 수 없다.

그래서 참조 변수로 멀티 catch블럭에 ‘ | ’ 기호로 연결된 예외 클래스들의 공통 분모인 조상 예외 클래스에 선언된 멤버만 사용할 수 있다.

밀티 catch블럭에 선언된 참조 변수는 상수이므로 값을 변경할 수 없다는 제약이 있는데, 이것은 여러 catch블럭이 하나의 참조 변수를

공유하기 때문에 생기는 제약으로 실제로 참조 변수의 값을 바꿀 일은 없다.

```java
public class Exception3 {
    public static void main(String[] args) {
        try{
            Exception exception = new Exception("고의로 발생시켰음.");
            throw exception;
            
        } catch (Exception exception){
            System.out.println("에러 메시지:" + exception.getMessage());
            exception.printStackTrace();
        }
        System.out.println("프로그램이 정상 종료되었음");
    }
}
```

```java
에러 메시지:고의로 발생시켰음.
프로그램이 정상 종료되었음
java.lang.Exception: 고의로 발생시켰음.
	at Exception3.main(Exception3.java:4)
```

그리고 컴파일러가 예외 처리를 확인하지 않는 RuntimeException클래스들은 ‘unchecked예외’ 라고 부르고, 예외 처리를 확인하는 Exception클래스들은 checked예외 라고 부른다.












