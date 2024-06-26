나눗셈 / 와 나머지 값을 구하는 %연산을 수행할 때 ArithmeticException(산술 예외)의 오류가 나오는 경우가 있는데 이런 경우는 무한대의 값을 정수로는 표현할 수 없기 때문이다. 하지만 실수로 표현하는 경우에는 나눗셈 / 연산 하였을 시 오류가 발생하지 않고 infinity 라는 값이 나오고 나머지 % 연산 하였을 때는 Nan(Not a number)가 나오게 된다.

```java
public class ArithmeticException {
 
    public static void main(String[] args) {
                int x = 5;
                int y = 0;
                int result = x % y;
                System.out.println(result);
        }
}
```

```java
 Exception in thread "main" java.lang.ArithmeticException: / by zero
     at ch02.sec04.infinityAndNan.chek.main(chek.java:8)
```

```java
public class InfinityAndNanEx {

        public static void main(String[] args) {
                int x = 5;
                double y = 0.0;
                double result1 = x / y;
                double result2 = x % y;
                System.out.println(result1);
                System.out.println(result2 + ("(Not a Number)"));
        }
}
```

```java
//Infinity
//NaN(Not a Number)
```

프로그램을 사용할 때 연산 결과가 infinity, Nan형태의 값이 조금이라도 예상된다면 Double.isInfinite(), Double.isNan()메서드를 사용하여 boolean값을 확인해야 한다. 왜냐하면 infinity, Nan의 결과 값과 연산을 하게 된다면 계속 infinity, Nan의 결과가 나오기 때문이다.


```java
public class InfinityAndNanEx {
 
        public static void main(String[] args) {
                int x = 5;
                double y = 0.0;
                double result1 = x / y;
                double result2 = x % y;
                System.out.println(result1);
                System.out.println(result2 + ("(Not a Number)"));
                
                System.out.println(result1 + x);
                System.out.println(result2 + y + ("(Not a Number)"));
        }
}
```

```java
//Infinity
//NaN(Not a Number)
//Infinity
//NaN(Not a Number)
```

```java
public class isInfiniteAndisNanEx1 {
 
        public static void main(String[] args) {
                int x = 5;
                double y = 0.0;
                double result1 = x / y;
                double result2 = x % y;
                
                if(Double.isInfinite(result1)&&Double.isNaN(result2)) { 
                        // if문 조건식의 값이 True일 경우 실행
                        System.out.println("result1, result2 값은 Infinite, Nan 입니다 = True ");
                        System.out.println("result1 = "+Double.isInfinite(result1));
                        System.out.println("result2 = "+Double.isNaN(result2));
                        System.out.println("result1 + x = 연산을 하여도\"" + (result1+x) + "\"입니다.");// 문자열 결합 주의
                        System.out.println("result2 + x = 연산을 하여도\"" + (result2+x) + "\"입니다.");// 문자열 결합 주의
                        
                } else {
                        // if문 조건식의 값이 false일 경우 실행
                        System.out.println("result1, result2 값은 Infinite, Nan이 아니므로 false 입니다.");
                        System.out.println("result1="+Double.isInfinite(result1)); 
                        System.out.println("result2="+Double.isNaN(result2));
                        System.out.println("연산을 수행합니다. : result1 + x = " + (result1 + x)); // 문자열 결합 주의
                        System.out.println("연산을 수행합니다. : result2 + x = " + (result2 + x)); // 문자열 결합 주의
                }
 
        }
}
```

```java
result1, result2 값은 Infinite, Nan 입니다 = True 
result1 = true
result2 = true
result1 + x = 연산을 하여도"Infinity"입니다.
result2 + x = 연산을 하여도"NaN"입니다.
```

```java
public class isInfiniteAndisNanEx2 {
 
        public static void main(String[] args) {
                int x = 5;
                double y = 1.0;
                double result1 = x / y;
                double result2 = x % y;
                
                if(Double.isInfinite(result1)&&Double.isNaN(result2)) { 
                        // if문 조건식의 값이 True일 경우 실행
                        System.out.println("result1, result2 값은 Infinite, Nan 입니다 = True ");
                        System.out.println("result1 = "+Double.isInfinite(result1));
                        System.out.println("result2 = "+Double.isNaN(result2));
                        System.out.println("result1 + x = 연산을 하여도\"" + (result1+x) + "\"입니다.");// 문자열 결합 주의
                        System.out.println("result2 + x = 연산을 하여도\"" + (result2+x) + "\"입니다.");// 문자열 결합 주의
                        
                } else {
                        // if문 조건식의 값이 false일 경우 실행
                        System.out.println("result1, result2 값은 Infinite, Nan이 아니므로 false 입니다.");
                        System.out.println("result1="+Double.isInfinite(result1)); 
                        System.out.println("result2="+Double.isNaN(result2));
                        System.out.println("연산을 수행합니다. : result1 + x = " + (result1 + x)); // 문자열 결합 주의
                        System.out.println("연산을 수행합니다. : result2 + x = " + (result2 + x)); // 문자열 결합 주의
                }
        }
}
```

```java
//result1, result2 값은 Infinite, Nan이 아니므로 false 입니다.
//result1=false
//result2=false
//연산을 수행합니다. : result1 + x = 10.0
//연산을 수행합니다. : result2 + x = 5.0
```
