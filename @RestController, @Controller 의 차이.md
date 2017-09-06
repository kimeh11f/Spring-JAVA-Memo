# @RestController, @Controller 의 차이  

```
@Controller
public class MainController {
    @RequestMapping("/")
    public String hello(){
        return "Hello World";
    }
```
위 소스는 화면에 글씨가 띄워지지 않음
```
@Controller
public class MainController {
    @RequestMapping("/")
    @ResponseBody
    public String hello(){
        return "Hello World";
    }
```
위 소스는 화면에 글씨가 띄워짐
```
@RestController
public class MainController {
    @RequestMapping("/")
    public String hello(){
        return "Hello World";
    }
```
위 소스는 화면에 글씨가 띄워짐

@RestController : 뷰가 필요없는 API만 지원하는 서비스에서 사용, @ResponseBody를 포함하고 있음  
@Controller : API와 뷰를 동시에 사용, 대신 API 서비스는 @ResponseBody를 붙여줘야 함
