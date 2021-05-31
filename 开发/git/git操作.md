## 基本操作

```shell
git init	#初始化仓库
git status	#查看仓库的状态
git add 	#向暂存区中添加文件
git commit 	#保存仓库的历史记录		
	-m "First commit" 	#记述一行提交信息
git log 	#查看提交日志	
	--pretty=short		#只显示提交信息的第一行
	(文件名)			#只显示指定目录、文件的日志
	-p(文件名)		#显示文件的改动
git diff		#查看更改前后的差别（查看工作树和暂存区的差别）	
	HEAD		#查看工作树和最新提交的差别

```

## 分支的操作

```shell
git branch 		#显示分支一览表（*表示当前正在使用）
git checkout -b #创建、切换分支
git checkout -b feature-A		#切换到feature-A分支并进行提交
    #等同于
    git branch feature-A
    git checkout feature-A
git checkout master		#切换到master分支
git checkout - 			#切换回上一个分支
git merge				#合并分支
  	git merge --no-ff  feature-A	#为了在历史记录中明确记录下本次分支合并，我们需要创建合并提交
git log --graph			#以图表形式查看分支
```

##  更改提交的操作

```shell
git reset 	#回溯历史版本
	git reset --hard +(哈希值)		#回溯到指定时间
git reflog	#查看仓库执行过的操作的日志
git	commit --amend	#修改提交信息
git rebase -i 	#压缩历史
```

## 推送至远程仓库

```shell
git remote add 	#添加远程仓库
git push	#推送至远程仓库
	git push origin feature-A	#提交本地分支feature-A到远程(远程没有 feature-A 分支，并且本地已经切换到 feature-A分支)  远程新建名为 feature-A分支，并push代码
```

## 从远程仓库获取

```shell
git clone 	#获取远程仓库
git pull	#获取最新的远程仓库分支
```

