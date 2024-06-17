Vector란 List 인터페이스를 상속받은 요소 추가 및 제거를 수용하기 위해 필요에 따라 확장하거나 축소할 수 
있는 동적 배열을 나타낸다.

```java
package JavaStandardExample.CollectionFramework.ListInterface.Vector;
import java.util.*;

public class VectorEx1 {
    public static void main(String[] args) {
        Vector vector = new Vector(5); // 용량(capacity)이 5인 Vector를 생성한다.
        vector.add("1");
        vector.add("2");
        vector.add("3");
        print(vector);

        vector.trimToSize(); // 빈 공간을 없앤다. (용량과 크기가 같아진다.)
        System.out.println("=== After trimTosize() ===");
        print(vector);

        vector.ensureCapacity(6);
        System.out.println("=== After ensure Capacity(6) ===");
        print(vector);

        vector.setSize(7);
        System.out.println("=== After setSize(7) ===");
        print(vector);

        vector.clear();
        System.out.println("=== After clear() ===");
        print(vector);
    }

    public static void print(Vector vector){
        System.out.println(vector);
        System.out.println("size : " + vector.size());
        System.out.println("capacity : " + vector.capacity() + "\\n");
    }
}

```

```java
[1, 2, 3]
size : 3
capacity : 5

=== After trimTosize() ===
[1, 2, 3]
size : 3
capacity : 3

=== After ensure Capacity(6) ===
[1, 2, 3]
size : 3
capacity : 6

=== After setSize(7) ===
[1, 2, 3, null, null, null, null]
size : 7
capacity : 12

=== After clear() ===
[]
size : 0
capacity : 12
```

이 코드는 Vector의 용량(capacity)과 크기(size)에 관한 실행 과정에 관한 것이다.

capacity(용량)가 5인 Vector인스턴스 vector를 생성하고, “1”. “2”, “3” 즉 3개의 객체를 저장하면

vector에 저장된 값은 1,2,3이 되고, 총 용량은 5, size는 3이 된다.

배열은 크기를 변경할 수 없기 때문에 새로운 배열을 생성해서 그 주소 값을 변수 vector에 할당한다.

기존의 Vector인스턴스는 더 이상 사용할 수 없으며, 후에 garbage collector에 의해서 메모리에서 제거된다.

v.ensureCapacity(6)은 vector의 용량이 최소한 6이 되도록한다.

만약 vector의 capacity가 6이상 이라면 아무일도 일어나지 않지만 위의 코드는 v.trimToSize()를 사용하였기 때문에

vector의 capacity가 3이므로 크기가 6인 배열을 생성해서 vector내용을 복사한다.

여기서 기존의 인스턴스를 다시 사용하는 것이 아니라 새로운 인스턴스를 생성하였다는 것을 유의해야한다.

v.setSize(7)는 v의 size가 7이 되도록 한다. 만약 vactor의 capacity가 충분하면 새로 인스턴스를 생성하지 않아도 되지만

지금은 capacity가 7으로 변경되었음으로 새로운 인스턴스를 생성해야 한다. Vector는 capacity가 부족할 경우 자동적으로

기존의 크기보다 2배의 크기로 증가 되기 때문에 vector의 capacity는 12가 된다.

v.clear();는 v의 모든 요소를 삭제하기 때문에 값과 size가 모두 없어지게 되고 capacity(용량)만 남게 된다.

ArrayList나 Vetor같이 배열을 이용한 자료구조는 데이터를 읽어오고 저장하는 데는 효율이 좋지만, 용량을 변경해야 할 때는

새로운 배열을 생성한 후 기존의 배열로부터 새로 생성된 배열로 데이터를 복사 해야 하기 때문에 효율이 떨어진다는 단점을 가지고 있다.

하여 처음 인스턴스를 생성할 때, 저장할 데이터의 개수를 잘 고려하여 충분한 용량의 인스턴스를 생성하는 것이 좋다.