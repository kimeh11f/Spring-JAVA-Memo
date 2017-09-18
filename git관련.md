# .gitignore 파일 다시 적용하기  
#### (기존에 저장소에 있던 파일을 모두 삭제 후 재커밋. 이후 PUSH하면 원격 저장소에 있던 파일도 .gitignore파일을 기반으로 파일이 삭제 후 다시 올라감)
1. .git이 있는 디렉토리에서 cmd창을 실행
2. 다음명령어를 실행  
<code>git rm -r --cached .</code>  
<code>git add .</code>  
<code>git commit -m "gitignore 재적용"</code>

# IntelliJ에서 원격저장소에 있는 파일들을 로컬로 가져오는 법

VCS-> Checkout from version control -> GitHub  
Git Repository URL 선택 후, 디렉토리 선택 한 뒤, Clone버튼 클릭
