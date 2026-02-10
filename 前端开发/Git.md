# Git记录


### git 将提交记录合并在一条 commit 内
```
# master分支 合并 test分支
git merge --squash test
```

### git 创建分支并且提交和关联远程
```
# 切换分支
git checkout -b dev

# 提交远程分支
git push origin dev

# 关联远程分支
git push --set-upstream origin dev
```

### git 打tag
```
# 新建tag
git tag v1.0.0

# 推送远程
git push tag v1.0.0




```