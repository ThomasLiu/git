# rebase 工作模式

很多人在争论 到底是 merge 好 还是 rebase 好。

[git在工作中正确的使用方式----git rebase篇](https://blog.csdn.net/nrsc272420199/article/details/85555911)

个人见解各有各的好处，rebase 到一个统一的提交，好处是让提交历史简洁，但是坏处是如果发现其中某个提交是有问题，想单独拆出来处理，就比较复杂和麻烦。

虽然说各位大佬出现这些情况的机率不高，但是条条大路通罗马，自己团队去评估和决定吧。

所以关于 rebase 的推荐工作流程是：

``` bash
git checkout master
git pull
git checkout local
#切换到local分支后， 就是修改代码
#修改完了， 就正常提交代码-------git commit
#如果有多次local分支的提交，就合并，只有一次可以不合并
git rebase -i HEAD~2  //合并提交 --- 2表示合并两个
#将master内容合并到local
git rebase master
# 解决冲突后
git rebase --continue
#再起切换到master或其他目标分支
git checkout master
#将local合并到master
git merge local
#推送到远程仓库
git push
```
