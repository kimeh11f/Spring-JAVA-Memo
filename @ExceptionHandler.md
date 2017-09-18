# @ExceptionHandler

예외처리의 경우, 다른방식으로도 구현이 가능하지만...  
이 방법은 해당 컨트롤러에서 발생하는 특정 익셉션들에 대한 처리를 공통적으로 할 수 있어서, 리팩토링 효과가 있다.  
컨트롤러에에서 작업 중 발생한 익셉션을 직접처리할때에, @ExceptionHandler 애노테이션을 적용한 메서드를 구현한다.
```
AccountController.java
@RestController
public class AccountController {
........
    @ExceptionHandler(UserDuplicatedException.class) //직접생성한 예외클래스(RuntimeException)
    public ResponseEntity handleUserDuplicatedException(UserDuplicatedException e){
        ErrorResponse errorResponse = new ErrorResponse(); //직접생성한 에러처리용 객체.
        errorResponse.setMessage("["+e.getUsername() +"] 중복 username 입니다.");
        errorResponse.setCode("duplicated.username.exception");
        return new ResponseEntity<>(errorResponse, HttpStatus.BAD_REQUEST);
    }
}
```
