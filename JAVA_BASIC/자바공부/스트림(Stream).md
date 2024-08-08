<aside>
💡 스트림은 다양한 데이터 소스(컬렉션)를 표준화 된 방법으로 다루기 위한 것이며 데이터의 
연속적인 흐름을 나타낸다.

</aside>

기존의 컬렉션 프레임워크인 List, Set, Map등이 모두 사용 방법이 달라서 표준화를 하지 못했다. 
하지만 jdk 1.8부터 스트림을 통해 표준화를 달성했다.
하여 모든 데이터 소스는 스트림으로 만들 수 있으며 스트림으로 만든 다음에는 표현하는 방식은 
어떤 데이터 소스라도 동일해진다.

컬렉션이나 배열에 데이터를 담고 원하는 결과를 얻기 위해 for문과 Iterator를 이용해서 코드를 작성
해왔다. 그러나 이러한 방식으로 작성된 코드는 너무 길고 알아보기 어려우며 재 사용성도 떨어진다.

또 다른 문제는 데이터 소스마다 다른 방식으로 다뤄야 한다는 것이다. Collection이나 Iterator와 같은
인터페이스를 이용해서 컬렉션을 다루는 방식을 표준화 하기는 했지만, 각 컬렉션 클래스에는 같은 
기능의 메서드들이 중복 해서 정의되어 있다. 

예를 들어 List를 정렬할 때는 Collections.sort( )를 사용해야 하고, 배열을 정렬할 때는 Array.sort( )를
사용해야 한다.

이러한 문제점들을 해결하기 위해서 만든 것이 ‘스트림(Stream)’이다. 스트림은 데아터 소스를 추상화
하였고, 데이터를 다루는데 자주 사용되는 메서드들을 정의해 놓았다. 
데이터 소스를 추상화 하였다는 것은, 데이터 소스가 무엇이던 간에 같은 방식으로 다룰 수 있게 되었
다는 것과 코드의 재 사용성이 높아진다는 것을 의미한다.

스트림을 이용하면, 배열이나 컬렉션 뿐만 아니라 파일에 저장된 데이터도 모두 같은 방식으로 다룰 수 있다. 

예를 들어, 문자열 배열과 같은 내용의 문자열을 저장하는 List가 아래와 같이 있다고 가정하였을 때 

```java
String[] strArr = {"aaa", "ddd", "ccc"};
List<String> strList = Arrays.asList(strArr);
```

이 두 데이터 소스를 기반으로 하는 스트림은 다음과 같이 생성한다.

```java
Stream<String> strStream1 = strList.stream();
Stream<String> strStream2 = Arrays.stream(strArr);
```

이 두 스트림으로 데이터 소스의 데이터를 읽어서 정렬하고 화면에 출력하는 방법은 다음과 같다.
데이터 소스가 정렬되는 것은 아니라 것에 유의하자.

```java
strStream1.sorted().forEach(System.out::println);
strStream2.sorted().forEach(System.out::println);
```

<aside>
💡 System.out::println에서 :: 문법은  메서드 참조 문법으로 스트림의 각 요소가 System.out.println 메서드에 직접 전달한다는 표시이다.

</aside>

두 스트림의 데이터 소스는 서로 다르지만, 정렬하고 출력하는 방법은 완전히 동일하며 스트림을 사용
하지 않았다면 아래와 같이 코드를 작성하여야 한다.

```java
Arrays.sort(strArr);
Collection.sort(strList);

for(String str : strArr){
	System.out.println(str);
}

for(String str : strList){
	System.out.println(str);
}
```

비교해 보면 스트림을 사용한 코드가 간결하고 이해하기 쉬우며 재 사용성도 높다는 것을 알 수 있다.

## 스트림의 특징

### 스트림은 데이터 소스로부터 데이터를 읽을 뿐  변경하지 않는다.

스트림은 데이터 소스로부터 데이터를 읽기만 할 뿐, 데이터 소스를 변경하지 않는다는 차이가 있다.
필요하다면, 정렬된 결과를 컬렉션이나 배열에 담아서 반환할 수도 있다.

```java
List<Integer> list = Arrays.asList(3, 1, 5, 4, 2);
//List를 정렬해서 새로운 List에 저장
List<Integer> sortedList = list.stream().sorted().collect(Collectors.toList());
System.out.println(list); // 3, 1, 5, 4, 2
System.out.println(sortedList); // 1, 2, 3, 4, 5
System.out.println(list); // 3, 1, 5, 4, 2 //원본은 변경되지 않음
```

### 스트림은 일회용이다.

