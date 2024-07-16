배열은 가장 기본적인 형태의 자료구조로 구조가 간단하며 사용하기 쉽고 데이터를 읽어오는데 
걸리는 시간(접근 시간, access time)이 가장 빠르다는 장점을 가지고 있지만 단점으로는 크기를 
변경할 수 없으며 비 순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.

배열은 크기를 변경할 수 없어 배열의 크기를 조정하고 싶을 경우에는 새로운 배열을 생성해서 
기존의 데이터를 복사해야 하며 애플리케이션이 처리해야 할 데이터의 양을 정확히 예측할 수 없을
때 크기에 의한 배열 재 할당 및 데이터 복사 작업과 같이 실행 중에 배열의 크기를 조정하게 되면 실행 
속도가 저하된다. 

실시간 시스템과 같은 실행 속도 및 처리 지연이 매우 중요한 애플리케이션은 데이터 처리에 발생하는 지연이 사용자에게 직접적인 영향을 미친다. 
하여 미리 배열의 크기를 크게 배열의 재 할당과 데이터 복사를 줄여 실행 속도를 향상 시키지만 메모리를 많이 사용한다는 단점이 있다. 

이러한 배열의 단점을 보완하기 위해서 LinkedList라는 자료구조가 고안되었다.
배열은 모든 데이터가 연속적으로 존재하지만 LinkedList는 데이터가 서로 연결되어 있는 형태로 구성 되어있다.

링크드 리스트의 각 요소(node)들은 자신과 연결된 다음 요소에 대한 참조(주소 값)와 데이터로 구성되어 있다.

링크드 리스트에서의 데이터 삭제는 간단하다. 삭제하고자 하는 요소의 이전 요소가 삭제 하고자 하는 요소의 다음 요소를 참조하도록 변경하기만 하면 된다. 
하나의 참조만 변경하면 삭제가 가능하기 때문에 배열처럼 데이터를 이동하기 위해 복사하는 과정이 없기 때문에 처리 속도가 빠르다.

위의 그림과 같이 삭제할 요소의 이전 요소가 삭제할 요소의 다음 요소를 참조하면 삭제할 요소는 리스트에서 연결이 끊어지게 되어 리스트의 일부가 아니게 되고 
가비지 켈럭터(Garbage Collector)가 주기적으로 메모리를 스캔하여 더 이상 참조 되지 않는 객체들을 찾아내어 메모리에서 해제한다.

새로운 데이터를 추가할 때는 새로운 요소를 생성한 다음 추가하고자 하는 위치의 이전 요소의 참조를 새로운 요소에 대한 참조로 변경해주고, 
새로운 요소가 그 다음 요소를 참조하도록 변경하면 되므로 처리 속도가 매우 빠르다.

링크드 리스트는 이동 방향이 단 방향이기 때문에 다음 요소에 대한 접근은 쉽지만 이전 요소에 대한 접근은 어렵다. 
이 점을 보완한 것이 더블 링크드 리스트(doubly linked list)이다.

단순히 링크드 리스트에 참조 변수를 하나 더 추가하여 다음 요소에 대한 참조 뿐 아니라 이전 요소에 대한 참조가 가능하도록 하였고 기본적인 것은 링크드 리스트와 같다.

더블 링크드 리스트는 링크드 리스트보다 각 요소에 대한 접근관 이동이 쉽기 때문에 링크드 리스트보다 많이 사용된다.

더블 링크드 리스트의 접근성 보다 향상 시킨 것이 “더블 써큘러 링크드 리스트”이다. 더블 써큘러 링크스 리스트는 이중 원형 연결 리스트(doubly circular linked list)

이며 더블 링크드 리스트에서 첫 번째 요소와 마지막 요소를 서로 연결시킨 것이다. 

이렇게 하면 마지막 요소의 다음 요소가 첫 번째 요소가 되고, 첫 번째 요소의 이전 요소가 마지막 요소가 된다.

