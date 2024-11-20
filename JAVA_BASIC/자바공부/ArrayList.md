ArrayList는 컬렉션 프레임워크에서 가장 많이 사용되는 컬렉션 클래스이며 List인터페이스를 구현하기 때문에 저장 순서가 유지되고

중복을 허용한다는 특징을 갖는다.

기존Vector를 개선한 것으로 Vector와 구현 원리가 기능적인 측면에서 동일하다.

Vector는 기존에 작성된 소스와의 호환성을 위해서 계속 남겨 두고 있을 뿐이기 때문에 가능하면 Vector보다는 ArrayList를 사용하는 것이 좋다.

ArrayList는 Object배열을 이용해서 데이터를 순차적으로 저장한다. 예를 들면, 첫 번째로 저장한 객체는 Object배열의 0번째 위치에 저장되고

그 다음 저장하는 객체는 1번째 위치에 저장된다. 이렇게 계속 배열에 순서대로 저장되며, 배열에 더 이상 저장할 공간이 없으면 보다 큰 새로운

배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열로 복사한 다음에 저장된다.

**ArrayList의 소스코드 일부**

```java
public class ArrayList extends AbstactList implements List, RandomAccess, Cloneable, java.io.Serializable{
	transient Object[] elementData;
}
```

ArrayList는 elementData라는 이름의 Object배열을 멤버 변수로 선언하고 있고 선언된 배열의 타입이 모든 객체의 최고 조상인 Object이기 때문에

모든 종류의 객체를 담을 수 있다.

ArrayList 메서드

