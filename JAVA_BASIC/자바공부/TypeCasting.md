자동 타입 변환 (promotion) 
자동 타입 변환은 큰 허용 범위 타입의 변수에 작은 허용 범위 타입의 변수를 대입 하는 것을 말한다. int 타입의 변수에 byte타입의 변수를 대입한다고 
가정하였을 때 int 타입은 4byte의 메모리 크기를 가지고, byte 타입은 1byte의 메모리크기를 byte타입이 int타입보다 작기 때문에 int 타입의 변수에 자동으로 타입이 변환된다.
 
int variable = byte variable -> int 타입 4byte (32bit) = byte 타입 1byte (8bit)
 
float, double타입의 변수에 byte, short, char, int, long과 같은 정수타입이 대입될 경우에는 실수 타입의 허용 범위가 정수 타입의 허용범위 보다 무조건
크기 때문에 항상 자동으로 타입이 변환된다.
 
float variable = long variable
Double variable = long variable
 
Char타입의 경우 char타입의 변수를 int 타입의 변수에 대입한다고 하였을 때 자동으로 타입 변환이 되지만 더 작은 정수타입인 byte타입의 변수를 
char타입의 변수에 대입을 한다고 가정 하였을 때 작은 허용 범위의 타입에서 큰 허용 범위의 타입으로 자동 타입 변환이 일어남에도 불구하고 
컴파일 에러가 발생하는데 이유는 byte타입은 -128 ~ 127의 허용 범위를 가지는데 char타입은 0 ~ 65535의 허용범위를 가지는데 char타입에 음수를 
포함할 수 있는 범위가 없기 때문에 더 작은 타입이라도 자동 타입 변환이 일어나지 않는다. (강제 타입 변환을 사용해야 한다.)
 
Int, long variable = char variable(o)
Char vriable = byte, short, int, long variable (x)
 
강제 타입 변환 (casting)
강제 타입 변환은 작은 허용 범위 타입의 변수에 큰 허용 범위 타입의 변수를 대입 하는 것을 말한다. 하지만 작은 범위에서 큰 범위로 대입될 수 있지만 
큰 범위가 작은 범위안에 들어갈 수는 없다. 하여 강제 타입 변환(casting)을 사용하여 작은 허용 범위 타입의 변수에 큰 허용 범위 타입의 변수를 
사용할 수 있게 해준다. 강제 타입 변환(casting)의 목적은 원래의 값을 유지하면서 타입을 바꾸는 것이다.
 
정수타입 = (casting) 정수타입
byte variable = (byte) int variable -> byte 타입 1byte (8bit) = int 타입 4byte (32bit)
Int variable = (int) long variable -> int 타입 4byte (32bit) = long 타입 8byte (64bit)
 
정수타입 = (casting) 실수타입
Int variable = (int) float, double variable
 
정수 타입의 변수에 실수 타입의 변수를 대입할 경우 반드시 강제 타입 변환(casting)을 해줘야 한다. 왜냐하면 실수 타입의 변수에 정수 타입의 변수를 
대입할 경우에는 실수 타입이 허용범위가 더 크기 때문에 자동 타입이 변환이 일어나지만 정수 타입의 변수에 실수 타입의 변수를 대입할 경우에는 작은 범위의 변수에 큰 범위의 변수가 들어가는 것이기 때문에 강제 타입 변환(casting)을 해주어야 한다.
 
정수 타입의 변수에 실수 타입의 변수가 대입될 경우 소수점 이하 자리는 버려지고 정수부분만 대입된다.
 
Ex)
Double doubleVariable = 1.7
Int intVariable = (int) doubleVariable
System.out.print(intVariable)
출력 : 1
 
연산식에서의 자동 타입 변환(operation promotion)
Java는 실행 성능을 향상시키기 위해 컴파일 단계에서 연산을 수행한다. 예를 들어 int 타입의 변수에 리터럴 10+20을 사용한다고 가정 하여 보면
Java컴파일러는 int 타입의 변수에 리터럴이 대입하여 저장하는 순간 30으로 연산하고 바이트 코드를 생성한다. 이렇게 되면 바이크 코드 실행시에는 
연산을 하지 않게 되고 값이 바로 30이 나오게 된다(미리 30이 저장되었기 때문) 이러한 기술은 실행 시간 단축 및 최적화에 도움을 준다.
 