스트림은 Iterator처럼 일회용이다. Iterator로 컬렉션의 요소를 모두 읽고 나면 다시 사용할 수 없는 것
처럼, 스트림도 한번 사용하면 닫혀서 다시 사용할 수 없다. 만약 다시 사용하여야 한다면 새로운
스트림을 만들어야 한다.

```java
strStream1.sorted().forEach(System.out::println);
int numOfStr = strStream1.count(); // 에러 스트림이 이미 닫혀있다.
```

### 최종 연산 전까지 중간 연산이 수행되지 않는다. (지연된 연산)

각 메서드가 호출되었을 때 스트림 처리를 바로 하는 것이 아니라 스트림이 어떤 작업을 해야 할지
표시만 한 다음 필요할 때 나중에 연산한다. 아래의 코드를 보면 무한 스트림을 어떻게 중복 제거를
할 것 인지를 봤을 때 논리적으로 맞니 않는다 하지만 이것이 가능한 이유는 지연된 연산이 가능하기
때문이다.

```java
IntStream intStream = new random().ints(1, 46); // 1~45범위의 무한 스트림
intStream.distinct().limit(6).sorted() // 중간 연산
					.forEach(i -> System.out.print(i + ",")); // 최종 연산
```

### 스트림은 작업을 내부 반복으로 처리한다.

스트림을 이용한 직업이 간결할 수 있는 비결중의 하나가 바로 ‘내부 반복’ 이다. 
내부 반복이라는 것은 반복문을 메서드의 내부에 숨길 수 있다는 것을 의미한다. forEach( )는 스트림에 정의된 메서드 중에 하나로 매개변수에 대입된 람다식을 데이터 소스의 모든 요소에 적용한다.  

```java
for(String str : strList){
	System.out.println(str);
}
```

```java
stream.forEach(System.out::println);
```

## 병렬 스트림(멀티 쓰레드)

스트림의 작업을 병렬로 처리하는 것이 병렬 스트림이라 하며 
스트림으로 데이터를 다룰 때의 장점 중 하나가 병렬 처리가 쉽다는 것이다. 
병렬 스트림은 내부적으로 이 프레임워크를 이용해서 자동적으로 연산을 병렬로 수행한다.
병렬 스트림을 사용하기 위해서는 스트림에 parallel( )이라는 메서드를 호출해서 병렬로 연산을 수행
하면 된다. 
반대로 병렬로 처리되지 않게 하려면 sequential( )을 호출하면 된다.
모든 스트림은 기본적으로 병렬 스트림이 아니므로 sequential( )을 호출할 필요가 없기 때문에 이
메서드는 parallel( )을 호출한 것을 취소할 때만 사용한다.

병렬 스트림으로 처리했을 때의 장점은 순차 스트림으로 처리 했을 때 보다 결과를 더 빠르게 얻을 
수 있다.

```java
Stream<String> strStream = Stream.of("dd", "aaa", "CC", "cc", "b");
int sum = strStream.parallel() //병렬 스트림으로 전환(속성만 변경)
									.mapToInt(s -> s.length()).sum(); // 모든 문자열의 길이의 합
```

하지만 모든 상황에서 병렬 처리가 항상 더 빠른 결과를 얻게 해주는 것은 아니다.

## 스트림의 연산

스트림에 정의된 메서드 중에서 데이터 소스를 다루는 작업을 수행하는 것을 연산(operation) 이라고
한다. 

스트림이 제공하는 다양한 연산을 이용해서 복잡한 작업들을 간단히 처리할 수 있으며 중간 연산과 최종 연산으로 분류할 수 있다. 

- 중간 연산 : 연산 결과가 스트림인 연산. 스트림에 연속해서 중간 연산할 수 있음
- 최종 연산 : 연산 결과가 스트림이 아닌 연산. 스트림의 요소를 소모하므로 단 한번만 가능

```java
stream.distinct().limit(5).sorted().forEach(System.out::println)
 생성   중간연산   중간연산  중간연산          최종연산
```

모든 중간 연산의 결과는 스트림이지만, 연산 전의 스트림과 같은 것은 아니다. 위의 문장과 달리
모든 스트림은 연산을 나누어 쓰면 아래와 같다.  

### 각 연산의 반환 타입 및 스트림 변환 방법

```java
String[] strArr = { "dd", "aaa", "CC", "cc", "b" };
Stream<String> stream = Stream.of(strArr); // 문자열 배열이 소스인 스트림
Stream<String> filteredStream = stream.filter(); // 걸러내기 (중간 연산)
Stream<String> distinctedStream = stream.distinct(); // 중복제거 (중간 연산)
Stream<String> sortedStream = stream.sort(); // 정렬 (중간 연산)
Stream<String> limitedStream = stream.limit(5); // 스트림 자르기 (중간 연산)
int total = stream.count(); // 요소 개수 세기 (최종 연산)
```