|메소드|설명|
|---|---|
|ArrayList()|ArrayList생성|
|ArrayList(Collection c)|주어진 컬렉션이 저장된 ArrayList를 생성|
|ArrayList(int initialCapacity)|지정된 초기 용량을 갖는 ArrayList를 생성|
|boolean add(Object o)|ArrayList의 마지막에 객체를 추가, 성공하면 true|
|void add(int index, Object element)|지정된 위치(index)에 객체를 저장|
|boolean addAll(Collection c)|주어진 컬렉션의 모든 객체를 저장|
|boolean addAll(int index, Collection c)|지정된 위치부터 주어진 컬렉션의 모든 컬렉션의 모든 객체를 저장한다.|
|void clear()|ArrayList를 완전히 비운다.|
|Object clone()|ArrayList를 복제한다.|
|boolean contains(Object o)|지정된 객체(o)가 ArrayList에 포함되어 있는지 확인|
|void ensureCapacity(int minCapacity)|ArrayList의 용량이 최소환 minCapacity가 되도록 한다.|
|Object get(int index)|지정된 위치(index)에 저장된 객체를 반환한다.|
|int indexOf(Object o)|지정된 객체가 저장된 위치를 찾아 반환한다.|
|boolean isEmpty()|ArrayList가 비어 있는지 확인한다.|
|lterator iterator()|ArrayList의 Iterator객체를 반환.|
|int IastlndexOf(Object o)|객체(o가 저장된 위치를 끝부터 역방향으로 검색해서 반환|
|Listlterator listIterator()|ArrayList의 ListIterator를 반환|
|Listlterator listIterator(int index)|ArrayList의 지정된 위치부터 시작하는 ListIterator를 반환|
|Object remove(Object o)|지정된 위치(index)에 있는 객체를 제거한다.|
|boolean remove(Object o)|지정된 객체를 제한다.(성공하면 true 실패하면 false)|
|boolean removeAll(Collection c)|지정한 컬렉션에 저장된 것과 동일한 객체들을 ArrayList에서 제거한다.|
|boolean retainAll(Collection c)|ArrayList에 저장된 객체 중에서 주어진 컬렉션과 공통된 것들만 남기고 나머지는 삭제한다.|
|Object set(int index, Object element)|주어진 객체(element)를 지정한 위치(index)에 저장한다.|
|int size()|ArrayList에 저장된 객체의 개수를 반환한다.|
|void sort(int fromIndex, int tolndex)|fromIndex부터 toIndex사이에 저장된 객체를 반환한다.|
|Object[] toArray()|ArrayList에 저장된 모든 객체들을 객체배열로 반환한다.|
|Object[] toArray(Object[] a)|ArrayList에 저장된 모든 객체들을 객체배열 a에 담아 반환한다.|
|void trimTosize()|용량을 크기에 맞게 줄인다.(빈공간을 없앤다.)|

```java
package JavaStandardExample.CollectionFramework.ListInterface.ArrayList;

import java.util.ArrayList;
import java.util.Collections;

public class ArrayListEx1 {
    public static void main(String[] args) {
        ArrayList arrayList1 = new ArrayList(10);

        arrayList1.add(5);
        arrayList1.add(4);
        arrayList1.add(2);
        arrayList1.add(0);
        arrayList1.add(1);
        arrayList1.add(3);

        ArrayList arrayList2 = new ArrayList(arrayList1.subList(1, 4)); //1인덱스 부터 4인덱스 사이에 저장된 객체를 반환한다.
        print(arrayList1, arrayList2);

        Collections.sort(arrayList1); // arrayList1를 정렬함
        Collections.sort(arrayList2); // arrayList2를 정렬함
        print(arrayList1, arrayList2);

        //arrayList2가 arrayList1에 포함되어 있는지 확인
        System.out.println("list1.containsAll(arrayList2) : " + arrayList1.containsAll(arrayList2));

        arrayList2.add("B");
        arrayList2.add("C");

        arrayList2. add(3, "A");
        print(arrayList1, arrayList2);

        arrayList2.set(3, "AA");
        print(arrayList1, arrayList2);

        //arrayList1에 arrayList2의 값과 공통으로 포함된 항목이 있으면 공통된 항목만 남기고 나머지 삭제
        System.out.println("arrayList1.retainsAll(arrayList2) : " + arrayList1.retainAll(arrayList2));
        print(arrayList1, arrayList2);

        //arrayList2에서 arrayList1에 포함된 객체(항목의 값)를 삭제한다.
        for(int i = arrayList2.size()-1; i >= 0; i--){
            if(arrayList1.contains(arrayList2.get(i)))arrayList2.remove(i);
        }
        print(arrayList1,arrayList2);

    }
    static void print(ArrayList arrayList1, ArrayList arrayList2) {
        System.out.println("arrayList1" + arrayList1);
        System.out.println("arrayList2" + arrayList2);
        System.out.println();
    }

}

```

```java
arrayList1[5, 4, 2, 0, 1, 3]
arrayList2[4, 2, 0]

arrayList1[0, 1, 2, 3, 4, 5]
arrayList2[0, 2, 4]

list1.containsAll(arrayList2) : true
arrayList1[0, 1, 2, 3, 4, 5]
arrayList2[0, 2, 4, A, B, C]

arrayList1[0, 1, 2, 3, 4, 5]
arrayList2[0, 2, 4, AA, B, C]

arrayList1.retainsAll(arrayList2) : true
arrayList1[0, 2, 4]
arrayList2[0, 2, 4, AA, B, C]

arrayList1[0, 2, 4]
arrayList2[AA, B, C]
```

ArrayList는 List인터페이스를 구현했기 때문에 저장된 순서를 유지한다는 것을 알 수 있다.

arraylist2의 각 요소를 접근하기 위해 get(int index)메서드와 for문을 사용하였는데, for문의 변수 i를

0 부터 증가시킨 것이 아니라, ‘arrayList2.size()-1’ 부터 감소 시키면서 반대로 반복시켰다.

만일 변수 i를 감소가 아닌 증감하면서 index를 삭제하면, 한 요소가 삭제될 때 마다 빈공간을 채우기 위해

나머지 요소들이 자리이동을 하기 때문에 정확한 값을 가질 수 없기 때문에 i를 감소 시키면서 삭제를 해야

자리이동이 발생해도 영향을 받지 않고 결과 값을 얻을 수 있다.

```java
package JavaStandardExample.CollectionFramework.ListInterface.ArrayList;

import java.util.ArrayList;
import java.util.List;

public class ArrayListEx2 {
    public static void main(String[] args) {
        final int LIMIT = 10;
        String source = "0123456789abcdefghijABCDEFGHIJ!@$%^&*()ZZZ";
        int lenth = source.length();

        List list = new ArrayList(lenth / LIMIT + 10);

        for (int i = 0; i < lenth; i+=LIMIT){
            if(i + LIMIT < lenth){
                list.add(source.substring(i, i+LIMIT));
            } else {
                list.add(source.substring(i));
            }
        }

        for(int j = 0; j < list.size(); j++){
            System.out.println(list.get(j));
        }
    }
}
```

```java
0123456789
abcdefghij
ABCDEFGHIJ
!@#$%^&*()
ZZZ
```

긴 문자열 데이터를 원하는 길이로 잘라서 ArrayList에 담은 다음 출력한다.

단순히 문자열을 특정 크기로 잘라서 출력할 것이라면, charAt(int i)와 for문을 이용하면 되겠지만

ArrayList에 잘라서 담아 놓음으로써 ArrayList의 기능을 이용해서 다양한 작업을 간단하게 처리할 수 있다.

ArrayList를 생성할 때, 저장할 요소의 개수를 고려해서 실제 저장할 개수보다 약간 여유 있는 크기로 하는 것이

좋다. 생성할 때 지정한 크기보다 더 많은 객체를 저장하면 자동적으로 크기가 늘어나기는 하지만 이 과정에서

처리시간이 많이 소요되기 때문이다.