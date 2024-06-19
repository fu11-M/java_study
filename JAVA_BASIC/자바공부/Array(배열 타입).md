변수는 하나의 값만 저장할 수 있어 여러개의 값을 다룰 때 값을 하나씩 저장하여야 하는 방식을 사용해야 하기에 코드가 길어져 효율적이지 못한 프로그래밍이 되지만 Array타입은 연속된 공간에 값을 나열 시키고 
각 값에 index를 부여해 놓은 자료구조 이기에 index를 통해서 값을 변경하고 저장할 수 있고 많은 양의 값을 다루기 위한 상황일 때 유리하다. 

Array타입은 타입[ ] 변수 = {값}; 와 같은 형식으로 사용되며 특징으로는 {값} 부분에 나열된 항목은 선언한 타입과 같은 타입의 값만 관리하고 생성과 동시에 Array의 길이가 결정되기에 길이를 늘리거나 줄일 수 없다.

{ }에 나열된 값들을 힙영역에 배열의 항목으로 가져와 객체 형태로 나열하고 힙영역에 생성된 배열 객체의 주소를 변수에 저장한다. (참조 타입)

값의 목록을 미리 선언하지 않고 배열의 길이를 설정하고 후에 값을 저장하고 싶을 경우에는 new연산자를 사용하여 Array객체를 생성하고 index를 통해서 값을 저장할 수 있다.
겂의 목록을 설정하지 않았을 경우에는 배열의 모든 값이 설정한 타입의 기본값으로 설정된다.

배열의 길이를 읽을 때는 String타입과 마찬가지로 해당 Array 변수를 선언하여 .lenth()를 사용함으로 변수의 값인 Array 객체의 주소를 찾아가 객체의 길이를 반환한다.
```java
package ch06.sec01ReferenceTypeArray;

import java.util.Arrays;

public class Ex1 {

    public static void main(String[] args) {
        int[] intArray1 = {10, 20 ,30};
        
        int[] intArray2 = new int[3];
        
        int[] intArray3;
        intArray3 = new int[] {70, 80, 90};
        
        //intArray1
        System.out.println(intArray1[0]);
        System.out.println(intArray1[1]);
        System.out.println(intArray1[2]);
        
        System.out.println(Arrays.toString(intArray1));
        System.out.println("intArray1 메모리주소 = "+intArray1);
        System.out.println();
        
        //intArray2
        intArray2[0] = 40;
        intArray2[1] = 50;
        intArray2[2] = 60;
        
        for(int Array2Index = 0; Array2Index <=2; Array2Index++) {
            System.out.println(intArray2[Array2Index]);
        }
        
        System.out.println(Arrays.toString(intArray2));
        System.out.println("intArray2 메모리주소 = "+intArray2);
        System.out.println();
        
        //intArray3
        for(int Array3Index = 0; Array3Index < intArray3.length; Array3Index++) {
            System.out.println(intArray3[Array3Index]);
        }
        
        System.out.println(Arrays.toString(intArray3));
        System.out.println("intArray3 메모리주소 = "+intArray3);
        System.out.println();
    
    }
}
```
```java
10
20
30
[10, 20, 30]
intArray1 메모리주소 = [I@626b2d4a

40
50
60
[40, 50, 60]
intArray2 메모리주소 = [I@5e91993f

70
80
90
[70, 80, 90]

intArray3 메모리주소 = [I@1c4af82c
```
intArray1은 int타입의 숫자 배열 10, 20, 30을 저장하였고 배열은 각 항목에 index를 부여하기 때문에 숫자 배열을 표현하려면 index를 표현하여야 값이 나오게 되고 println으로 변수만 출력하게 되면 해당 변수의 
객체가 저장되어있는 힙영역의 주소만 나오게 된다. 배열을 표현하는 다른 방법으로는 저장된 배열을 문자열로 출력해주는 Array.toString(배열 변수) 메소드를 사용하여 intArray1에 저장되어 있는 배열을 표현
할 수 있는데 이 메소드는 배열의 요소 즉 index를 순회하면서 각 요소를 쉼표로 구분하여 문자열로 변환한다.

