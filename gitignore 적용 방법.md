# .gitignore 파일 다시 적용하기  
### (기존에 저장소에 있던 파일을 모두 삭제 후 재커밋)
1. .git이 있는 디렉토리에서 cmd창을 실행
2. 다음명령어를 실행  
<code>git rm -r --cached .</code>  
<code>git add .</code>  
<code>git commit -m "gitignore 재적용"</code>