Ex)
Int intVariable = 10+20;
-> 저장하는 순간 30이 intVariable에 저장되고 소스코드에 대한 바이트코드 파일이 저장됨
 
변수가 피연산자로 오는 경우에는 리터럴과 다르게 바이트코드 실행시에 연산을 하게 되고 Java에서 정수연산은 결과값이 기본적으로 int 타입 이하의
타입들을 연산할 때는 모두 int 타입으로 간주하고 피연산자 중 하나라도 long 타입이 있을 경우 결과값이 long타입으로 나오게 된다.
이유는 정수 데이터 타입에서 크기에 따라 숫자를 표현할 수 있는 범위가 달라 연산을 수행할 경우 결과가 해당 데이터 타입의 범위를 초과(오버 플로우)
할 수 있기 때문에 int타입 이하는 int의 범주안에서, long타입은 long타입의 범주안에서 안전하게 처리(오버 플로우 방지) 가능하다.
 
(피연산자중 허용범위가 더 큰 크기의 타입 값으로 타입 변환)
 
예를 들어 2개의 byte 타입의 변수에 값을 각각 저장하고 연산할 때 대입되는 변수가 byte 타입의 변수라고 가정 하였을 때 대입되는 변수에는 피연산자들
이 연산을 하였기 때문에 int 타입으로 변환 후 연산하여 byte타입이 올 수 없고 int타입이 선언되어야 한다.
 
Ex)
byte byteVariable1  = 10;
byte byteVariable2 = 20;
byte byteVariable3 = byteVariable1 + byteVariable2 (x)
Int intVariable = byteVariable1 + byteVariable2 (o)
 
Ex)
Int intVriable1 = 10;
Int intVriable2 = 20;
Int intVriable3 = intVariable1 + intVariable2; (o)
 
Ex)
Int intVariable1 = 10;
long longVariable1 = 20;
Int intVariable2 = intVariable1 + longVraible1 (x)
Long longVariable2 = intVriable1 + longVriable1 (o)
 
실수 연산은 float타입과 float타입의 연산은 float타입의 변수에 연산이 가능하고 float 타입과 double타입을 연산을 하게 되면 허용 범위가 더 큰 타입인 double타입으로 결과값이 나오기 때문에 double타입으로 저장할 수 있다.
 
Ex)
Float floatVriable1 = 1.7;
Float floatVriable2 = 1.4;
Float floatVriable3 = floatVriable1 + floatVriable2; (o)
 
Ex)
Float floatVriable1 = 1.7;
double doubleVriable1 = 1.4;
Float floatVriable2 = floatVriable1 + doubleVriable1; (x)
Double doubleVriable2 = floatVriable1 + doubleVriable2; (o)
 
피연산자로 정수 타입의 변수와 실수 타입의 변수를 연산을 할 경우 실수가 허용범위가 더 크기 때문에 정수타입이 실수 타입으로 자동타입변환이 이루어지므로 결과값은 실수 타입의 변수에만 대입할 수 있다.
 
Int intVariable1 = 10;
Float floatVariable1 = 1.3f;
Int intResult = intVariable1 + floatVariable1; (x)
Float floatResult = intVariable1 + floatVariable1; (o) 
-> 11.3
 
정수 타입과 실수 타입의 연산에서 꼭 int타입의 결과값을 나타내야 한다면 실수 타입의 변수에 강제타입변환(casting)을 사용하여야 한다.
 
Int intVariable1 = 10;
Float floatVariable1 = 1.3f;
Int intResult = intVariable1 + (int) floatVariable1; (o) 
-> 11
 
정수 타입을 연산한다면 결과값에는 정수 값만 저장되기 때문에 정확한 결과값을 얻고 싶을 때는 정수타입 변수에 실수타입으로 강제타입변환(casting)을 해주게 되면 연산할 때 나머지 정수타입의 변수도 실수 타입으로 변환되어 실수타입의 결과값을 나타낼 수 있다.
 
int intVariable1 = 1;
int intVariable2 = 2;
Float floatResult1 = intVariable1 / intVariable2; (x) -> 0.0 (연산할 시점에 int타입으로 연산을 하고 float타입으로 저장된다.)
Float floatResult2 = (float) intVariable1 / intVariable2 (o) -> 0.5 (연산할 시점에 float타입으로 연산하고 float타입으로 저장된다.)
 