intArray2같은 경우는 new연산자를 사용하여 직접 배열 객체를 생성하고 배열의 길이를 선언하였고 배열의 값은 index를 통해서 저장한 방법이다. 저장된 배열들을 Array1의 예시와 다르게 for문을 사용하여
출력하였는데 Array2의 값은 index [0] = 40, [1] = 50,  [2] = 60 으로 선언하였으니 Array2의 index에 부여할 for문의 초기화 변수를 0으로 선언하고 index는 0, 1, 2까지 생성되어 있기 때문에 조건식에서는 2보다
작거나 같을 때 까지 즉 0이 2가 될 때 까지 반복함으로 Array2의 index를 0 ~ 2 까지 표현한다. 

intArray3같은 경우는 intArray2와 전반적으로 같지만 조건식에서 intArray3의 길이를 사용하기 위해 lenth를 사용하였고 사용한 이유는 intArray3의 길이는 70, 80, 90 3개의 길의가 정해져 있고 길이 가 3일 경우
index는 0, 1, 2인 경우 밖에 없기 때문에 조건식에서 intAarray3.lenth보다 작을 때 까지 반복한다면 intArray3의 index가 2가 될 때 까지 반복한다는 뜻이됨으로 이런 초기화식과 조건식이 배열과 잘어루어지기 때문에
많은 경우 for문과 배열을 사용한다.


배열은 여러 개를 선언하여 중첩으로 사용할 수 있는데 이것을 다차원 배열이라고 한다. 배열의 요소를 또 다른 배열로 포함하는 구조이다.
```java
package ch06.sec01ReferenceTypeArray;

import java.util.Arrays;

public class Ex2 {

    public static void main(String[] args) {
    int[][] intArray1 = {
            {10, 20, 30},
            {40, 50, 60}
    };
    
    System.out.println("intArray1 배열 변수의 주소 = " + intArray1);
    System.out.println("intArray1의 [0],intArray1의 [1]의 주소 = " + Arrays.toString(intArray1));
    System.out.println("intArray1의 [0] 줏 = " + Arrays.toString(intArray1[0]));
    System.out.println("intArray1의 [1] 값 = " + Arrays.toString(intArray1[1]));
    System.out.println();
    
    System.out.println("intArray1[0][0] = "+intArray1[0][0]);
    System.out.println("intArray1[0][1] = "+intArray1[0][1]);
    System.out.println("intArray1[0][2] = "+intArray1[0][2]);
    System.out.println("intArray1[1][0] = "+intArray1[1][0]);
    System.out.println("intArray1[1][1] = "+intArray1[1][1]);
    System.out.println("intArray1[1][2] = "+intArray1[1][2]);
    System.out.println();
    
    for(int i = 0; i<intArray1[0].length; i++) {
        System.out.println("intArray1[0][" + i + "] = "+intArray1[0][i]);
    }
    
    System.out.println();
    
    for(int i = 0; i<intArray1[1].length; i++) {
        System.out.println("intArray1[1][" + i + "] = "+intArray1[1][i]); 
    }
    
    System.out.println();
    
    for(int i = 0; i<intArray1.length; i++) {
        for(int j = 0; j<intArray1[i].length; j++) {
            System.out.println("intArray1[" + i + "]["+ j +"] = "+intArray1[i][j]);
        }
    }
    }
    }
```
```java
intArray1 배열 변수의 주소 = [[I@626b2d4a
intArray1의 [0],intArray1의 [1]의 주소 = [[I@5e91993f, [I@1c4af82c]
intArray1의 [0] 값 = [10, 20, 30]
intArray1의 [1] 값 = [40, 50, 60]

intArray1[0][0] = 10
intArray1[0][1] = 20
intArray1[0][2] = 30
intArray1[1][0] = 40
intArray1[1][1] = 50
intArray1[1][2] = 60

intArray1[0][0] = 10
intArray1[0][1] = 20
intArray1[0][2] = 30

intArray1[1][0] = 40
intArray1[1][1] = 50
intArray1[1][2] = 60

intArray1[0][0] = 10
intArray1[0][1] = 20
intArray1[0][2] = 30
intArray1[1][0] = 40
intArray1[1][1] = 50
intArray1[1][2] = 60
```

