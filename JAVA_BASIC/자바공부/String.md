String 타입의 객체는 변경이 불가능한 특성을 가지고있다.

문자열을 비교할 때 == 이 아닌 equals를 사용하는 이유는 문자열이 참조 타입이기 때문이다. 참조타입의 변수에 == 를 사용하게 되면 참조타입의 변수의 값은 객체의 주소로 되어 있으니 변수의 내용이 아니라 주소가 같은지  비교하게 되는 것이다.

객체를 생성하는 연산자는 new 연산자를 사용하고 해당 타입을 사용한다.

```java
public class StringEx1 {

    public static void main(String[] args) {
        String var1 = "문자열";
        String var2 = new String("문자열");
        
        boolean bool1 = var1 == var2;
        boolean bool2 = var1.equals(var2);
        
        if(bool1) {
            System.out.println("(var1 == var2) = "+bool1);
        }else {
            System.out.println("(var1 == var2) = "+bool1);
        }
        
        if(bool2) {
            System.out.println("var1.equals(var2) = "+bool2);
        }else {
            System.out.println("var1.equals(var2) = "+bool2);
        }
        
    }

}
```

```java
(var1 == var2) = false
var1.equals(var2) = true
```

String타입의 var1과 var2의 리터럴이 같을 때 ==연산의 결과는 var1의 객체 주소와 var2의 객체 주소가 다르기 때문에 faslse가 나오게 되고 equals를 사용하였을 때의 결과는 var1과 var2가 객체는 다르지만 내용이 같기 때문에 ture가 나오게 된다.

Java는 new 연산자를 사용하지 않고 var1과 var2와 같이 문자열 리터럴이 동일하면 String객체를 공유하도록 되어있다.

```java
public class StringEx2 {

    public static void main(String[] args) {
        String var1 = "문자열";
        String var2 ="문자열";
        boolean bool = var1 == var2;
        
        if(bool) {
            System.out.println("(var1 == var2) = "+bool);
        }else {
            System.out.println("(var1 == var2) = "+bool);
        }
    }
}
```
```java
(var1 == var2) = true
```
new 연산자를 사용하지 않은 변수인 var1과 var2가 리터럴이 같기 때문에 객체 한곳에서 공유 하여 var1과 var2가 같은 주소값을 가지게 된다.



문자열에서 특정 문자열을 추출 하고 싶을 경우 문자열이 저장되어 있는 변수의 객체를 참조하여 charAt()메소드에 문자열 index의 위치를 입력하여 index에 맞는 위치의 문자열을 얻을 수 있다.

```java
public class CharAt {

    public static void main(String[] args) {
        String strVar = "A, B, C, D";
        char strExtraction = strVar.charAt(6);
        System.out.println(strExtraction);
    }

}
```
```java
C
```

스택 영역에 저장되어 있는 strVar 변수에 A, B, C, D가 저장되어 있는 힙영역의 객체 주소 값이 저장되어 있는데 strVar.charAt(6)을 사용한다면 strVar변수의 값인 객체의 주소를 찾아가 힙 영역의 A, B, C, D객체를 참조하여 index의 7번째 위치에 존재하는 C를 추출하게 된다.


문자열의 길이가 얼마나 되는지 숫자로 알고 싶다면 lenth메소드를 사용하여 얻을 수 있다.
```java

public class Lengh {

    public static void main(String[] args) {
        String strVar = "안녕하세요 저는 ㅁㅁㅁ 입니다.";
        int strVarLengh = strVar.length();
        System.out.println(strVarLengh);
    }
}
```
```java
17
```
strVar 변수에  힙 영역의 "안녕하세요 저는 ㅁㅁㅁ 입니다." 가 저장되어 있는 객체 주소 값이 저장되어 있어 strVar.lengh를 사용하면 strVar 변수의 값인 힙 영역의 객체 주소를 찾아가 "안녕하세요 저는 ㅁㅁㅁ 입니다."  문자열의 index수를 출력한다.

문자열의 특정 부분을 다른 문자열로 변경하고 싶을 경우에는 replace("수정 하고 싶은 기존 문자열", "수정 될 문자열") 메소드를 사용하여 값을 얻을 수 있다.

