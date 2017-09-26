### HTTP Request
- Request Line : 
  - HTTP메서드 방식 및 요청 URL과 프로토콜 정보  
  ```
  [HTTP METHOD(POST)] [URL(/--/--)] [PROTOCOL/VERSIONH (HTTP/1.1)]  
  ```  
- Request Header : 
  - 웹브라우저정보, 언어, 인코딩 방식, 요청 서버 정보 등과 같은 추가 정보  
  ```
  [USER-AGENT : MOZILLA/4.0] [CONTENT-TYPE : APPLICATION/X-WWW-FORM-RLENCODED] [ACCEPT-LANGUAGE : KO] ...  
  ```  
- Request Body  
  - 요청에 필요한 내용. 일반적으로 HTML 폼 태그 안에 입력된 값들인 파라미터 정보를 의미  


### HTTP Response  
- Status Line : 
  - 응답상태코드 및 프로토콜 정보를 갖는다.  주요상태코드 (200:OK, 404:NOT FOUND, 500:Internal Server Error]
  ```
  [PROTOCOL/VERSION (HTTP/1.1)] [상태코드(200)] [설명(OK)]  
  ```
- Response Header : 
  - 응답처리 날짜, 인코딩 방식, 요청 서버 정보 등과 같은 추가정보를 갖는다.  
  ```
  [CONTENT-TYPE : TEXT/HTML] [DATE : MON, 27, FEB 2006] [SERVER: APACHE-COYOTE/1.1] ...  
  ```
- Response Body : 
  - 응답에 필요한 내용을 갖는다. 일반적으로 HTML 문서이다.  
  ```html
  <HTML><HEAD><TITLE></TITLE></HEAD><BODY></BODY></HTML>
  ```
 
# HTTP 메시지 구조
- 메시지 헤더
- 개행 문자(CR+LF)
- 메시지 바디

# HTTP 헤더 필드 종류
- 일반적 헤더 필드(General Header Fields) : 리퀘스트 메시지와 리스폰스 메시지 둘 다 사용되는 헤더
- 리퀘스트 헤더 필드(Request Header Fields) : 리퀘스트의 부가적 정보와 클라이언트 정보, 리스폰스의 콘텐츠에 관한 우선 순위 등을 부가
- 리스폰스 헤더 필드(Response Header Fields) : 리스폰스의 정보와 서버의 정보, 클라이언트의 추가 정보 요구 등을 부가
- 엔티티 헤더필드(Entity Header Fields) : 리퀘스트 메시지와 리스폰스 메시지에 포함된 엔티티에 사용되는 헤더. 콘텐츠갱신 시간 등의 엔티티에 관한 정보 부가
