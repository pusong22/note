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