switch 조건문은 if문과 달리 조건식이 오는 것이 아니라 변수의 값에 따라서 실행문이 결정된다.  Switch의 변수 값은 정수타입(byte, short, char, int, long)과 문자열 타입(String)만 사용할 수 있다. 
case와 같이 사용되는 기능인 default는 if문의 else와 비슷하게 작동한다. 선언된 변수의 값과 동일한 data를 갖는 case가 없을 경우 default가 선언된 곳이 작동한다.

switch가 선언된 변수의 값과 case data값이 같을 경우 해당 case가 작동하는데 break를 사용하여 나머지 case, default가 실행되지 않게 해주어야 한다. break를 사용하지 않을 경우
switch문의 변수와 값이 같은 case문에서 멈추지 않고 다른 모든 case, default문이 작동하게 된다.

if문에서는 조건식을 평가해서 true, false와 같이 2개의 결과 값만 가지기 때문에 경우의 수가 많아 질 수록 계속해서 else if문을 사용하여야 하기에 코드가 복잡해보일 수 있지만 switch문은 case를 통해서 변수의 값을 가지고 평가하여 if문보다 코드가 간결해질 수 있다. 

```java
public class Ex1 {

    public static void main(String[] args) {
        int num = 50;
        
        switch(num) {
        case 50:
            System.out.println("num은 50 입니다.");
            break;
        
        case 51:
            System.out.println("num은 51 입니다.");
            break;
            
        case 52:
            System.out.println("num은 52 입니다.");
            break;
            
        case 53:
            System.out.println("num은 53 입니다.");
            break;
            
        case 54:
            System.out.println("num은 54 입니다.");
            break;
            
        }
    }
}
```
```java
num은 50 입니다.
```

switch문에 num값인 50을 기준으로 case의 data인 50을 검사하고 동일할 경우 실행하고 break를 사용하여 switch문의 변수와 동일한 data를 갖는 case문의 실행부분에서 종료한다.
(switch문은 case, default가 사용되지만 만약 경우에 따라 switch문의 변수가 default의 실행 부분에 해당하지 않는 경우 및 이것과 비슷한 상황이라면 default는 생략가능하다.)

```java
public class Ex2 {

    public static void main(String[] args) {
        int num = 55;
        
        switch(num) {
        case 50:
            System.out.println("num은 50 입니다.");
            break;
        
        case 51:
            System.out.println("num은 51 입니다.");
            break;
            
        case 52:
            System.out.println("num은 52 입니다.");
            break;
            
        case 53:
            System.out.println("num은 53 입니다.");
            break;
            
        case 54:
            System.out.println("num은 54 입니다.");
            break;
            
        default:
            System.out.println("범위를 벗어 났습니다.");
        }
    }
}
```
```java
범위를 벗어 났습니다.
```


만약 int num의 값이 55일 경우 case의 data중  55가 없기 때문에 default값이 출력된다. 

```java
public class Ex3 {

    public static void main(String[] args) {
        int num = 50;
        
        switch(num) {
        case 50:
            System.out.println("num은 50 입니다.");
        
        case 51:
            System.out.println("num은 51 입니다.");
            
        case 52:
            System.out.println("num은 52 입니다.");
            
        case 53:
            System.out.println("num은 53 입니다.");
            
        case 54:
            System.out.println("num은 54 입니다.");
            
        default:
            System.out.println("범위를 벗어 났습니다.");
        }
    }
}
```
```java
num은 50 입니다.
num은 51 입니다.
num은 52 입니다.
num은 53 입니다.
num은 54 입니다.
범위를 벗어 났습니다.
```
break를 사용하지 않을 경우 case의 data와는 상관 없이 모든 실행 부분이 작동하기 때문에 일반적으로 break를 사용하는 것이 좋다.

```java
public class Ex4 {

    public static void main(String[] args) {
        int num = 55;
        
        switch(num) {
        case 50:
            System.out.println("num은 50 입니다.");
        
        case 51:
            System.out.println("num은 51 입니다.");
            
        case 52:
            System.out.println("num은 52 입니다.");
            
        case 53:
            System.out.println("num은 53 입니다.");
            
        case 54:
            System.out.println("num은 54 입니다.");
            
        default:
            System.out.println("범위를 벗어 났습니다.");
        }
    }
}
```

```java
범위를 벗어 났습니다.
```

