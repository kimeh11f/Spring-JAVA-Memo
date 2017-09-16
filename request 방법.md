# Request 방법

예를들어, url에
```
http://localhost:8080/account?id=1234&username=홍길동
```
이런식으로 넘겨주면, 해당 파라미터 정보를 그대로 JSON으로 응답해주는 API가 있다고 가정한다.  
```
{"id":1234,"username":"홍길동","password":null,"email":null,"fullName":null,"joined":null,"updated":null}
```

1. HttpServletRequest 매개변수로 사용
```
    @RequestMapping("/account")
    public Account account(HttpServletRequest httpServletRequest){
        Account account = new Account();
        account.setId(Long.parseLong(httpServletRequest.getParameter("id")));
        account.setUsername(httpServletRequest.getParameter("username"));
        return account;
    }
```
위 방법은, getParameter에 해당하는 인자가 URL 파라미터에 존재하지 않아도, Exception은 발생하지 않는다.

2. @RequestParam 애노테이션을 매개변수에 사용 
```
    @RequestMapping("/account")
    public Account account(@RequestParam("id") long id, @RequestParam("username") String username){
        Account account = new Account();
        account.setId(id);
        account.setUsername(username);
        return account;
    }
```
위 방법은, @RequestParam애노테이션이 붙은 것을 필수 파라미터라고 인식한다.  
해당 파라미터가 없다면, Exception이 발생한다.(400에러코드. BAD_REQUEST)  
@RequestParam(value="username", required=false)로, 필수가 아님 체크를 해주면, 해당 파라미터를 null로 세팅한다.  
(기본적으로 required는 true로 되어있다.)  
다만, null을 세팅할 수 없는 int 등의 기본타입의 경우 Exception이 발생하기 때문에,  
해당 값들은 클래스 인스턴스 변수와 매개변수를 Wrapper클래스를 사용하여 null이 가능하게 해줄 수도 있고,  
required=false 대신 defaultValue="0"로 기본값 세팅하는 방법을 사용할 수 있다.  
@RequestParam이 적용된 파라미터가 String 타입이 아닐 경우, 그에 맞 형변환을 해준다.  

3. 객체를 그대로 매개변수로 사용 
```
    @RequestMapping("/account")
    public Account account(Account account){
        return account;
    }
```
위 방법은, 미리 생성된 Account라는 클래스의 인스턴스 변수들이 URL의 파라미터로 넘어온다는 가정하에 진행된다.  
받아올 파라미터와 set메소드가 일치할때 매핑이되며, 파라미터들을 개별적으로 매핑시키기 위한 작업이 필요없다.  
이 때 Account를 커맨드 객체라고 한다.
