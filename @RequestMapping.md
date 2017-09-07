# RequestMapping

타입레벨뿐 아니라, 매소드레벨에도 붙일 수 있다.
타입레벨의 정보를기준으로 삼고, 메소드 레벨의 정보로 세분화한다.  

### URL 패턴  
```
@RequestMaping("/hello")
@RequestMaping({"/hello", "/hello/"})
@RequestMaping("/main*")
@RequestMaping("/admin/**/user")
```
위와 같이 사용할 수 있다.  
확장자가 붙어있지않고 /로 끝나지도 않는 경우에는, 접미어처럼 인식되어, /hello 나 /hello.html 이나 같은 결과가 나온다.  

### mapping
```
@RequestMaping("/user")
public class UserController{
  @RequestMapping("/add") public String add(...){}
}
```
위는 /user/add로 결합된다.

```
public class UserController{
  @RequestMapping("/add") public String add(...){}
}
```
타입레벨에 아무것도 없는 위의 경우에는 클래스자체가 매핑대상으로 등록되지않아서, 매핑이 일어나지 않는다.  
이 때는 아래 처럼 아무 내용이없는 @RequestMapping이라도 붙여야한다.
```
@RequestMapping
public class UserController{
  @RequestMapping("/add") public String add(...){}
}
```
  
```
@Controller
public class UserController{
  @RequestMapping("/add") public String add(...){}
}
```
위와같이, @Controller를 사용하여 빈자동스캔방식으로 등록되게 했다면, @RequestMapping을 생략가능하다.  
스프링이 애노테이션방식을 사용한 클래스라고 판단하기 때문이다.
