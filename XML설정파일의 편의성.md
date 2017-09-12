# XML설정파일의 편의성
```
public class CarTester {
	public static void main(String[] args){
	AbstractApplicationContext ctx = new GenericXmlApplicationContext("classpath:car.xml");
	Car car = ctx.getBean("car", Car.class);
	car.drive();
	}
}
```
```
Car car = ctx.getBean("car", Car.class);
```
위 부분에서, Car타입은 인터페이스이고, Car.class도 Car타입과 일치해야한다.

위의 소스는 건들지 않은 상태에서, xml파일의 편집만으로, 인터페이스 Car 타입에 맞는 "car" bean을 변경시켜서
의존객체를 변경 가능하다.(com.test.HyndaiCar클래스와 com.test.KiaCar클래스는 Car인터페이스를 구현한다.)  

car.xml 파일  
```
<bean id ="car" class="com.test.HyndaiCar"/>
```
결과 : "현대차를 운전한다."  
위 에서, 아래 처럼 변경시에는,
```
<bean id ="car" class="com.test.KiaCar"/>
```
결과 : "기아차를 운전한다."
