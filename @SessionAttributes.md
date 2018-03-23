## @SessionAttributes
1. 컨트롤러 메소드가 생성하는 모델 정보 중에서 @SessionAttributes에 지정한 이름과 동일한 이름의 모델이 있다면 이를 세션에 저장해준다.  
2. 컨트롤러의 메소드의 매개변수에 @ModelAttribute 설정이 있으면, 세션에 해당 이름으로 저장된 데이터가 있는지 확인하고, 있다면, 해당객체를 세션에서 가져와서 매개변수로 선언된 변수에 할당한다.
(실행된 컨트롤러에 @SessionAttributes가 있고 메소드에 @ModelAttribute로 지정된 동일이름의 매개변수가 있는데, @ModelAttribute로 선언된 이름의 attribute가 정작 세션에는 없다면, - not found in session 에러 발생. 만약 @SessionAttributes가 컨트롤러에 선언되있는데, 실행된 메소드의 매개변수에 @ModelAttribute 없거나, 있지만 동일이름으로 선언되지 않았다면 에러는 발생하지 않음.)

### 사용 이유
기존의 값을 불러서 update 등 DB처리를 할 때, 우선 불러온 값들을 세션에 저장해놓고, update시에는 세션에 있었던 값 전체를 모델에 할당후, 사용자가 update 할 부분들만 모델에 추가로 set하여, null 업데이트를 방지할 수 있다.
