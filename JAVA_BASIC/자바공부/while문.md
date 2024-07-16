for문 외에 다른 while반복문도 존재하는데 상황에 따라서 다르게 사용한다 for문은 반복 횟수가 비교적 명확한 경우에 사용되고 while문은 특정 조건이 충족될 때 까지 반복하는 상황에서 유용하다.
for문과 마찬가지로 while문도 조건문이 존재하며 ture일경우 반복하고 false일 경우 반복을 중단한다. 다른점은 for문은 초기화식을 포함할 수 있는 반면 while문은 초기화식이 어떤 경우에도 while문 밖에서 
이루어 져야 하고 while문의 조건식에는 연산한 boolena값이 아닌 boolean타입을 선언할 수 있으며 이럴 경우 무한 루프를 발생시킨다.

```java
public class Ex1 {

    public static void main(String[] args) {
        
        int sum = 0;
        int i = 1;
        
        while(i <= 10) {
            System.out.println(i);
            sum += i;
            i++;
        }
        System.out.println("1~"+(i-1)+"의 합 = " + sum); // i가 11이 되어야 반복문이 끝나니 while문이 끝난 i는 11이 됨으로 10을 표현하기 위해서 i - 1를 해주었다.
    }
}
```

```java
1
2
3
4
5
6
7
8
9
10
1~10의 합 = 55
```

초기화 식을 while문 외부에서 선언해주고 while문을 사용하여 조건식의 i가 10보다 작거나 같을 때 까지 반복하고 1번 반복할 때 i를 출력하고 합을 구하기 위해서 i를 sum에 더하여 누적 저장하고 i를 증감시켜
1~10까지 즉 10번 반복할 수 있게 한다. 

i가 11이 되어야 반복문이 끝나니 while문이 끝난 i는 11이 됨으로 10을 표현하기 위해서 i - 1를 해주었다.

```java
public class Ex2 {

    public static void main(String[] args) {
        
        boolean loof = true;
        int i = 1;
        int j;
        int multiply = 0;
        
        while(loof) {
            for(j = 1; j <= 9; j++) {
                multiply = i * j;
                System.out.println(i + "x" + j +" = "+multiply);
            }
            i++;
        }
    }
}
```

```java
1 x 1 = 1 
1 x 2 = 2 
1 x 3 = 3 
1 x 4 = 4 
1 x 5 = 5 
1 x 6 = 6 
1 x 7 = 7 
1 x 8 = 8 
1 x 9 = 9 

'''

394623x1 = 394623
394623x2 = 789246
394623x3 = 1183869
394623x4 = 1578492
394623x5 = 1973115
394623x6 = 2367738
394623x7 = 2762361
394623x8 = 3156984
394623x9 = 3551607
```

while문의 조건식에 boolean타입의 true를 선언한다면 끝나는 조건이 없기 때문에 무한 루프에 빠지게 되어 프로그램이 종료되지 못한다.

```java
public class Ex3 {

    public static void main(String[] args) {
        
        boolean loof = true;
        int i = 1;
        int j;
        int multiply = 0;
        
        while(loof) {
            System.out.println(i+"단");
            
            for(j = 1; j <= 9; j++) {
                multiply = i * j;
                System.out.println(i + "x" + j +" = "+multiply);	
            }
            
            System.out.println();
            
            if(i == 9) {
                break;
            }
            i++;
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

~~~

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

무한루프가 되는 경우에는 while문 내에 break제어문을 사용하여 무한 루프인 while문을 빠져 나올 수 있으며 보통 if 조건문과 사용된다. break문은 for, while, do while. switch문에서도 사용되기 때문에 반복문, 
조건문이 여러 번 사용되는 코드일 경우 어떤 반복문, 조건문 에서 break문을 사용하여 중지시킬 것인지 설정을 주의 하여야한다.
i++ 증감식은 j가 9까지 반복한다음 증감 시켜야 1단 에서 2단 구구단으로 넘어 갈 수있어 for문이 끝난 시점에 i를 증감시켜야 하며 i가 9미만 일 때는 break문이 실행하지 않고 i를 9까지 증감시키게 되지만 i가 9면 break문을 통해서 i가 9일 때 반복문을 종료하게 됨으로 9단 까지 표현할 수 있게 된다.


```java
public class Ex4 {

