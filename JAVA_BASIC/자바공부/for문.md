for반복문은 프로그램 내에서 실행문을 일정 횟수만큼 반복하여 수행하도록 제어하는 명령문 중 하나이며 반복 횟수를 지정하고 싶을 때 많이 사용된다.
만약 더하기를 100번 정도 하고싶다고 한다면 int num = num+1, int num += 1 와 같은 코드를 100번 작성해야하기 때문에 프로그래머가 작성하기에 피로하고
작성하는 시간에 비해 비효율적이기 때문에 반복문을 사용해서 간단하게 표현할 수 있다.

for문은 초기화식,  조건식, 증감식을 모두 포함하고 있고 코드로 사용하는 방식은 for(초기화식; 조건식; 증감식) {실행문}와 같이 사용된다. 초기식은 조건식, 증감식에서 사용할 변수를 초기화 하는 역할을 하고
조건식은 초기화된 변수를 사용한 연산을 통한 결과 값이 true면 반복하는 역할을 하는데 변수가 true일 경우 계속해서 반복한다. 증감식은 초기화 된 변수가 조건식을 통해서 반복될 때 마다 변수의 값을 얼마씩
증감시킬 것인지를 나타낸다.

for문의 실행 흐름은 다음과 같다.

                
for ( 초기화식;  조건식;  증감식  ) {

    실행문
    
    }

처음 for문을 작성하면 1.초기화식을 먼저 수행하고 2.조건식을 검사한다음 true이면 실행문을 수행한 다음 4.초기화식에 사용된 변수를 증감시키는데 다음 반복이 될 때는 4.증감된 변수를 2.조건식에서 검사하고 3.실행문을 출력하는 것을 반복한다.

```java

public class Ex1 {

    public static void main(String[] args) {
        int num = 1;
        int result = 0;
        for(int i = 1; i<=99; i++) {
            result = num + i;
            System.out.println(num + "+" + i + " = " + result);
        }
        
    }

}
```
```java
1+1 = 2
1+2 = 3
1+3 = 4
1+4 = 5
1+5 = 6
1+6 = 7
1+7 = 8
1+8 = 9
1+9 = 10
1+10 = 11
     '''
1+90 = 91
1+91 = 92
1+92 = 93
1+93 = 94
1+94 = 95
1+95 = 96
1+96 = 97
1+97 = 98
1+98 = 99
1+99 = 100
```

숫자 1에 1~99까지의 숫자를 더하는 반복문을 작성할 때 먼저 고정 숫자인 1을 int num에 1을 초기화 하고 결과 값을 담을 int result를 0으로 초기화 한 다음 for반복문을 작성하여 초기화 식에서 int i = 1로 초기 화 한 한다음 조건식에서 i가 99보다 작거나 같을 때 까지 i++증감식을 사용한 즉 덧셈을 표현하는데 이 말은 즉 i 를 1로 초기화 하여 99가 될 때 까지 i에 1씩 더하여 1~99까지의 숫자를 표현한다는 뜻이 된다.
그리고 결과 값을 담는 result는 for문의 { } 실행부분에서 i가 증감 되기전 num(1) + i(1) 연산을 먼저 수행하여 결과를 result에 담고 print문을 출력한 다음 i는 다시 증감되어 num(1) + i(2) 연산을 수행하는 식이 며 이것을 i가 99가 될 때 까지 즉 99번 반복한다.


```java
public class Ex2 {

    public static void main(String[] args) {
        int num = 1;
        int result = 0;
        for(int i = 0; i <= 99; i++) {
            result = num + i;
            System.out.println(num + "+" + i + " = " + result);
        }
        System.out.println(num + "+" + i + " = " + (num + i));
    }
}
```
```java
Exception in thread "main" java.lang.Error: Unresolved compilation problems: 
    i cannot be resolved to a variable
    i cannot be resolved to a variable

at Sec05.For.Ex2.main(Ex2.java:12)
```

```java
Exception in thread "main" java.lang.Error: Unresolved compilation problems: 
    i cannot be resolved to a variable
    i cannot be resolved to a variable

at Sec05.For.Ex2.main(Ex2.java:12)
```

