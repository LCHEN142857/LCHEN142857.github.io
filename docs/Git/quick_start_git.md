# Quick Start Git  

- git clone  

- git fetch  

- git rebase  

- git status  

- git add  

- git diff  

- git commit  

- git push  

- oftenly work flow  

```git
# 个人分支更新代码推荐
git pull --rebase origin master
---
git add xx/xxx
git commit -m "xxxxx"
git checkout master
git pull
git checkout your_branch
git rebase origin/master
git push --set-upstream origin your_branch(first time)
# 修改之后合入上一次的提交
git add xxx/xxxx
git commit --amend --no-edit
git push -f
```
