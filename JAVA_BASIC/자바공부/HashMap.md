HashtaMap과 Hashtable의 관계는 Vector와 ArryList의 관계와 같고 Hashtable보다는 새로운 버전인 HashMap을 사용하는 것이 좋다.

HashMap은 Map을 구현했으므로 앞에서 살펴본 Map의 특징, 키(key)와 값(value)을 묶어서 하나의 데이터로 저장한다는 특징을 가지고 있으며 해싱(hashing)을 사용하기 때문에 많은 양의 데이터를 검색하는데 있어서 뛰어난 성능을 보인다.

```java
public class HashMap extends AbstractMap implement Map, Cloneable, Serializable {
	
	transient Entey[] table;
	// 관련된 코드 '''
	
	static class Entry implements Map.Entry {
		final Object key;
		Object value;
		// 관련된 코드 '''
	}
}
```

HashMap은 Entry라는 내부 클래스를 정의하고, 다시 Entry타입의 배열을 선언하고 있으며 키와 값은 별개의 값이 아니라 서로 관련된 값이기 때문에 각각의 배열로 선언하기 보다는 하나의 클래스로 정의해서 하나의 배열로 다루는 것이 데이터의 무결성 적인 측면에서 더 바람직하기 때문이다.

비 객체 지향적인 코드
```java
Object[] key;
Object[] value;
```

객체 지향적인 코드
```java
Entry[] table;
class Entry{
	Object key;
	Object value;
}
```

HashMap은 키와 값을 각각 Object타입으로 (Object, Object) 형태로 저장하기 때문에 어떠한 객체도 저장할 수 있지만 키는 주로 String을 대문자 또는 소문자로 통일해서 사용한다.

키는 저장된 값을 찾는데 사용되기 때문에 컬렉션 내에서 유일(unique)해야 하기 때문에 중복을 허용하지 않는다. 즉, HashMap에 저장된 데이터를 하나의 키로 검색했을 때 결과 값이 하나 이여야 한다. 키에 대해 여러 검색 결과 값을 얻는다면 원하는 값이 어떤 것인지 알 수 없기 때문이다.

```java
package ch07;

import java.util.*;

public class HashMapEx1 {

	public static void main(String[] args) {
		HashMap hashmap = new HashMap();
		hashmap.put("myId", "1234");
		hashmap.put("asdf", "1111");
		hashmap.put("asdf", "1234");
		
		Scanner scanner = new Scanner(System.in);
		
		while(true) {
			System.out.println("id와 password를 입력하세요.");
			System.out.print("id : ");
			String id = scanner.nextLine().trim();
			
			System.out.print("password : ");
			String password = scanner.nextLine().trim();
			System.out.println();
			
			if(!hashmap.containsKey(id)) {
				System.out.println("입려하신 id는 존재하지 않습니다." + " 다시 입력해주세요.");
				continue;
			}
			
			if(!hashmap.get(id).equals(password)) {
				System.out.println("입려하신 비밀번호가 일치하지 않습니다." + " 다시 입력해주세요.");
			} else {
				System.out.println("id와 비밀번호가 일치합니다.");
				break;
			}
		}
	}
}

```

```java
id와 password를 입력해주세요.
id :asdf
password :1111

입력하신 비밀번호가 일치하지 않습니다. 다시 입력해주세요.
id와 password를 입력해주세요.
id :asdf
password :1234

id와 비밀번호가 일치합니다.
```

위의 코드에서 HashMap을 생성하고 데이터를 저장하는 부분인데 이 코드가 실행되고 나면 HashMap에는 아래와 같은 형태로 데이터가 저장된다.

|        |         |
| ------ | ------- |
| 키(key) | 값(value |
| myId   | 1234    |
| asdf   | 1234    |

3개의 데이터 쌍을 저장했지만 실제로는 2개 밖에 저장되지 않은 이유는 중복된 키가 있기 때문이다. 세 번째로 저장한 데이터의 키인 ‘asdf’는 이미 존재하기 때문에 새로 추가되는 대신 기존의 값을 덮어쓴다. 하여 키 ‘asdf’에 연결된 값은 ‘1234’가 된다. 즉, Map은 값은 중복을 허용하지만 키는 중복을 허용하지 않기 때문에 저장하려는 두 데이터 중에서 어느 쪽을 키로 할 것 인지를 잘 결정해야 한다.

```java
package ch07;

import java.util.*;

public class HashMapEx2 {

	public static void main(String[] args) {
		HashMap hashMap = new HashMap();
		hashMap.put("김자바", new Integer(100));
		hashMap.put("이자바", new Integer(100));
		hashMap.put("강자바", new Integer(80));
		hashMap.put("안자바", new Integer(90));
		
		Set set = hashMap.entrySet();
		Iterator iterator = set.iterator();
		
		while(iterator.hasNext()) {
			Map.Entry entry = (Map.Entry)iterator.next();
			System.out.println("이름 : " + entry.getKey() + ", 점수 : " + entry.getValue());
		}
		
		set = hashMap.keySet();
		System.out.println("참가자 명단 : " + set);
		
		Collection values = hashMap.values();
		iterator = values.iterator();
		
		int total = 0;
		
		while(iterator.hasNext()) {
			Integer i = (Integer)iterator.next();
			total += i.intValue();
		}
		
		System.out.println("총점 : " + total);
		System.out.println("평균 : " + (float)total / set.size());
		System.out.println("최고점수 : " + Collections.max(values));
		System.out.println("최저점수 : " + Collections.min(values));
	}
}
```

```java
이름 : 안자바, 점수 : 90
이름 : 김자바, 점수 : 100
이름 : 강자바, 점수 : 80
이름 : 이자바, 점수 : 100
참가자 명단 : [안자바, 김자바, 강자바, 이자바]
총점 : 370
평균 : 92.5
최고점수 : 100
최저점수 : 80
```

entrySet( )을 이용해서 키와 값을 함께 읽어 올 수도 있고 keySet( )이나 values( )를 이용해서 키와 값을 따로 읽어 올 수 있다.