intAraay1을 두 개의 배열로 선언하였는데 이것은 2차원의 다차원 배열을 표현 한 것이다. 2차원 배열은 중괄호 안의 중괄호로 표현되지만 1차원 배열과 다르게 intArray1의 1차원 index는 값을 표현하지 않고 1차원
index값의 위치를 표현하는데 1차원 index[0]은 첫 번째 중괄호에 선언된 10, 20, 30이 저장되어 있는 배열의 주소가 저장되어 있고 index[1]은 두 번째 중괄호에 선언된 40, 50, 60이 저장되어 있는 배열의 주소가 저장되어 있기 때문에 10, 20, 30의 값은 intArray1[0][0~2] 의 값이 되고 40, 50, 60은 intArray[1][0~2] 의 값이 되는 것이다 즉 배열이 배열을 포함하고 있는 구조이다.

1차원 배열에서 Array.toString(배열변수)를 사용하면 index의 값들이 모두 출력되었으나 다차원 배열은 1차원 index의 값이 2차원 index의 주소를 가지고 있기 때문에 intArray1[0], intArray[1]의 주소 값을 표현하게
되고 Array.toString메소드를 사용하여 다차원 배열에 저장된 값을 표현하려면 배열변수에 1차원 배열의 index와 같이 표현해주면 된다.

배열을 표현할 때 용이한 for문을 사용하여 각각 1차원 배열에 포함되어 있는 2차원 배열을 표현하였고 중첩 for문을 사용하여 1차원 배열 다차원 배열을 연달아 표현할 수 있다.
먼저 intArray1의 전체 배열의 길이인 2를 조건식에 사용하여 2번 반복한다. 길이가 2인 이유는 1차원 배열의 index값에 2차원 배열의 index값이 포함되어 있는 것이니 길이 자체가 늘어나지는 않은 것이다.
intArray1.lenth가 2기 때문에 i가 intArray의 길이보다 보다 작을 때 까지 즉 i가 1이 될 때까지 반복하는 것이므로 1차원 index[0], index[1]를 표현할 수 있게 된다. 

다음 for문의 조건식으로는 intArray[i].lenth를 사용하는데 첫 번째 for문의 초기화식이 0이기 때문에 intArray1[0]일 때의 길이 10, 20, 30 즉 3이기 때문에 3보다 작을 때 까지 반복을 한다면 j가 2가 될 때 까지 반복하여 2차원 배열의 index를 [0~2]까지 표현 할 수 있게 되는 것이고 그 후 조건식이 false가 되어 다시 첫 번째 for문으로 돌아가 i를 증감시켜 1이 되고 두 번째 for문으로 넘어 간 후 j는 0으로 초기화 되고 intArray[i].lenth의 조건식에서 i는 1이 되었기 때문에 intArray1[1]의 값인 40, 50, 60 즉 3이 되어 j가 2가 될 때 까지 반복하니 intArray[i][j]는 intArray1[0][0~2], intArray1[1][0~2]를 표현할 수 있게 되는 것이다. 

int타입과 같은 기본타입을 배열로 생성 했을 때는 배열에 각각 값을 저장하지만 String, Class, interface와 같은 참조타입을 배열을 생성 했을 때는 배열에 각각 참조타입 객체의 주소를 저장한다.

```java
package ch06;

import java.util.Arrays;

public class IntArray {

    public static void main(String[] args) {
        int[] intArray = {10, 20, 30};
        
        System.out.println("int 배열 변수 intArray의 값 = "+intArray);
        System.out.println("intArray[0] index의 값 = "+intArray[0]);
        System.out.println("intArray[1] index의 값 = "+intArray[1]);
        System.out.println("intArray[2] index의 값 = "+intArray[2]);
        
        System.out.println(Arrays.toString(intArray));
        
    }
}
```
```java
int 배열 변수 intArray의 값 = [I@626b2d4a
intArray[0] index의 값 = 10
intArray[1] index의 값 = 20
intArray[2] index의 값 = 30
[10, 20, 30]
```
int 타입의 1차원 배열을 생성하고 index( [0~2] )의 값을 10, 20, 30을 저장하고 System.out.print메소드를 사용하여 intArray변수의 값을 출력하면 heap영역의 int배열이 있는 주소가 저장되어 있는 것을 알 수 있고
intArray[0]~[2]를 출력하면 int는 기본타입이니 int배열의 각 항목에는 10, 20, 30이 저장되어 있다는 것을 알 수 있다.

