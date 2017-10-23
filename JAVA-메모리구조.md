# JVM 메모리 구조
응용프로그램이 실행되면, JVM은 시스템으로부터 프로그램을 수행하는데 필요한 메모리를 할당받고 JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.  
Runtime Data Area의 3가지 주요 영역에는 method area, call stack, heap 이 있다.

### method area
메서드 영역은 모든 스레드가 공유하는 영역으로 JVM이 시작될 때 생성된다.  
JVM이 읽어들인 클래스와 인터페이스 대한 런타임 상수 풀(상수 자료형을 저장하여 참조하고 중복을 막는 역할), 멤버 변수(필드), 클래스 변수(Static 변수), 생성자와 메소드를 저장하는 공간이다.  
프로그램 실행 중 어떤 클래스가 사용되면, jvm은 해당 클래스의 클래스파일(.class)을 읽어서 분석하여 클래스에 대한 정보(클래스데이터)를 이곳에 저장한다.  
이 때, 그 클래스의 클래스변수도 이 영역에 함께 생성된다.  
가비지컬렉션은 JVM 벤더의 선택 사항이다.
1) Field Information  
멤버변수의 이름, 데이터 타입, 접근 제어자에 대한 정보
2) Method Information  
메소드의 이름, 리턴타입, 매개변수, 접근제어자에 대한 정보
3) Type Information  
Type의 속성이 Class인지 Interface인지의 여부 저장
 - Type의 전체이름(패키지명+클래스명)
 - Type의 Super Class의 전체이름 (단, Type이 Interface이거나 Object Class인 경우 제외)
 - 접근 제어자 및 연관된 interface의 전체 리스트 저장
4) 런타임 상수 풀(Runtime Constant Pool)
 - Type에서 사용된 상수를 저장하는 곳(중복이 있을 시 기존의 상수 사용)
 - 문자 상수, 타입, 필드, 메서드 레퍼런스도 저장
 - 즉,어떤 메서드나 필드를 참조할 때 JVM은 런타임 상수 풀을 통해 해당 메서드나 필드의 실제 메모리상 주소를 찾아서 참조
5) Class Variable
 - Static 변수라고도 불림
 - 모든 객체가 공유 할 수 있고, 객체 생성 없이 접근 가능
6) Class 사용 이전에 메모리 할당
 - final class 변수의 경우(상수로 치환되어) 상수 풀에 값 복사

### call stack
호출스택은 메서드의 작업에 필요한 메모리 공간을 제공한다.  
 - 메서드 호출 시마다 각각의 스택프레임(그 메서드만을 위한 공간)이 생성  
 - 메서드 안에서 사용되어지는 값들 저장, 호출된 메서드의 매개변수, 지역변수, 리턴 값 및 연산 시 일어나는 값들을 임시로 저장  
 - 메서드가 수행을 마치고나면 사용했던 메모리를 반환하고 스택에서 제거된다.  
Last In First Out (LIFO)  
호출스택의 제일 위에 있는 메서드가 현재 실행 중인 메서드이고, 아래에 있는 메서드가 바로 위의 메서드를 호출한 메서드이다.
각 thread는 자신들만의 고유한 스택영역을 가지고 있다.  
기본(원시)타입 변수는 스택 영역에 직접 값을 가진다.  
참조타입 변수는 힙 영역이나 메소드 영역의 객체 주소를 가진다.  

### heap
인스턴스가 생성되는 공간. 프로그램 실행 중 생성되는 인스턴스는 모두 이곳에 생성된다.  
힙 영역에 생성된 객체와 배열은 스택 영역의 변수나 다른 객체의 필드에서 참조한다.  
클래스영역에 로드된 클래스만 생성 가능하다.  
가비지 콜렉터를 통해서 메모리를 반환한다.  
JVM성능 등의 이슈에서 가장 많이 언급되는 공간으로, 객체가 더 이상 사용되지 않거나 명시적으로 null 선언 시 Garbage Collection 대상이 된다.
모든 스레드에서 공유한다.  

#### Stack is used for execution purpose and heap is used for storage purpose

#### heap, method area(런타임상수풀 포함)는 모든 쓰레드가 공유해서 사용한다.

#### heap영역에는 String 상수 저장을 위한 별도 공간이 있다. (string constants pool)
In that heap memory, JVM allocates some memory specially meant for string literals. This part of the heap memory is called string constants pool
So for example, if you init the following objects
```
String s1 = "abc"; 
String s2 = "123";
String obj1 = new String("abc");
String obj2 = new String("def");
String obj3 = new String("456);
```
String literals s1 and s2 will go to string constant pool, objects obj1, obj2, obj3 to the heap. All of them, will be referenced from the Stack.  
Also, please note that "abc" will appear in heap and in string constant pool.  
Why is String s1 = "abc" and String obj1 = new String("abc") will be created this way? It's because String obj1 = new String("abc") explicitly creates a new and referentially distinct instance of a String object and  String s1 = "abc" may reuse an instance from the string constant pool if one is available. 

### PC Register
PC 레지스터는 각 쓰레드 마다 존재하며, 쓰레드가 시작될 때 생성된다. PC 레지스터는 현재 수행중인 JVM 명령의 주소를 가진다.

### Native Method Stack
자바 외의 언어로 작성된 네이티브 코드를 위한 스택이다.  
쓰레드마다 생성된다.
