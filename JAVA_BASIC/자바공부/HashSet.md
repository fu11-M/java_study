HashSet은 Set인터페이스를 구현한 가장 대표적인 컬렉션이며, Set인터페이스의 특징대로 HashSet은 중복된 요소를 저장하지 않는다.

HashSet에 새로운 요소를 추가할 때는 add메서드나 addAll메서드를 사용하는데, 만일 HashSet에 이미 저장되어 있는 요소와 중복된 요소를 추가하고자 한다면 이 메서드들은 false를 반환함으로써 중복된 요소이기 때문에 추가에 실패한다.

이러한 HashSet의 특징을 이용하면, 컬렉션 내의중복 요소들을 쉽게 제거할 수 있다.

ArrayList와 같이 List인터페이스를 구현한 컬렉션과 달리 HashSet은 저장 순서를 유지하지 않으므로 저장 순서를 유지하고자 한다면 LinkedHashSet을 사용해야한다.

### HashSet의 메서드

| 생성자 또는 메서드                                    | 설명                                              |
| --------------------------------------------- | ----------------------------------------------- |
| HashSet( )                                    | HashSet객체를 생성한다.                                |
| HashSet(Collection collection)                | 주어진 컬렉션을 포함하는 HashSet객체를 생성한다.                  |
| HashSet(int initalCapacity)                   | 주어진 값을 초기 용량으로 하는 HashSet객체를 생성한다.              |
| HashSet(int initalCapacity, flaot loadFactor) | 초기용량과 load factor를 지정하는 생성자                     |
| boolean add(Object object)                    | 새로운 객체를 저장한다.                                   |
| boolean addAll(Collection collection)         | 주어진 컬렉션에 저장된 모든 객체들을 추가한다.(합집합)                 |
| void clear( )                                 | 저장된 모든 객체를 삭제한다.                                |
| Object clone( )                               | HashSet을 복제해서 반환한다.                             |
| boolean contains(Object object)               | 지정된 객체를 폼하고 있는지 알려준다.                           |
| boolean containsAll(Collection collection)    | 주어진 컬렉션에 저장된 모든 객체들을 포함하고 있는지 알려준다.             |
| booelan isEmpty( )                            | HashSet이 비어있는지 알려준다.                            |
| Iterator iterator( )                          | Iterator를 반환한다.                                 |
| boolean remove(Object object)                 | 지정된 객체를 HashSet에서 삭제한다. (성공하면 true, 실패하면 false) |
| boolean removeAll(Collection collection)      | 주어진 컬렉션에 저장된 객체와 동일한 거만 남기고 삭제한다. (교집합)         |
| boolean retainAll(Collection collection)      | 주어진 컬렉션에 저장된 객체와 동일한 것만 남기고 삭제 한다.(교집합)         |
| int size( )                                   | 저장된 객체의 개수를 반환한다.                               |
| Object[ ] toArray( )                          | 저장된 객체들을 객체 배열의 형태로 반환한다.                       |
| Object[ ] toArray(Object[ ] a)                | 저장된 객체들을 주어진 객체 배열(a)에 담는다.                     |

### HashSetEx1
```java
package ch07;

import java.util.HashSet;
import java.util.Set;

public class HashSetEx1 {

	public static void main(String[] args) {
		Object[] objArray = {"1", new Integer(1), "2", "2", "3", "3", "4", "4", "4"};
		Set set = new HashSet();
		
		for(int i = 0; i < objArray.length; i++) {
			set.add(objArray[i]);
		}
		System.out.println(set);
	}
}
```

```java
[1, 1, 2, 3, 4]
```

Set인터페이스의 특징대로 HashSet은 중복된 값을 저장하지 않았다. add메서드는 객체를 추가할 때 HashSet에 이미 같은 객체가 있으면 중복으로 간주하고 저장하지 않는다.

1이 두 번 출력되었는데 하나는 String 인스턴스이고 다른 하나는 Integer인스턴스로 서로 다른 객체이므로 중복으로 간주하지 않는다.

Set을 구현한 컬렉션 클래스는 List를 구현한 컬렉션 클래스와 달리 순서를 유지하지 않기 때문에 저장한 순서와 다를 수 있다. 만일 중복을 제거하는 동시에 저장한 순서를 유지하고자 한다면 HashSet대신 Linked HashSet을 사용해야 한다.


### HashSetEx2
```java
package ch07;

import java.util.Collections;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.Set;
import java.util.List;

public class HashSetEx2 {

	public static void main(String[] args) {
		Set set = new HashSet();
		
		for(int i = 0; set.size() < 6; i++) {
			int num = (int) ((Math.random()*45) + 1);
			set.add(new Integer(num));
		}
		
		List linkedSet = new LinkedList(set);
		Collections.sort(linkedSet);
		System.out.println(linkedSet);
	}
}
```

```java
[7, 11, 17, 18, 24, 28]
```

번호 크기를 순서대로 정렬하기 위해서 Collections클래스의 sort( )를 사용했으며 이 메서드는 인자로 List인터페이스 타입을 필요로 하기 때문에 LinkedList클래스의 생성자 LinkedList(set)을 이용하여 HashSet에 저장된 객체들을 LinkedList에 담아서 처리하였다.

실행 결과의 정렬 기준은, 컬렉션에 저장된 객체가 Integer이기 때문에 Integer클래스에 정의된 기본 정렬이 사용되었다.

### HashSetEx3
```java
package ch07;

import java.util.HashSet;
import java.util.Iterator;
import java.util.LinkedHashSet;
import java.util.Set;

public class HashSetEx3 {

	public static void main(String[] args) {
		Set set = new HashSet();
		//Set set = new LinkedHashSet();
		
		int[][] board = new int[5][5];
		
		for(int i = 0; set.size() < 25; i++) {
			set.add((int)(Math.random() * 50) + 1 + "");
		}
		
		Iterator iterator = set.iterator();
		
		for(int i = 0; i < board.length; i++) {
			for(int j = 0; j < board[i].length; j++) {
				board[i][j] = Integer.parseInt((String) iterator.next());
				System.out.print((board[i][j] < 10 ? "  " : " ") + board[i][j]);
			}
			System.out.println();
		}
	}
}
```

```java
  7 24 30 10 12
 11 22 28  1 18
  4 44 32 45 35
 49 17 16  8 20
 26  2 37  5 25
```

HashSet은 저장된 순서를 보장하지 않고 자체적인 저장 방식에 따라 순서가 결정되기 때문에 이 부분을 고려하여 HashSet과 LinkedHashSet중 사용 결정을 내리면 된다.