```java
public class Replace {

    public static void main(String[] args) {
        String str = "1, 2, 3, 4, 5, 6, 7, 8, 10";
        String strCorrection = str.replace("10", "9");
        System.out.println(str);
        System.out.println(strCorrection);
    }
}
```
```java
1, 2, 3, 4, 5, 6, 7, 8, 10
1, 2, 3, 4, 5, 6, 7, 8, 9
```
replace()메소드를 사용하여 반환한 문자열은 str변수가 참조하는 객체의 값이 수정된 것이 아니라  replace의 매개 값 과 같이 변경하여 새로운 문자열의 객체를 만드는 것이다.

문자열의 특정 부분을 끊어서 표현하고 싶다면 subString(index, index)메소드를 사용 하여 값을 얻을 수 있다.
```java
public class Ex4SubString {

    public static void main(String[] args) {
        String day_time = "2023-11-17_01:46";
                
        String day = day_time.substring(0,10);
        String time = day_time.substring(11);
        
        System.out.println("day : "+day);
        System.out.println("time : "+time);
    }
}
```
```java
day : 2023-11-17
time : 01:46
```
day_time의 변수의 객체를 참조하여 substring(0, 10)을 사용하면 index0번~10번까지 끊어서 heap영역에 객체를 저장하고 객체의 주소가 day변수의 값이 되고 day_time의 변수의 객체를 참조하여 substring(11)을
사용하면 index11번 부터 index끝 번호 까지 끊어 heap영역에 객체를 저장하고 객체의 주소가 time변수의 값이 된다.

substring()메소드의 매개값으로 index번호가 1개만 온다면 1개의 index번호 부터 index끝 번호까지 잘라내어 표현한다.

특정 문자열의 index값을 얻기 위해서는 indexOf( )메소드를 사용하여 얻을 수 있다.

```java
public class Ex5IndexOf {

    public static void main(String[] args) {
        String studyChart = "Java, Jsp, Spring";
        
        int springIndex = studyChart.indexOf("Spring");
        int htmlIndex = studyChart.indexOf("Html");
        
        System.out.println("spring문자의 index는" + springIndex + "번 부터 시작입니다.");
        System.out.println(htmlIndex+"은 포함되어 있지 않다는 뜻 입니다.");
        
    }
}
```
```java
spring문자의 index는11번 부터 시작입니다.
-1 은 포함되어 있지 않다는 뜻 입니다.
```
indexOf(Spring)를 사용하면 Spring문자열이 시작되는 index값을 반환하고 만약 study변수의 문자열에 없는 값을 사용한다면 -1이 나오게 된다.

특정 문자를 기준으로 문자열을 나누고 싶다면 split("문자열을 나누는 기준")을 사용하면 된다.
```java
public class Ex6Split {

    public static void main(String[] args) {
        String studyChart = "Java, Jsp, Spring";
        
        String[] studyArray = studyChart.split(", ");
        System.out.println("1."+studyArray[0]);
        System.out.println("2."+studyArray[1]);
        System.out.println("3."+studyArray[2]);
    }
}
```
```java
1.Java
2.Jsp
3.Spring
```

studyChart의 "Java, Jsp, Spring" 문자열을 split메소드를 사용하여 ", " (쉼표) 기준으로 나누어 배열에 할당하게 되면 ", " 기준 처음 분리 되는 "Java"가 studyArray 배열의  index가 [0]이 되고 다음 순서로 분리되는 Jsp가 [1] Spring이 [2]가 되는 것이다.


참조 타입 변수는 null이라는 값으로 초기화를 할 수 있는데 아직 번지가 저장되어 있지 않다 라는 의미이며 객체가 생성되지 않은 상태이다. 객체가 생성되지 않았을 뿐 변수의 초기값으로 사용할 수 있기 때문에 stack영역에 null값이 생성된다.

```java
public class NullEx1 {

    public static void main(String[] args) {
        String strVar1 = "문자열";
        String strVar2 = null;
        
        System.out.println("var1 = "+strVar1.length());
        System.out.println("var2 = "+strVar2.length());
    }
}
```
```java
var1 = 3
Exception in thread "main" java.lang.NullPointerException: Cannot read the array length because "arrayVar" is null
at ch05.ReferenceType.NullEx1.main(NullEx1.java:10)
```
strVar1을 사용하여 lenth()메소드를 사용한다면 strVar1변수의 값은 객체의 번지이기 때문에 객체를 참조하여 "문자열" 이란 데이터의 길이를 표현할 수 있지만 strVar2변수를 사용하여 lenth()메소드를 사용한
다면 strVar2의 값은 null인 상태 즉 객체가 없는 상태인데 객체를 참조하는 메소드를 사용하면 "NullPointerException" 이라는 예외(프로그램 실행 도중 발생하는 오류)가 발생한다.