```java
package ch06;

import java.util.Arrays;

public class StriArray {

    public static void main(String[] args) {
        String[] StrArray = {"AA", "BB", "CC"};
        
        System.out.println("String 배열 변수 StrArray의 값 = "+StrArray);
        System.out.println("StrArray[0] index의 값 = "+StrArray[0]);
        System.out.println("StrArray[1] index의 값 = "+StrArray[1]);
        System.out.println("StrArray[2] index의 값 = "+StrArray[2]);
        
        System.out.println(Arrays.toString(StrArray));
        
    }

}
```

```java
String 배열 변수 StrArray의 값 = [Ljava.lang.String;@626b2d4a
StrArray[0] index의 값 = AA
StrArray[1] index의 값 = BB
StrArray[2] index의 값 = CC
[AA, BB, CC]
```

StrArray[0]~[2] index의 값에는 String객체의 주소가 저장되어야 하는데 int타입처럼 String객체의 값 자체를 표현한다. 이것은 Java에서 모든 Class의 부모인 Object Class에서 객체의 값을 문자열로 표현하는
 toString( ) 메소드가 존재하는데 String Class가 Object Class에서 toString( )메소드를 상속 받아 재정의 하였기 때문에 실제로 heap영역의 String배열 index값은 String 객체의 주소가 저장되어 있지만 System.out.print( )메소드를 사용하여  String배열에서의 index값을 출력하면 String객체의  주소가 아니라 String객체의 값 자체인 AA, BB, CC 값이 나오게 되는 것이다.

 ```java
 package ch06;
 
 import java.util.Arrays;
 
 public class IntMultiArray {
 
    public static void main(String[] args) {
        int[][] intStr1 = {
                {10, 20, 30},
                {40, 50, 60}
        };
        
        System.out.println(intStr1);
        System.out.println(intStr1[0]);
        System.out.println(intStr1[1]);
        System.out.println(Arrays.toString(intStr1));
        System.out.println();
        
        System.out.println(intStr1[0][0]);
        System.out.println(intStr1[0][1]);
        System.out.println(intStr1[0][2]);
        System.out.println(Arrays.toString(intStr1[0]));
        System.out.println();
        
        System.out.println(intStr1[1][0]);
        System.out.println(intStr1[1][1]);
        System.out.println(intStr1[1][2]);
        System.out.println(Arrays.toString(intStr1[1]));
    }
 }
 ```

 ```java
 int 다차원 배열 변수 intMultiArray의 값 = [[I@626b2d4a
 intMultiArray[0] index의 값 = [I@5e91993f
 intMultiArray[1] index의 값 = [I@1c4af82c
 [[I@5e91993f, [I@1c4af82c]
 
 intMultiArray[0][0] index의 값 = 10
 intMultiArray[0][1] index의 값 = 20
 intMultiArray[0][2] index의 값 = 30
 [10, 20, 30]
 
 intMultiArray[1][0] index의 값 = 40
 intMultiArray[1][1] index의 값 = 50
 intMultiArray[1][2] index의 값 = 60
 [40, 50, 60]
 ```

 ```java
 package ch06;
 
 import java.util.Arrays;
 
 public class Ex6StrMultiArray {
 
    public static void main(String[] args) {
        String[][] strMultiArray = {
                {"AA", "BB", "CC"},
                {"DD", "EE", "FF"}
        };
        
        System.out.println("str 다차원 배열 변수 strMultiArray의 값 = " + strMultiArray);
        System.out.println("strMultiArray[0] index의 값 = " + strMultiArray[0]);
        System.out.println("strMultiArray[0] index의 값 = " + strMultiArray[1]);
        System.out.println(Arrays.toString(strMultiArray));
        System.out.println();
        
        System.out.println("strMultiArray[0][0] index의 값 = " + strMultiArray[0][0]);
        System.out.println("strMultiArray[0][1] index의 값 = " + strMultiArray[0][1]);
        System.out.println("strMultiArray[0][2] index의 값 = " + strMultiArray[0][2]);
        System.out.println(Arrays.toString(strMultiArray[0]));
        System.out.println();
        
        System.out.println("strMultiArray[0][0] index의 값 = " + strMultiArray[1][0]);
        System.out.println("strMultiArray[0][0] index의 값 = " + strMultiArray[1][1]);
        System.out.println("strMultiArray[0][0] index의 값 = " + strMultiArray[1][2]);
        System.out.println(Arrays.toString(strMultiArray[1]));
    }
 
 }
 ```
 ```java
 str 다차원 배열 변수 strMultiArray의 값 = [[Ljava.lang.String;@626b2d4a
 strMultiArray[0] index의 값 = [Ljava.lang.String;@5e91993f
 strMultiArray[0] index의 값 = [Ljava.lang.String;@1c4af82c
 [[Ljava.lang.String;@5e91993f, [Ljava.lang.String;@1c4af82c]
 
 strMultiArray[0][0] index의 값 = AA
 strMultiArray[0][1] index의 값 = BB
 strMultiArray[0][2] index의 값 = CC
 [AA, BB, CC]
 
 strMultiArray[0][0] index의 값 = DD
 strMultiArray[0][0] index의 값 = EE
 strMultiArray[0][0] index의 값 = FF
 [DD, EE, FF]
 ```

