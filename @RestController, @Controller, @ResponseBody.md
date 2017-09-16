# @RestController, @Controller

```
@Controller
public class MainController {
    @RequestMapping("/")
    public String hello(){
        return "Hello World";
    }
```
위 소스는 브라우저 화면에 글씨가 띄워지지 않음. 기본적으로 뷰의 이름을 리턴하기 때문. 해당 뷰이름에 해당하는 파일이 미존재하는 경우.
```
@Controller
public class MainController {
    @RequestMapping("/")
    @ResponseBody
    public String hello(){
        return "Hello World";
    }
```
위 소스는 브라우저 화면에 글씨가 띄워짐
```
@RestController
public class MainController {
    @RequestMapping("/")
    public String hello(){
        return "Hello World";
    }
```
위 소스는 브라우저 화면에 글씨가 띄워짐

@RestController : 뷰가 필요없는 API만 지원하는 서비스에서 사용, @ResponseBody를 포함하고 있음  
```
    @RequestMapping("/a")
    public ResponseEntity a(){
        Test t = new test();
        t.setName("홍길동");
        t.setPassword("1234");
        return new ResponseEntity<>(t, HttpStatus.CREATED);
    }
```
@RestController의 경우, 객체로 return을 해주면, 
```
Content-Type:application/json;charset=UTF-8
Date:Sat, 16 Sep 2017 11:28:21 GMT
Transfer-Encoding:chunked
```
```
{"name":"홍길동","password":"1234"}
```
위와 같이, 응답은 자동으로 json형식으로 넘어가게 된다.

@Controller : API와 뷰를 동시에 사용, 대신 API 서비스는 @ResponseBody를 붙여줘야 함

# @ResponseBody
@ResponseBody가 메소드 레벨에 부여되면 메소드가 리턴하는 오브젝트는 뷰를 통해 결과를 만들어내는 모델로 사용되는 것이 아니라, 메시지 컨버터를 통해 바로 HTTP응답의 메지 본문으로 전환된다.  
@ResponseBody가 없다면, 스트링 타입의 리턴 값은 뷰 이름으로 인식된다.  
하지만, @ResponseBody가 붙으면 스트링타입을 지원하는 메시지 컨버터가 이를 변환해서 HttpServletResponse의 출력스트림에 넣어버린다.  
근본적으로 @RequestBody, @ResponseBody는 XML이나 JSON과 같은 메시지 기반의 커뮤니케이션을 위해 사용된다.
