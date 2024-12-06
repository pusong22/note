# git命令
## git init --bare
创建一个中央仓库，相当于一个远程仓库，用来进行代码管理

测试
```shell
#创建一个裸仓库，原先git init生成的.git目录的内容显示创建到test目录中
git init --bare test.git
#克隆到本地，c1目录中生成.git目录，可以进行正常提交代码等操作
git clone test.git c1
```

## git branch --track 和 git checkout --track
- git branch 
1. --track branch-name remote-branch-name: 创建本地分支，并且跟踪远程分支
2. --set-upstream-to remote-branch-name: 修改跟踪的远程分支
- git checkout
1. --track remote-branch-name: 创建与远程分支同名的本地分支，然后跟踪远程分支，并且切换到该分支
2. -b branch-name --track remote-branch-name: 创建给出的分支名称，然后跟踪远程分支，并且切换到该分支


## git prune
清理不必要的内容

## git gc
压缩文件

