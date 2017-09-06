
<code>
@Controller
public class MainController {
    @RequestMapping("/")
    public String hello(){
        return "Hello World";
    }
</code>

<code>
@Controller
public class MainController {
    @RequestMapping("/")
    @ResponseBody
    public String hello(){
        return "Hello World";
    }
</code>

<code>
@RestController
public class MainController {
    @RequestMapping("/")
    public String hello(){
        return "Hello World";
    }
</code>

@RestController : 뷰가 필요없는 API만 지원하는 서비스에서 사용, @ResponseBody를 포함하고 있음
@Controller : API와 뷰를 동시에 사용, 대신 API 서비스는 @ResponseBody를 붙여줘야 함
