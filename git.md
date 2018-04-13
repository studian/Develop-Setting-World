깃에서 리모트에 있는 특정 브랜치를 바로 로컬로 클론하려고 한다.


해결책:

http://stackoverflow.com/questions/1911109/git-clone-a-specific-branch

git clone -b <branch> <remote_repo>

git clone -b my-branch git@github.com:user/myproject.git  
