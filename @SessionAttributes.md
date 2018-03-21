## @SessionAttributes
1. 컨트롤러 메소드가 생성하는 모델 정보 중에서 @SessionAttributes에 지정한 이름과 동일한 이름이 있다면 이를 세션에 저장해준다.  
2. @ModelAttribute가 지정된 파라미터가 있을 때 이 파라미터에 전달해줄 동일이름의 오브젝트를 세션에서 가져온다. 
(@ModelAttribute로 지정된 동일이름의 파라미터가 세션에는 없다면, 에러 발생. 만약 @SessionAttributes가 컨트롤러에 선언되있는데, @ModelAttribute가 없거나, 있지만 동일이름은 없다면 에러는 발생하지 않음.)
