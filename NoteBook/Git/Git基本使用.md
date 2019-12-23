# Git基本使用
1. 在win10操作系统中，系统默认安装了openSSH组件，故无需再次安装openSSH；
2. 首先需要安装Git，可以到其官方网站下载git的适用于windows的安装程序；
3. 初始化git仓库 ```git init```
4. 在Gitee（码云）或GitHub上创建空的仓库，Gitee可支持创建免费的不超过5人团队的私有仓库，而GitHub仅能创建开源库，私有库需要收费；
5. 注册Gitee帐号后需要首先将当前计算机的sshkey添加到信任清单，生成方式```ssh-keygen -t rsa -C "njustmxn@163.com"```
6. 本地仓库与远程仓库进行关联```git remote add origin git@gitee.com:njustmxn/JV```
7. 关联之后就可以创建本地与远程的分布式版本控制系统了；
8. 推送本地仓库文件```git push -u origin master```
9. 拉取远程仓库```git pull origin master```
10. 当pull或push时提示```fatal: refusing to merge unrelated histories```，说明本地库与远程库无关，此时需要强行关联，增加参数项```--allow-unrelated-histories```即可，即
```
git pull origin master --allow-unrelated-histories
```
或
```
git push -u origin master --allow-unrelated-histories
```

## 常用命令
添加文件：
```
git add ***.***/dir
```
提交当前版本
```
git commit -m "blablabla"
```
查看状态
```
git status
```
查看异同
```
git diff
```
克隆远程库
```
git clone ******地址*******
```
查看远程仓库
```
git remote -v
```
修改远程仓库在本地的简称
```
git remote rename
```