    public static void main(String[] args) {
        for(int i = 1; i<=10; i++) {
            if(i % 2 != 0) {
                continue;
            }
            System.out.println(i);
            
        }
    }
}
```

```java
2
4
6
8
10
```

반복문과 같이 사용되는 기타 제어문인 continue문은 for, while, do while문에서만 사용할 수 있고 주로 if문과 사용되며 해당 루프의 나머지 부분을 건너 뛰고 다음 조건식의 판단으로 넘어가게 해준다.  for문에서 continue를 사용하게 되면 나머지 부분을 건너 뛰고  for문의 증감식으로 가서 다시 반복문을 수행하고 while,  do while문은 나머지 부분을 건너 뛰고 조건식으로 가서 반복문을 수행한다.  

루프의 나머지 부분은 for 반복문 외부에 있는 System.out.println(i);을 말하며 Ex6의 코드는 i를 10보다 작거나 같을 때 까지 반복하게 되는데 조건문을 사용해서 i 를 2로 나누고 나머지 값이 0이 아니면 즉 짝수가 
아니고 홀수면 continue문을 실행 해서 기존의 실행 흐름인 System.out.println(i); 출력하지않고 실행 흐름을 증감식으로 가져가 홀수가 나오게 되는 경우를 예외 처리 하게 되고 짝수일 경우 코드 실행 흐름에 따라 
반복문 밖에 있는 코드를 출력하게 된다.

break와 비교하자면 break는 실행 흐름을 제어하여 반복문을 종료하기 위한 목적으로 사용되고 continue는 반복문 내에서 실행 흐름을 제어하여 특정 조건에 대한 예외 처리를 할 때 사용된다.  

```java
public class Ex5 {

    public static void main(String[] args) {
        System.out.println("프로그램을 종료하려면 q를 눌러주세요.");
        System.out.println();
        
        String inputStrim;
        Scanner sc = new Scanner(System.in);
        
        do {
            System.out.print("메시지를 입력하세요 : ");
            inputStrim = sc.nextLine();
            System.out.println("->"+inputStrim);
            System.out.println();
            
        }while( ! inputStrim.equals("q") );
        
        System.out.println("프로그램을 종료합니다.");
    }
}
```
```java
프로그램을 종료하려면 q를 눌러주세요.

메시지를 입력하세요 : 안녕하세요
->안녕하세요

메시지를 입력하세요 : 현재 시간은 05 : 30 입니다.
->현재 시간은 05 : 30 입니다.

메시지를 입력하세요 : q
->q

프로그램을 종료합니다.
```

while문의 다른 형태로 do while문이 존재 하는데 조건식에 의해 반복 실행한다는 점에서 while문과 동일하지만 다른점은 while문 같은 경우는 while문을 선언하고 조건식을 검사하여 실행 블록을 실행 시키지만
do while문은 do를 사용하여 실행 블록 내부를 먼저 실행 시키고 while문의 조건식 실행 결과가 true면 do의 실행 블록을 다시 반복하여 실행하고 false일 경우 반복문을 종료한다.

while문과 동일하게 변수를 사용할 초기화식을 반복문 외부에서 선언하고 메시지를 입력할 데이터를 읽어 오기 위해서 Scanner를 선언해준다. do{ }실행 블록을 선언하고 { }내부에서는 데이터를 읽어 오기 위한 문자열을 출력하고 사용자가 입력한 데이터를 Scanner를 통해서 읽어와 inputStrim에 저장하고 inputStrim에 저장된 입력 데이터를 다시 출력하기 까지 반복하고 while문의 조건식은 프로그램 종료를 위한 false값이 나와야 하기에 입력데이터q와 문자열 q를 비교하면 true가 나오게 되지만 !(not)을 사용하여 false가 됨으로 입력데이터가 q면 반복문을 종료하게된다.



