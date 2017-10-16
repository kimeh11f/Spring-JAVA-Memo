# JAVA-지네릭스  

지네릭의 사용 이유는, 만약 아래와 같이 중복된 코드를 리팩토링을 하여 하나의 클래스로 줄였을 때에, 컴파일 단계에서 타입체크를 하기 위함이다.

```
class StudentInfo{
	public int grade;
	StudentInfo(int grade) { this.grade = grade; }
}

class StudentPerson {
	public StudentInfo info;
	StudentPerson(StudentInfo info) { this.info = info; }
}

class EmployeeInfo{
	public int rank;
	EmployeeInfo(int rank) { this.rank = rank; }
}

class EmployeePerson{
	public EmployeeInfo info;
	EmployeePerson(EmployeeInfo info){ this.info = info; }
}

public class GenericDemo {

	public static void main(String[] args){
		StudentInfo si = new StudentInfo(2);
		StudentPerson sp = new StudentPerson(si);
		EmployeeInfo ei = new EmployeeInfo(1);
		EmployeePerson ep = new EmployeePerson(ei);
	}
}
```
위와 같은 코드를 아래와 같이 줄였을 때는, 문제가 있다.

```
class StudentInfo{
	public int grade;
	StudentInfo(int grade) { this.grade = grade; }
}

class EmployeeInfo{
	public int rank;
	EmployeeInfo(int rank) { this.rank = rank; }
}

class Person{
	public Object info;
	Person(Object info){ this.info = info; } //어떠한 클래스도 올 수 있게 줄임
}

public class GenericDemo {

	public static void main(String[] args){
		Person p1 = new Person("부장"); //문제점 1 : 의도와 다르게, String으로 파라미터를 넘김. 하지만, 체크 불가능.
		EmployeeInfo ei = (EmployeeInfo)p1.info; //문제점 2 : 문법상 아무 문제가 없어서 컴파일시 에러가 나지 않는 상황 발생. 실행시켜야 cast 에러 발생
	}
}
```
컴파일시, 오류를 검출할 수 있어야지만, 컴파일 언어가 제공하는 혜택을 받을 수 있다.  
그렇기 때문에, 지네릭을 사용한다.  

```
class StudentInfo{
	public int grade;
	StudentInfo(int grade) { this.grade = grade; }
}

class EmployeeInfo{
	public int rank;
	EmployeeInfo(int rank) { this.rank = rank; }
}

class Person<T, S>{
	public T info;
	public S id;
	Person(T info, S id){
		this.info = info;
		this.id = id;
	}
}

public class GenericDemo {

	public static void main(String[] args){
		Person<EmployeeInfo, int> p1 = new Person<EmployeeInfo, int>(new EmployeeInfo(1), 1); //지네릭에 올 수 있는 데이터 타입은 레퍼런스 타입만 올 수 있기에, 에러.
		Integer id = new Integer(1);
		Person<EmployeeInfo, Integer>p1 = new Person<EmployeeInfo, Integer>(new EmployeeInfo(1), id); //기본데이터타입 대신 wrapper클래스 사용.
		System.out.println(p1.id.intValue()); //intValue()함수를 사용해서 기본데이터 타입의 값으로 출력.
	}
}
```
# 오버로딩시 지네릭을 사용할 수 있는가

```
static Juice makeJuice(FruitBox<Fruit> box){
	String tmp = "";
	for(Fruit f : box.getList()) tmp += f+ " ";
	return new Juice(tmp);
}

static Juice makeJuice(FruitBox<Apple> box){
	String tmp = "";
	for(Fruit f : box.getList()) tmp += f+ " ";
	return new Juice(tmp);
}
```
위와 같이 오버로딩하면, 컴파일 에러가 발생한다. 지네릭 타입이 다른 것만으로는 오버로딩이 성립하지 않기 때문이다.

### 지네릭 타입은 컴파일러가 컴파일 할 때만 사용하고 제거해버리기 때문이다.
