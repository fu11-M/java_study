## Stack과 Queue의 기본 개념과 특징

Stack은 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 LIFO(Last In First Out)

구조로 되어있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ea204791-94b0-4594-95e9-37705edf8245/75a86973-833f-4d30-a670-072e98a2ee6a/Untitled.png)

스택에 a, b, c의 순서로 데이터를 넣었다면 꺼낼 때는 c, b, a의 순서로 꺼내게 된다.

Queue는 처음에 저장한 데이터를 가장 먼저 꺼내게 되는 FIFO(First In First Out)

구조로 되어있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ea204791-94b0-4594-95e9-37705edf8245/ebc1eae9-b447-4eb6-8a6b-98641c79eabf/Untitled.png)

Queue는 a, b, c의 순서로 데이터를 넣었다면 꺼낼 때 역시 a, b, c 순서로 꺼내게 된다.

그렇다면 Stack과 Queue를 구현하기 위해서는 어떤 컬렉션 클래스를 사용하는 것이 좋냐면

순차적으로 데이터를 추가하고 삭제하는 Stack에는 ArrayList와 같은 배열 기반의 컬렉션

클래스가 적합하지만, Queue 데이터를 꺼낼 때 항상 첫 번째 저장된 데이터를 삭제하므로,

ArrayList와 같은 배열 기반의 컬렉션 클래스를 사용한다면 데이터를 꺼낼 때마다 빈 공간을

채우기 위해 데이터의 복사가 발생하므로 비효율적이다. 하여 Queue는 ArrayList보다 데이터의

추가/삭제가 쉬운 LinkedList로 구현하는 것이 더 적합하다.

```java
package ch07;

import java.util.*;

public class Stack_Queue {
	public static void main(String[] args) {
		Stack stack = new Stack();
		Queue queue = new LinkedList();
		
		stack.push("0");
		stack.push("1");
		stack.push("2");
		
		queue.offer("0");
		queue.offer("1");
		queue.offer("2");
		
		System.out.println("===Stack===");
		while(!stack.empty()){ // empty() -> Stack이 비어있는지 알려준다.
			System.out.println(stack.pop());
		}
		
		System.out.println("===Queue===");
		while(!queue.isEmpty()) {
			System.out.println(queue.poll());
		}
	}
}
```

```java
===Stack===
2
1
0
===Queue===
0
1
2
```

Stack과 Queue의 활용

```java
package ch07;

import java.util.*;

public class StackEx1 {
	public static Stack back = new Stack();
	public static Stack forward = new Stack();
	
	public static void main(String[] args) {
		goURL("1.네이트");
		goURL("2.야후");
		goURL("3.네이버");
		goURL("4.다음");
		
		printStatus();
		
		goBack();
		System.out.println("= '뒤로' 버튼을 누른 후 =");
		printStatus();
		
		goBack();
		System.out.println("= '뒤로' 버튼을 누른 후 =");
		printStatus();
		
		goForward();
		System.out.println("= '앞으로' 버튼을 누른 후 =");
		printStatus();
		
		goURL("gmail.com");
		System.out.println("= 새로운 주소 이동 후=");
		printStatus();
	}
	
	public static void printStatus() {
		System.out.println("back:" + back);
		System.out.println("forward:" + forward);
		System.out.println("현재 화면은 '" + back.peek() + "' 입니다." );
		System.out.println();
	}
	
	public static void goURL(String url) {
		back.push(url);
		if(!forward.empty()) {
			forward.clear();
		}
	}
	
	public static void goForward() {
		if(!forward.empty()) {
			back.push(forward.pop());
		}
	}
	
	public static void goBack() {
		if(!back.empty()) {
			forward.push(back.pop());
		}
	}
}
```

```java
package ch07;

import java.util.*;

public class QueueEx1 {
	static Queue q = new LinkedList();
	static final int MAX_SIZE = 5;
	
	public static void main(String[] args) {
		System.out.println("help를 입력하면 도움말을 볼 수 있습니다.");
		
		while(true) {
			System.out.println(">>");
			try {
				Scanner scanner = new Scanner(System.in);
				String input = scanner.nextLine().trim();
				
				if("".equals(input)) continue;
				
				if(input.equalsIgnoreCase("q")) {
					System.exit(0);
				}else if(input.equalsIgnoreCase("help")) {
					System.out.println(" help - 도움말을 보여줍니다.");
					System.out.println(" q 또는 Q - 프로그램을 종료합니다.");
					System.out.println(" hostory - 최근에 입력한 명령어를" + MAX_SIZE + "개 보여줍니다.");
					
				}else if(input.equalsIgnoreCase("history")) {
					int i = 0;
					save(input);
					
					LinkedList tmp = (LinkedList) q;
					ListIterator it = tmp.listIterator();
					
					while(it.hasNext()) {
						System.out.println(++i+"."+it.next());
					}
				}else {
					save(input);
					System.out.println(input);
				} 
			} catch(Exception exception) {
				System.out.println("입력 오류 입니다.");
			}
		}
	}

	public static void save(String input) {
		if(!"".equals(input)) {
			q.offer(input);
		}
		
		if(q.size() > MAX_SIZE) {
			q.remove();
		}
	}
}

```

