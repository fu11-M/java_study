Scanner는 입력된 데이터를 읽는 도구 중 하나이며 텍스트를 입력 받고 처리하기 위한 객체이다 Java표준 라이브러리인 java.util 패키지에 포함되어 
제공되는 클래스이다. 주로 표준 입력 스트림의 객체를 포함한 System.in과 사용된다.
 
일반적으로 키보드와 연결되어 키보드로 입력한 텍스트(문자열, 숫자 입력을 받을 때 사용되기 때문에 데이터를 읽을 수 있는 Scanner의 객체를 생성하고 Scanner 
객체에 System.in을 매개변수로 받아 입력소스로 지정하여 사용자가 입력한 키보드 입력 데이터를 Scanner를 통해 읽을 수 있다.
 
Java에서 다른 패키지에 있는 Class를 현재 패키지에 작성하고 있는 Class에 가져와 사용할 경우에는 컴파일러에게 사용해야 하는 클래스가 어떤 패키지에 
있는지 알려주기 위해서 import 사용해야 하는 패키지명.클래스 형식으로 작성 해야 한다. Scanner 같은 경우에는 java.util 패키지에 속해 있으니
Import java.util.Scanner 와 같이 작성하면 Scanner를 쓸 수 있게 된다. 만약 import를 해주지 않는다면 컴파일러가 Scanner의 클래스를 찾지 못하여
컴파일 오류가 나게 된다.
 
Import java.util.Scanner
 
Scanner 객체를 생성하여 참조하는 방법은 기본 타입과 마찬가지로 Scanner타입의 변수를 설정하고 이 변수에 new연산를 통해서 Scanner의 객체를 생성
하여 대입하고 Scanner의 객체의 매개변수는 system.in을 받아 키보드 입력 데이터를 Scanner를 통해서 읽을 수 있다.
 
Scanner scanner = new Scanner(System.in)
 
Scanner의 객체가 저장된 Scanner타입의 scanner변수를 사용하여 Scanner클래스에 있는 nextLine(다음 줄의 입력을 읽어온다), nextInt(입력을 읽어 정수로 반환.), nextFloat(입력을 읽어 실수로 반환.)과 같은 메소드를 사용할 수 있는데 키보드에서 입력 받은 데이터를 읽고 원하는 값으로 파싱하고 필요한 형태로 변환하기 위해 사용되며 Scanner로 읽어온 값을 사용자가 원하는 반환 값에 맞는 데이터 타입으로 변수를 지정하여 대입한 후 키보드로부터 읽은 데이터를
데이터 타입에 맞게 저장할 수 있다. 
 
    System.out.pirnt("이름을 입력하세요:");
    String name = scanner.next line();
     
    System.outprit("나이를 입력하세요:");
    int age = scanner.nextInt();
     
기본적으로 Scanner클래스의 메소드 들은 Enter키가 입력될 때 까지 대기 상태가 되고 Enter키가 입력되는 순간 키보드에서 입력된 데이터는 문자열로 먼저 값을 받게 되는데 그러면 읽어온 데이터를 대입할 변수는 String만 사용해야 하는 건가 라는 생각이 들 수 있지만 나이 혹은 숫자 연산을 해야 하는 코드일 경우 숫자로 표현해야 하니 nextInt()를 사용하여 대입될 때 타입 변환 하거나 문자열을 기본 타입으로 변환하는 코드(parse.숫자형 타입)를 작성하면 된다.
     
    System.outprit("A값을 입력하세요:");
    String strA = Scanner.nextline();
    int  intA = Integer.parseInt(strA);
     
    System.outprit("B값을 입력하세요:");
    int intB = scanner.nextInt();
     
    int result = intA + intB;
     
    System.out.print("A+B 값:"+result);
     
Scanner 클래스의 nextLine 메소드와 nextInt, long, flaoat, double, boolean등의 차이점은 메소드 마다 데이터를 읽는 타입이 다르다는 것과
구분자로 인한 데이터처리 방식에 차이가 있다.
 
next메서드들은 구분자를 통해서 데이터를 나누거나 구분하는데 구분자는 Space, Tap, Enter와 같은 공백문자로 구성되어 있다. 
즉 데이터를 입력 받을 때 공백문자( Space, Tap, Enter)가 있으면 공백문자 앞 뒤의 데이터가 구분 지어 진다는 뜻이다.
 
사용자가 Scanner를 사용하고 System.out.print(문자열)로 값을 입력하도록 콘솔에 출력한다고 가정하면 값을 입력하고 넘어가기 위해 Enter라는 키를
눌러야 하는데 이는 next메소드들의 구분자중 하나이기 때문에 사용자가 값을 입력하고 넘어가려고 하는 순간 next메소드들에게는 공백문자로 취급되어
구분자로 인식되기 때문에 Enter입력시점에 데이터가 분할될 수 있다.
 
nextLine 메서드는 구분자를 Space, Tap을 사용하여 구분하고 Enter키는 구분자로 사용하지 않기 때문에 콘솔에서 값을 입력하고 Enter를 누르면
Enter키 자체도 문자열에 포함되어 데이터를 읽는다 하지만 Space, Tap이 온다면 데이터는 구분 지어진다.
 
Sysotem.out.print("이름을 입력하세요:"); -> AAABBB333 콘솔입력(Enter) (Enter키가 구분자로 사용되지 않음)
String strVariable1 = Scanner.nextLine(); -> 콘솔에 Enter키를 통해서 입력 했을 때 데이터가 구분되지 않고 Enter키를 포함한 문자열을 전체를 읽는다.
 
Sysotem.out.print("이름을 입력하세요:"); -> AAA BBB 333 입력 (문자열 사이의 공백 AAA뒤 Space을 기준으로 데이터를 분할하여 읽는다.)
String strVariavle1 = Scanner.nextLine(); -> 하여 AAA만 저장되고 나머지 BBB 333은 Buffer라는 공간에 임시 저장됨
String strVariable2 = Scanner.nextLine(); -> nextLine 메소드를 다시 호출하면 처리되지 않았던 BBB 데이터를 저장할 수 있음
String strVariable3 = Scanner.nextLine() -> BBB 뒤 구분자Space를 기준으로 구분되었으니 333데이터를 얻기 위해 nextLine메소드를 호출 해야한다.
 
 
NextInt는 NextLine과 다르게 구분자를 Space, Tap, Enter를 사용하여 구분한다. 콘솔에 값을 입력 하고 다음으로 넘어가려면  줄 바꿈을 위해 Enter를 
누르게 되는데 공백문자인 Enter키를 누르는 순간 데이터를 구분 지어야 되는 구분자로 인식하여 콘솔에 입력한 데이터와 Enter자체의 기능인 줄 바꿈 데이터가 나뉘어서 저장되고 Buffer에 줄 바꿈 데이터가 저장되어 지는 상황이다. Buffer에 있는 줄 바꿈 데이터는 빈문자열로 되어있다. 그 이유는 콘솔에서 
데이터를 작성을 모두 하고 Enter키를 눌러 데이터와 줄 바꿈이 줄 구분되어 콘솔입력이 끝났기 때문에 줄 바꿈이 일어나고 이후 내용이 있을 수 없다.
 
System.out.print("나이를 입력하세요:"); -> 콘솔에 12입력 
Int intVariavle1 = scanner.nextInt(); ->  동시에 12와 Enter자체의 기능인 줄 바꿈 내용이 나뉘어 저장됨 (12 | "")
String StrVariable1 = scanner.nextLine(); -> Buffer에 있던 줄 바꿈을 저장함 ("")
 
nextInt메소드를 사용한다음에 입력 받는 다른 nextLine메소드를 사용하면 "나이를 입력하세요" 문자열에 12라고 작성하고 Enter키로 입력하는 순간
줄 바꿈이 Buffer에 저장되고 Buffer에 있는 줄 바꿈이 Scanner에 의해 읽혀 adressNum에 저장되고 "주민번호 앞자리를 입력하세요"는 그냥 출력 문자열이 되어진다.