배열의 길이는 배열을 한 번 생성하면 길이를 변경할 수 없지만 길이가 더 긴 배열을 사용하려면 길이가 더 긴 배열을 생성하고 길이가 짧은 배열의 값들을 길이가 더 긴 배열에 저장하여야 하는데 이것을
배열 복사라고 한다. 길이가 더 긴 배열을 생성할 때 배열의 값이 초기화가 되어 있어야 하는데 이럴 경우 new연산자로 배열을 생성하여 배열을 초기화 시켜 짧은 배열의 항목들을 긴 배열의 항목으로 저장할 수 
있고 for문, SystemClass의 arraycopy()메소드, ArrayClass의 copyOf()메소를 사용하여 배열 복사를 간단하게 구현할 수 있다.

 SystemClass의 arraycopy()메소드는 메소드 안에 
(기존 배열, 기존 배열에서 복사 하는데 어디서 부터 복사할 것인지를 위한 시작 인덱스, 복사 배열, 복사 배열의 인덱스 중 어디부터 시작하여 저장할지를 위한 index, 복사 하고 싶은 index수)와 같이 사용되고

ArrayClass의 copyOf()메소드는 메소드 안에
(복사 배열, 복사 하고 싶은 index수)와 같이 사용된다.

```java
package ch06;

public class Ex7ArrayCopy {

    public static void main(String[] args) {
        int[] intArray = {1, 2, 3};
        
        int[] newArray = new int[5];
        
        newArray[0] = intArray[0];
        newArray[1] = intArray[1];
        newArray[2] = intArray[2];
        
        
        System.out.println("intArray[0] = " + intArray[0]);
        System.out.println("intArray[1] = " + intArray[1]);
        System.out.println("intArray[2] = " + intArray[2]);
        
        System.out.println();
        
        System.out.println("newArray[0] = " + newArray[0]);
        System.out.println("newArray[0] = " + newArray[1]);
        System.out.println("newArray[0] = " + newArray[2]);
        System.out.println("newArray[0] = " + newArray[3]);
        System.out.println("newArray[0] = " + newArray[4]);
        
        System.out.println();
        
        for(int i = 0; i<intArray.length; i++) {
            System.out.println("intArray["+ i +"] = " + intArray[i]);
            newArray[i] = intArray[i];
        }
        
        System.out.println();
        
        for(int i = 0; i<newArray.length; i++) {
            System.out.println("newArray["+ i +"] = " + newArray[i]);
        }
    
    }

}
```