for문의 초기화식에 선언된 변수(i)는 for문의 실행 블록 { }안에서만 사용되는 local변수이기 때문에 실행 블록을 벗어나서 사용을 한다면 오류가 발생한다.

```java
public class Ex3 {

    public static void main(String[] args) {
        int num = 1;
        int result = 0;
        for(int i = 1; i<=99; i++) {
            result = num + i;
            System.out.println(num + "+" + i + " = " + result);
        }
        System.out.println("num = " + num);
        System.out.println("result = " + result);
    }
}
```

```java
1+1 = 2
1+2 = 3
1+3 = 4
1+4 = 5
1+5 = 6
1+6 = 7
1+7 = 8
1+8 = 9
1+9 = 10
1+10 = 11
     '''
1+90 = 91
1+91 = 92
1+92 = 93
1+93 = 94
1+94 = 95
1+95 = 96
1+96 = 97
1+97 = 98
1+98 = 99
1+99 = 100
num = 1
result = 100
```

하지만 num과 result변수는 for문의 초기화식에 선언되지 않았고 실행되기전에 선언한 global변수이기 때문에 for문의 { }실행 블록과 상관 없이 실행할 수 있다.


```java
public class Ex4 {

    public static void main(String[] args) {
        int num = 1;
        int result = 0;
        int i;
        for(i = 0; i <= 99; i++) {
            result = num + i;
            System.out.println(num + "+" + i + " = " + result);
        }
        System.out.println(num + "+" + i + " = " + (num + i));
    }
}
```

```java
1+1 = 2
1+2 = 3
1+3 = 4
1+4 = 5
1+5 = 6
1+6 = 7
1+7 = 8
1+8 = 9
1+9 = 10
1+10 = 11

     '''
1+90 = 91
1+91 = 92
1+92 = 93
1+93 = 94
1+94 = 95
1+95 = 96
1+96 = 97
1+97 = 98
1+98 = 99
1+99 = 100
1+100 = 101
```

이렇게 for문의 초기화 식에서 i라는 변수를 선언하는 것이 아닌 for문 이전에 i라는 변수를 선언하면 global 변수로 인식되고 for문에서 진행되기 전 변수를 선언하였기 때문에 초기화만 for문에서 진행하고
num, result와 마찬가지로 실행 블록 { }과 상관 없이 사용할 수 있다. 

for문의 실행블록 내부에 있는 i의 마지막 값은 99인데 외부에 있는 i의 값은 100인 이유는 for문의 조건식에서 i가 99보다 작거나 같을 때 까지 반복하는 것이니 i가 100이 되어야 조건식에서 검사할 시 false가 나와 for문을 빠져나와 외부 실행문을 수행 하기 때문에 i는 100이 되는 것이고 실행 내부에 있는 i는 선언된 for문이 99까지 표현하고 100이 되면 실행 부분을 실행하지 않고 다음 실행문을 수행 하기 때문에 실행 내부에서 마지막으로 출력되는 i는 99를 넘어 설 수 없다.


for문은 for문 내부에 중첩으로 사용할 수 있으며 외부에 선언된 for문이 1번 반복될 때 마다 내부에 선언된 for문이 지정햇수 만큼 반복하고 내부 for문이 지정한 햇수 만큼 반복하였으면 외부 for문의 다음 반복이 실행되며 이것을 외부에 있는 for문이 지정한 햇수 만큼 반복한다.


```java
public class Ex5 {

    public static void main(String[] args) {
        for(int i = 1; i<=9; i++) {
                System.out.println(i+"단");
            for(int j = 1; j<=9; j++) {
                System.out.println(i + "x" + j + "=" + (i * j));
            }
        }
    }
}
```

```java
1단
1x1=1
1x2=2
1x3=3
1x4=4
1x5=5
1x6=6
1x7=7
1x8=8
1x9=9

'''
9단
9x1=9
9x2=18
9x3=27
9x4=36
9x5=45
9x6=54
9x7=63
9x8=72
9x9=81
```

외부 for문인 i가 1일 때 내부 for문이 1~9까지 반복한 다음 외부 for문의 i가 증감하여 2가 되며 내부 for문이 다시 1~9까지 반복하는 것을 i가 9가 될 때 까지 반복한다.


