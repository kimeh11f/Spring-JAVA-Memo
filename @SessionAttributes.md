## @SessionAttributes
1. 컨트롤러 메소드가 생성하는 모델 정보 중에서 @SessionAttributes에 지정한 이름과 동일한 이름이 있다면 이를 세션에 저장해준다.  
2. @ModelAttribute가 지정된 파라미터가 있을 때 이 파라미터에 전달해줄 동일이름의 오브젝트를 세션에서 가져온다. 그리고 해당 커맨드객체에 값을 넣어준다.
(@ModelAttribute로 지정된 동일이름의 파라미터가 세션에는 없다면, 에러 발생. 만약 @SessionAttributes가 컨트롤러에 선언되있는데, @ModelAttribute가 없거나, 있지만 동일이름은 없다면 에러는 발생하지 않음.)

### 사용 이유
기존의 값을 불러서 update 등 DB처리를 할 때, 우선 불러온 값들을 세션에 저장해놓고, update시에는 세션에 있었던 값 전체를 모델에 불러와서, 사용자가 update 할 부분들만 모델에 추가로 set하여, null 업데이트를 방지할 수 있다.
