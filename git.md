# 把其他分支的commit合并到当前分支
用到的命令：`cherry-pick`
```shell
git cherry-pick commit_id_1 commit_id_2 commit_id_3
```
`cherry-pick`可以一次性选择多个commit，并且这些commit可以分布在不同分支，因为commit id在哪个分支都不会重复，所以不用指定分支名称

## 区间操作
如果是要从一个分支选取连续的多个commit，可以用`..`连接开头commit和结尾commit
```shell
git cherry-pick commit_id_1..commit_id_4
```