실제로 LinkedList클래스는 이름과 달리 ‘링크드 리스트’가 아닌 더블 링크드 리스트로 구현되어 있다.
이는 링크드 리스트의 단점인 낮은 접근성(accessability)을 높이기 위 한 것이다.

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class ArrayListLinkedListTest {
    public static void main(String[] args) {
        ArrayList arrayList = new ArrayList(2000000);
        LinkedList linkedList = new LinkedList();

        System.out.println("===순차적으로 추가하기===");
        System.out.println("ArrayList : " + add1(arrayList));
        System.out.println("ArrayList : " + add1(linkedList));
        System.out.println();

        System.out.println("===중간으로 추가하기===");
        System.out.println("ArrayList : " + add2(arrayList));
        System.out.println("ArrayList : " + add2(linkedList));
        System.out.println();

        System.out.println("===중간에서 삭제하기===");
        System.out.println("ArrayList : " + remove2(arrayList));
        System.out.println("ArrayList : " + remove2(linkedList));

        System.out.println("===순차적으로 삭제하기===");
        System.out.println("ArrayList : " + remove1(arrayList));
        System.out.println("ArrayList : " + remove1(linkedList));

    }

    public static long add1(List list){
        //현재 시간을 밀리세컨드(1/1000초) 단위로 가져와서 long 타입의 start에 저장한다.
        long start = System.currentTimeMillis();

        for(int i = 0; i<1000000; i++){
            list.add(i + "");
        }
        long end = System.currentTimeMillis();

        return end - start;
    }

    public static long add2(List list){
        long start = System.currentTimeMillis();

        for(int i = 0; i <1000000; i++) {
            list.add(500, "X");
        }
        long end = System.currentTimeMillis();

        return end - start;
    }

    public static long remove1(List list){
        long start = System.currentTimeMillis();

        for(int i = list.size()-1; i >= 0; i--){
            list.remove(i);
        }
        long end = System.currentTimeMillis();

        return end - start;
    }

    public static long remove2(List list){
        long start = System.currentTimeMillis();

        for(int i = 0; i < 10000; i++){
            list.remove(i);
        }
        long end = System.currentTimeMillis();

        return end - start;
    }
}
}
```

```java
===순차적으로 추가하기===
ArrayList : 284
LinkedList : 406

===중간에 추가하기===
ArrayList : 3453
LinkedList : 16

===중간에 삭제하기===
ArrayList : 2641
LinkedList : 234

===순차적으로 삭제하기===
ArrayList : 0
LinkedList : 31
```

순차적으로 추가, 삭제하는 경우에는 ArrayList가 LinkedList보다 빠르다. 그 이유는 순차적 추가 같은 경우에는 단순히 저장하는 시간을 비교할 수 있도록 하기 위해서 
ArryList를 생성할때는 저장할 데이터의 개수만큼 충분한 초기 용량을 확보하였기 때문에 저장 공간이 부족하여 새로운 ArrayList를 생성해야 하는 상황이 일어나지 않아 ArrayList가 더 빠른 것이다. 

만약 ArrayList의 크기가 충분하지않아 새로운 크기의 ArrayList를 생성하고 데이터를 복사하는 경우가 생긴다면 LinkedList가 더 빠를 확률이 높다. 

순차적 삭제 같은 경우에는  마지막 데이터부터 역순으로 삭제하기 때문에 ArrayList는 각 요소들의 재배치를 하는 경우에 시간이 많이 걸리는데 마지막 데이터부터
순차적으로 삭제한다면 각 요소들의 재배치가 필요하지 않기 때문에 ArrayList가 더 빠른것이다.

중간 데이터를 추가, 삭제하는 경우에는 LinkedList가 ArrayList보다 더 빠르다. 그 이유는 중간 요소를 추가 또는 삭제하는 경우, LinkedList는 각 요소 간의 연결만
변경해주면 되지만 ArrayList는 각 요소들을 재배치 하여 추가할 공간을 확보하거나 빈 공간을 채워야 하기 때문이다.