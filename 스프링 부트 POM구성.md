스프링 부트는 프로젝트구성에 필요한 의존성을 자동 구성해준다.

```
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.6.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
```
위는 스프링부트 상위 의존체. 앱 실행에 필요한 라이브러리가 담겨있다.  

```
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
```

위는 실제로 갖다 쓸 스프링 부트 기능에 해당하는 의존체. 스타터폼은 앱에 필요한 의존체를 전부 알아서 넣는다.
예를들어, 웹 애플리케이션 프로젝트면 spring-boot-starter-web 하나만 있으면 된다.
