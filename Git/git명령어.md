
##### `git init`  -  git 생성하기     
   
##### `git clone git_path `  -  코드가져오기  
     
##### `git checkout branch_name `  -  브랜치 선택하기
   
##### `git checkout -t remote_path/branch_name `  -  원격 브랜치 선택하기  

##### `git branch branch_name` -  브랜치 생성하기     
   
##### `git branch -r`  -  원격 브랜치 목록보기  
    
##### `git branch -a`  -  로컬 브랜치 목록보기 
     
##### `git branch -m branch_name change_branch_name`  -   브랜치 이름 바꾸기     

##### `git branch -d branch_name`  -  브랜치 삭제하기     

##### `git rm file_name`  -  파일 삭제하기     
  
##### `git push remote_name — delete branch_name   ( git push origin — delete branch_name )` -  원격 브랜치 삭제하기   

##### `git add file_path   ( git add * )` -  수정한 코드 선택하기     
  
##### `git commit -m “commit_description”   ( git commit -m “내용”)` -  선택한 코드 설명 적기   

##### `git push romote_name branch_name   (git push origin master)` -  add하고 commit한 코드 git server에 보내기     
  
##### `git pull` -  git서버에서 최신 코드 받아와 merge 하기   

##### `git fetch` -  git서버에서 최신 코드 받아오기     

##### `git reset — hard HEAD^` -  commit한 이전 코드 취소하기     
  
##### `git reset — soft HEAD^` -  코드는 살리고 commit만 취소하기   

##### `git reset — merge` -  merge 취소하기     
   
##### `git reset — hard HEAD && git pull`  -  git 코드 강제로 모두 받아오기  

##### `git config — global user.name “user_name ”`  -  git 계정Name 변경하기     

##### `git config — global user.email “user_email”`  -  git 계정Mail변경하기     

##### `git stash / git stash save “description”`  -  작업코드 임시저장하고 브랜치 바꾸기     
  
##### `git stash pop`  -  마지막으로 임시저장한 작업코드 가져오기   
  
##### `git branch — set-upstream-to=remote_path/branch_name`  -  git pull no tracking info 에러해결   
     
         
***              
Git 처음 push 할때 설정해주어야하므로      
`git push --set-upstream origin (branch name)`     
을 해주어야한다

##### 후에 푸쉬하기전 커밋은 필수

SourceTree에서 깃 패스워드를 까먹거나 잘 되지 않을 시 C:\Users\[계정이름]\AppData\Local\Atlassian\SourceTree\ 에 passwd 파일을 삭제한 후 다시 접속하여 아이디와 패스워드를 입력한다.      

참고 : https://pks2974.medium.com/%EC%9E%90%EC%A3%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EA%B8%B0%EC%B4%88-git-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-533b3689db81
https://goddaehee.tistory.com/274
