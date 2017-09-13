# Configuration 애노테이션  
javaCode로 xml파일을 대신하여 설정을 할 수 있다.  
해당 애노테이션없이 만들었을 경우, 싱글톤 및 의존성주입이 일어나지 않았다. 
또한, @Configuration 애노테이션 사용시, 해당애노테이션이 사용된 클래스가 스프링 빈으로 등록된다.  
그래서, 자바설정코드 두 개가 있을 때 한 개를 나머지 하나에 Autowired로 설정해서 사용하면, 해당 설정코드에서 사용한 객체를 다른설정코드에 자동주입해서 사용도 가능하다.  

```
AppicationContext ctx = new GenericXmlApplicationContext("classpath:main-conf.xml");
```
만약 위처럼 애플리케이션 컨텍스트에 XML 파일을 사용시에는  
어떠한 애노테이션이더라도 사용가능하게 하려면, 
```
<beans xmlns:context="http://www.springframework.org/schema/context
xsi:schemaLocation="http://www.springframework.org/schema/context
		http://www.springframework.org/schema/context/spring-context-3.2.xsd">
<context:annotation-config/>
```
위와같은 설정이 선행되어야 한다. 이 설정이 된 후
```
<bean class="config.JavaConf"/>
```
위와같이, xml파일에 해당 java설정클래스를 bean으로 등록해준다. 그럼, xml설정파일에 JAVA설정을 IMPORT해서 사용가능하다.

```
AppicationContext ctx = new AnnotationConfigApplicationContext(JavaConf.class);
```
위와같이, 애플리케이션 컨텍스트 사용을 JAVA클래스파일로 했을경우, 애노테이션사용은 자동으로 활성화된다.
JAVA설정에서 XML설정을 임포트하려면
```
@Configuration
@ImportResource("classpath:sub-conf.xml")
```
위 애노테이션을 사용한다.