```java
intArray[0] = 1
intArray[1] = 2
intArray[2] = 3

newArray[0] = 1
newArray[0] = 2
newArray[0] = 3
newArray[0] = 0
newArray[0] = 0

intArray[0] = 1
intArray[1] = 2
intArray[2] = 3

newArray[0] = 1
newArray[1] = 2
newArray[2] = 3
newArray[3] = 0
newArray[4] = 0
```

```java
package ch06;

import java.util.Arrays;

public class Ex8ArrayCopyMethod {

    public static void main(String[] args) {
        int[] intArray = {1, 2, 3};
        
        int[] newArray = new int[5];
        
        System.arraycopy(intArray, 0, newArray, 0, intArray.length);
        
        for(int i = 0; i<newArray.length; i++) {
            System.out.println("newArray["+ i +"] = " + newArray[i]);
        }
        
        System.out.println();
        
        String[] strArray = {"AA", "BB", "CC"};
        
        String[] newStrArray;
        
        newStrArray = Arrays.copyOf(strArray, 5);
        
        for(int i = 0; i<newStrArray.length; i++) {
            System.out.println("newStrArray["+ i +"] = " + newStrArray[i]);
        }
        
    }
}
```

```java
newArray[0] = 1
newArray[1] = 2
newArray[2] = 3
newArray[3] = 0
newArray[4] = 0

newStrArray[0] = AA
newStrArray[1] = BB
newStrArray[2] = CC
newStrArray[3] = null
newStrArray[4] = null
```

```java
package ch06;

import java.util.Arrays;

public class Ex9StringObject {

    public static void main(String[] args) {
        String[] strVar1 = {"AA","BB","CC"};
        String[] strVar2 = new String[5];
        
        strVar2 = Arrays.copyOf(strVar1, strVar1.length);
        
        System.out.println("strVar1 == strVar2 : " + (strVar1 == strVar2));
        System.out.println("strVar1[0] == strVar2[0] : " + (strVar1[0] == strVar2[0]));
        
    }

}
```
```java
strVar1 == strVar2 : false
strVar1[0] == strVar2[0] : true
```

StrVar1 배열 변수와 strVar2배열 변수의 주소를 비교해 보면 StrVar1의 값인 heap영역의 String배열 객체의 주소와 StrVar2의 값인 heap영역의 String배열 객체의 주소가 다르기 때문에 false가 나오게 되고
strVar1[0]와 strVar2[0]의 주소를 비교해 보면 strVar2는 strVar1의 배열을 복사하였기 때문에 문자열은 같은 리터럴이 사용되면 String 객체를 공유하기 때문에 strVar2의 String배열 [0]값이 StrVar1의 String 배열 
[0]값의 주소는 true가 나오게 된다.

( String[] strVar1 = {"AA","BB","CC"};를 선언 하였을 때 JVM메모리 내에서 Stack영역에는 strVar1이 저장되고 strVar1의 값은 heap영역에 있는 String타입의 배열 객체의 주소가 되며 String Pool이라는 영역에는
String객체가 저장되어 있다.
String타입의 배열 객체의 항목의 값 즉 index는 "AA"라는 String객체 "BB"라는 String객체 "CC"라는 String객체를 저장하는 공간인  String Pool이라는 공간의 주소가 된다. 하지만 srtVar1[0~2]의 값을 출력하면
주소가 아닌 "AA","BB","CC"가 나오게 되는데 이러한 이유는 Object Class의 toString() 메소드가 존재하는데 객체의 class이름과 hashcode를 문자열로 반환 하는 메소드이며 String Class가 Object Class를 상속받아 toString()를 재정의 하여 객체가 가지고 있는 실제 문자열 값을 반환하는 기능을한다. System.out.print() 출력 메소드로 srtVar1[0~2]의 값을 출력 할 때 String Class의 toString()메소드가 동작하여 String객체의 주소가 아닌 객체 자체의 문자열값이 출력되는 것이다.) (반환은 toString 출력은 System.out.print())



