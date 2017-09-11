# RequestBody
XML이나 JSON기반의 메시지를 사용하는 요청의 경우 사용.  
이 애노테이션이 붙은 파라미터에는 HTTP요청의 BODY가 그대로 전달된다  
```
public void message(@RequestBody String body){...}
```
```
    @RequestMapping(value = "/accounts", method = RequestMethod.POST)
    public ResponseEntity createAccount(@RequestBody @Valid AccountDto.Create create,
                                        BindingResult result){
        if(result.hasErrors()){
            return new ResponseEntity(HttpStatus.BAD_REQUEST);
        }
        Account newAccount = service.createAccount(create);
        return new ResponseEntity<>(modelMapper.map(newAccount, AccountDto.Response.class), HttpStatus.CREATED);
    }
```
