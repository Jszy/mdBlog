git commit 提交时候，配置信息与push时候不匹配，需要修改的话，运行下面命令  
注意把 old name和new name new email修改成相应的真实数据 
```
git filter-branch --commit-filter '  
        if [ "$GIT_COMMITTER_NAME" = "<Old Name>" ];  
        then  
                GIT_COMMITTER_NAME="<New Name>";  
                GIT_AUTHOR_NAME="<New Name>";  
                GIT_COMMITTER_EMAIL="<New Email>";  
                GIT_AUTHOR_EMAIL="<New Email>";  
                git commit-tree "$@";  
        else  
                git commit-tree "$@";  
        fi' HEAD 
```
