Object Oriented Programing(객체 지향 프로그래밍)은 현실 세계의 존재하는 모든 것을 소프트웨어에서 독립적인 객체로 정의하고 설계(모델링)하여 데이터와 데이터를 처리 하는 기능을 객체로 묶어 각각의 객체들이 서로 상호작용하는 조립형식으로 설계 하는 프로그래밍 방법론이다.

객체는 데이터를 나타내는 속성과 데이터를 처리 하는 기능인 동작으로 구성되는데 java에서 속성은 필드(field) 동작은 메소드(method)라고 부른다. 
즉 필드, 변수, 메소드를 객체에 모아서 그룹핑 하고 정리정돈 하고 서로 상호작용하며 프로그래밍 하는 것을 말한다. 

Object Oriented Programing(객체 지향 프로그래밍)은 객체들 간의 상호작용을 통해서 
추상화 : 공통의 속성 기능을 묶고 이름을 붙여 복잡한 시스템을 단순화하고 필요한 부분만 표기하고 필요하지 않은 것들은 숨기는 것을 의미한다.
다형성 : 한 객체가 여려 형태를 가질 수 있는 특성
상속 :  부모 Class의 특성과 기능을 자식 클래스가 상속받는 것을 의미
캡슐화 : 객체의 데이터와 그 데이터를 다루는 메서드들을 하나로 묶는 것 이 객체는 외부에서 직접 접근할 수 없고, 내부 메서드를 통해서만 접근 가능함
와 같은 기능으로 소프트웨어를 모듈화하고 규모가 커질수록 복잡해지는 코드를 유연하게 만들며 이로 인한 코드의 확장, 유지보수, 재사용성을 통한 생산성이 높은 프로젝트를 구현할 수 있는 장점이 있다.

단점으로는 여러 객체를 만들고 상호작용하기 때문에 설계하는 과정이 복잡하여 많은 시간과 비용이 소요되고 프로그램 실행시 처리되는 시간이 오래 걸린다. 

Object Oriented Programing(객체 지향 프로그래밍)과 다른 개념으로는 Procedural Programing(절차 지향 프로그래밍)이 존재하는데 일련의 처리 절차를 정해진 문법에 따라 순서대로 기술하고 Procedure
(프로시저)라고 하는 루틴, 서브 루틴,  method, 함수와 같은 기능들로만 결합하여 프로그램을 만드는 프로그래밍 기법이며 코드가 TOP~Down방향으로 순차적으로 진행되기 때문에 프로그램 실행 속도가
빠르고 이로 인한 개발을 하는 시간 및 비용이 적게 소요된다. 대표적인 언어로 C언어가 있다.

단점으로는 전체의 기능을 하나의 함수로 구현하고 절차적이기 때문에 프로그램에서 버그 발생시 모든 코드를 확인 해야 하는 상황이 생겨 어느 부분이 버그 인지 디버깅에 어려움이 있고 코드의 순서를 변경할 시 모든 코드에 영향을 주기 때문에 실행이 어려워진다.

Object Oriented Programing(객체 지향 프로그래밍)이 나오게 된 배경에는 기존의 Procedural Programing(절차 지향 프로그래밍)의 소프트웨어들은 모든 코드들이 서로 연관되어 있어 코드의 일부분을 고치려면 설계의 전체적인 부분을 고쳐야 하는 상황이 발생하였고 이런 상황이 반복되면 프로젝트를 완성하기까지 시간이 오래 걸리고 작업이 번거롭게 되는데 이런 문제점을 해결하기 위해서 Object Oriented Programing(객체 지향 프로그래밍) 방법론이 나오게 되었다.

하지만 method로만 프로그램을 만들기에 부족함을 느껴Object Oriented Programing(객체 지향 프로그래밍)프로그래밍 방법론을 만들게 되고 이를 지원하는 언어가 객체지향언어 이며 현재 학습하고 있는 java를 포함하여 C++, Python등이 객체지향언에 속한다.