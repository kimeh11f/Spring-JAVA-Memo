# JUnit 테스트코드 작성 예시

@Transactional  
- 테스트클래스에 @Transactional이 붙어있어야, 기본적으로 각 @Test 메서드별로 DB롤백이 된다.

@FixMethodOrder(MethodSorters.NAME_ASCENDING)  
- 테스트클래스에 붙어있으면, 메서드 이름 순으로 테스트를 수행한다. 기본적으로, 테스팅순서는 보장되지 않기 때문에, 순서를 보장할 수 있는 방법이다.

@Commit  
- @Test메서드에 해당 애너테이션을 붙이면, 테스트 후, 롤백이 수행되지 않고, 다음 테스트로 넘어간다.
- @Rollback(false)와 같은데, 좀 더 이후에 나왔다. 4.2버전

아래는 테스트 순서 정하기와 commit을 사용한 예제
```
@RunWith(SpringJUnit4ClassRunner.class) //테스트 속도 줄이기의 핵심. @TEST마다 애플리케이션 컨텍스트의 재사용.
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.MOCK)
@Transactional
@FixMethodOrder(MethodSorters.NAME_ASCENDING)
public class AccountControllerTest {

    @Autowired
    WebApplicationContext wac;
    @Autowired
    ObjectMapper objectMapper;

    MockMvc mockMvc;

    @Before
    public void setUp(){
        mockMvc = MockMvcBuilders.webAppContextSetup(wac).build();
    }

    @Test
    @Commit
    public void createAccount1() throws Exception {
        AccountDto.Create createDto = new AccountDto.Create();
        createDto.setUsername("whiteship");
        createDto.setPassword("password");

        ResultActions result = mockMvc.perform(post("/accounts")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(createDto)));
        result.andDo(print());
        result.andExpect(status().isCreated());
        //TODO JSON Path
        //result.andExpect(jsonPath("$.username", is("whiteship")));
        System.out.println("!!!!!!!!!!!!!" + objectMapper.writeValueAsString(createDto));

    }

    @Test
    public void createAccount2() throws Exception {
        AccountDto.Create createDto = new AccountDto.Create();
        createDto.setUsername("whiteship");
        createDto.setPassword("password");
        ResultActions result = mockMvc.perform(post("/accounts")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(createDto)));
        result.andDo(print());
        result.andExpect(status().isBadRequest());
        //TODO JSON Path
        //result.andExpect(jsonPath("$.username", is("whiteship")));
        System.out.println("!!!!!!!!!!!!!" + objectMapper.writeValueAsString(createDto));
    }
}
```
두 Test가 순차적으로 수행되며, 첫 번째 테스트 createAccount1 (첫유저생성후 DB COMMIT)와 두 번째 테스트 createAccount2 (첫유저와 동일한 유저생성요청 - DB에 동일한 유저가 존재해서 실패예측)가 모두 성공한다.
