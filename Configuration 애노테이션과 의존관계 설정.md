# Configuration 애노테이션과 의존관계설정
javaCode로 xml파일을 대신하여 설정을 할 수 있다.  
해당 애노테이션없이 만들었을 경우, 싱글톤 및 의존성주입이 일어나지 않았다. 
또한, @Configuration 애노테이션 사용시, 해당애노테이션이 사용된 클래스가 스프링 빈으로 등록된다.  
그래서, 자바설정코드 두 개가 있을 때 한 개를 나머지 하나에 Autowired로 설정해서 사용하면, 해당 설정코드에서 사용한 객체를 다른설정코드에 자동주입해서 사용도 가능하다.  

```
AppicationContext ctx = new GenericXmlApplicationContext("classpath:main-conf.xml");
```
만약 위처럼 애플리케이션 컨텍스트에 XML 파일을 사용시에는  
애노테이션을 통한 의존관계를 설정하기 위해서 
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
```<context:annotation-config/>```를 통해서 아래의 BeanPostProcessor들이 등록되어 애노테이션을 인식하게 된다.  
RequiredAnnotationBeanPostProcessor : @Required 애노테이션 처리  

AutowiredAnnotationBeanPostProcessor : @Autowired 애노테이션 처리  

CommonAnnotationBeanPostProcessor : @Resource, @PostConstruct,@PreDestroy 애노테이션 처리  

ConfigurationClassBeanPostProcessor : @Configuration 애노테이션 처리  

예를들어, ```<bean class="org.springframework.beans.factory.annotation.RequiredAnnotationBeanPostProcessor"/>``` 
이러한 빈을 따로 등록할 필요가 없어진다.  
빈 후처리기는 새로운 빈을 등록해주지는 않지만, 애노테이션 의존관계 정보를 읽어서 이미 등록된 빈의 메타정보에 프로퍼티 항목을 추가해주는 작업을 한다.
```
AppicationContext ctx = new AnnotationConfigApplicationContext(JavaConf.class); //또는
AppicationContext ctx = new AnnotationConfigWebApplicationContext(JavaConf.class);
```
위와같이, 애플리케이션 컨텍스트를 AnnotationConfigApplicationContext나 AnnotationConfigWebApplicationContext 로  
JAVA클래스파일로 했을경우, 애노테이션을 통한 DI 설정은 자동으로 활성화된다.
JAVA설정에서 XML설정을 임포트하려면
```
@Configuration
@ImportResource("classpath:sub-conf.xml")
```
위 애노테이션을 사용한다.