case실행문에 break를 사용하지 않았는데 int num의 변수 값에 맞는 case문을 잘표현하였습니다. 위의 코드는 변수를 사용자가 직접 선언해서 case의 다른 경우의 수는 나올수 없고 default값이 나올수 밖에 없는 코드를 작성 하였지만 switch문은 경우의수가 존재하는 조건문 이기 때문에 이런 형태의 코드는 크게 의미가 없고 case50~54의 경우수를 고려하여 작성 하여야 한다.

```java
public class Ex5 {

    public static void main(String[] args) {
        int num = (int)(Math.random()*6) + 50; // 50, 51, 51, 53, 54, 55를 랜덤하게 표현한다.
        
        switch(num) {
        case 50:
            System.out.println("num은 50 입니다.");
        
        case 51:
            System.out.println("num은 51 입니다.");
            
        case 52:
            System.out.println("num은 52 입니다.");
            
        case 53:
            System.out.println("num은 53 입니다.");
            
        case 54:
            System.out.println("num은 54 입니다.");
            
        default:
            System.out.println("범위를 벗어 났습니다.");
            
        }
    }
}
```
```java
num은 50 입니다.
num은 51 입니다.
num은 52 입니다.
num은 53 입니다.
num은 54 입니다.
범위를 벗어 났습니다.
```

이렇게 랜덤하게 데이터를 받을 경우 break를 사용하지 않아 첫 번째 결과(50)로는 모든 case가 출력되었고 두 번째 결과(53)로는 53~54, default값이 출력되는 현상을 볼 수 있다.

```java
public class Ex6 {

    public static void main(String[] args) {
        int num = (int)(Math.random()*6) + 50; // 50, 51, 51, 53, 54, 55를 랜덤하게 표현한다.
        
        switch(num) {
        case 50:
            System.out.println("num은 50 입니다.");
            break;
            
        case 51:
            System.out.println("num은 51 입니다.");
            break;
            
        case 52:
            System.out.println("num은 52 입니다.");
            break;
            
        case 53:
            System.out.println("num은 53 입니다.");
            break;
            
        case 54:
            System.out.println("num은 54 입니다.");
            break;
            
        default:
            System.out.println("범위를 벗어 났습니다.");
            
        }
    }
}
```
```java
num은 51 입니다.
```

이처럼 break를 사용함으로써 switch문의 변수를 랜덤하게 받아온다고 가정 하였을 때 case data에 맞는 실행문만 출력할 수 있게 된다.



Java12부터는 switch문의 Expressions(표현식)을 사용할 수 있는데 switch Expressions(표현식)를 사용하면 switch값을 변수에 저장할 수 있고 switch값을 변수에 저장한다면 case의 모든 
값이 충족하지 않을 수 있기 때문에 이것을 나타내기 위한 default값은 생략할 수 없다. 
기존의 switch문에서 break를 사용하지 않고 -> (화살표) 사용해서 break없이 표현할 수 있어 간결하고 가독성이 높게 사용할 수 있으며 ->사용 이후 { }안의 실행부분이 
단일 실행일 경우 { }생략이 가능하고 연산을 사용할 경우에는 반드시 { }를 사용해야 한다. 

```java
public class Ex8 {

    public static void main(String[] args) {
        String grade = "B";
        
        int score1 = 0;
        
        switch(grade) {
        
        case "A" :
            score1 = 100;
            break; 
            
        case "B" : 
            int result = 100 -20;
            score1 = result;
            break;
        
        default :  
            score1 = 60;
        }
        
        System.out.println("score1 = "+score1);
        
        int score2 = switch(grade) {
        
        case "A" -> 100;
        
        case "B" -> {
            int result = 100 -20;  
            yield result; // score2 = result	
        }
        
        default -> 60;
        
        };
        
        System.out.println("score2 = "+score2);
    
    }
}
```
```java
score1 = 80
score2 = 80
```
int score1코드 부분은 기존 switch문을 표현 한 것이고 score2부터는 switch expression을 사용하여 int score2라는 변수에 switch문의 case의 반환 값을 대입하고 String grade가 "B" 이니
case B에서 int score2에 저장될 80을 위한 연산식을 수행하고 int result에 저장되어 yield를 사용해서 result값을 case 값으로 반환한다. 만약 yield를 사용하지 않는다면 int result = 100 -20; 
연산을 수행한 후 result가 case B에서 반환하지 않고 { }에서 값 만 가지고 있게 됨으로 score2라는 변수에 result를 직접 대입해주어야 한다.










