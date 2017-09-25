# ResponseEntity 오브젝트  

ResponseEntity 오브젝트는  
1.HTTP Response BODY에 객체를 넘길 수 있다. (자동 json변환)  
2.HTTP Response HEADER를 설정할 수 있다.  
3.HTTP General HEADER에 statusCode를 설정해서 응답할 수 있다.  

ResponseEntity를 반환하는 것이면,   
그 내용을 HTTP응답에 삽입하는 것은 명확하므로, @ResponseBody를 설정할 필요가 없다.  
statusCode도 삽입을 해줄 수 있므로,@ResponseStatus를 설정할 필요 없다.  

@ResponseStatus를 사용하는 방법은, 응답의 상태가 고정이므로, 한 리퀘스트에 대해서 응답이 하나일 경우에만 사용한다. 예외처리 등..