문자열과 숫자 연산
Int, long, float, double타입의 숫자 간의 + 연산은 덧셈을 하지만 숫자 와 string타입의 문자열을 + 연산할 경우 숫자 타입이 문자열 타입으로 자동 변환되어 덧셈을 하지 않고 결합된다.
 
Int intVariable1 = 3;
String strVariable1 = "4";
String strResult1 = intVariable1 + strVariable1;
-> 34; (문자열)
 
Int intVariable1 = 3;
String strVariable1 = "4";
Int intVariable2 = 7;
String strResult1 = intVariable1 + strVariable1 + intVariable2;
-> 347 (문자열)
 
String strVariable1 = "3";
int intVariable1 = 4;
Int intVariable2 = 7;
String strResult1 = strVariable1 + intVariable1 + intVariable2; 
-> 347 (문자열)
 
연산식에서 + 연산자가 나올 경우 연산식의 앞에 연산부터 순차적으로 수행한다.
 
Int intVariable1 = 3;
Int intVariable2 = 7;
String strVariable1 = "4";
String strResult1 = intVariable1 + intVariable2 + strVariable1; (숫자 간의 연산(3+7)이 먼저 일어나고 문자열 결합(10+"4")이 일어난다.)
-> 104 (문자열)
 
특정 부분을 우선 연산하고 싶을 경우 우선하고 싶은 연산식에 괄호()를 사용한다.
 
String strVariable1 = "3";
int intVariable1 = 4;
Int intVariable2 = 7;
String strResult1 = strVariable1 + (intVariable1 + intVariable2); 괄호()로 인해서 숫자 타입의 연산이 먼저 일어나고(11) 문자열 결합이 일어난다.(311)
-> 311 (문자열)
 
문자열 타입 변환
프로그램을 할 시 문자열을 연산할 경우 결합이 발생하여 문자열을 숫자 타입으로 변환하여 연산하여야 하는 상황이나 문자열을 기본 타입의 숫자형으로 표현해야 할 때 문자열을 기본 숫자 타입으로 변환하는 방법을 사용해야 하는데 방법은  래퍼 클래스.타입의 래퍼 클래스의 매서드(변환해야 하는 문자열)와 같다. 
 
타입의 래퍼 클래스는 java.lang패키지에 속해 있는 클래스이며 java의 기본 API중 하나 이다.
타입 변환 작업을 해야 할 때 타입을 매서드를 통해서 변환 하는 작업이 이루어져야 하는데 이러한 작업이 이루어지는 래퍼 클래스 안에 속해 있는 변환 
매서드를 사용하려면 래퍼 클래스를 참조 하여야 하기 때문에 타입의 기본 형태로는 참조 할 수 없고 객체 형태가 되어야 참조할 수 있어 값이 대입되는
변수의 기본 타입의 래퍼 클래스 사용한다. 
 
 byte = Byte.parseByte(???)
 short = Short.parseShort(???)
 int = Integer.parseInt(???)
 long = Long.parseLong(???)
 float = Float.parseFloat(???)
 double = Double.parseDouble(???)
 
 (parse = 해석한다.)
 
 String strVariable1 = "15";
 byte byteVariable1 = Byte.parseByte(strVariable); 
 위 와 같이 작성하였을 때 byteVarialbe1을 출력하면 문자열 "15"가 아닌 byte타입의 정수형 15가 결과값으로 나온다.
 
 String strVariable1 = "15";
 short shortVariable1 = Short.parseShort(strVariable1);
 
 String strVariable1 = "15";
 int intVarialble1 = Integer.parseInt(strVariable1);
 
 String strVariable1 = "15";
 float floatVariable1 = Float.parseFloat(strVariable1);
 
 String strVariable1 = "15";
 double doubleVariable1 = Double.parseDouble(strVariable1);
 
 String strVariable2 = "true";
 boolean booleanVariable1 = Boolean.parseBoolean(striVariable2);
 
 기본 타입 문자열 변환
 기본 숫자형 타입을 문자열로 변경할 경우에는 래퍼 클래스String을 참조하여 기본 타입을 문자열로 변환해주는 valueOf라는 메소드를 사용하여야 한다.
 
 int intVariable1 = 10;
 String strVariable1 = String.valueOf(intVariable1);
 
 boolean booleanVariable1 = true;
 String strVariable1 = String.valueOf(booleanVariable1);