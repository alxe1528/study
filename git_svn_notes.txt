Target SVN Repository url: https://localhost:8443/svn/test1


1）、Tracking and contributing to the trunk of a Subversion-managed project (ignoring tags and branches):

1、git复制svn仓库
git svn clone https://localhost:8443/svn/test1 [项目别名]
或者使用某个版本号进行加速复制，不是必须的
git svn init https://localhost:8443/svn/test1 [项目别名]
git svn fetch [-r 版本号:HEAD] #如果使用了版本号，则之前的log信息在git中是看不到的。

如果目标SVN仓库文件太大，在clone完成之后执行git gc进行压缩磁盘空间。

2、拉取服务器上所有最新的改变，在此基础上衍合你的修改
git svn rebase

3、如果既要向 Git 远程服务器推送内容，又要推送到 Subversion 远程服务器，
则必须先向 Subversion 推送（dcommit），因为该操作会改变所提交的数据内容。
git svn dcommit

4、要在 Subversion 中建立一个新分支，需要运行 git svn branch [分支名]

git svn show-ignore
git svn log
git svn info



2）、Tracking and contributing to an entire Subversion-managed project (complete with a trunk, tags and branches):

git svn clone https://localhost:8443/svn/test1 -s --prefix=mytest1/
  --prefix 用于设置在.git/refs/remotes下保存引用时的的前缀
  -s 即标准的版本库，trun/branches/tags会以git的分支展示（使用git checkout切换），而不是svn中看到的三个目录
测试下来是不支持git svn fetch加版本号复制

git config -l
其中有三条svn url信息生成
svn-remote.svn.url=https://localhost:8443/svn/test1
svn-remote.svn.fetch=trunk:refs/remotes/mytest1/trunk
svn-remote.svn.branches=branches/*:refs/remotes/mytest1/
svn-remote.svn.tags=tags/*:refs/remotes/mytest1/tags/*

查看分支上svn url信息
git svn info

查看remote上所有branch信息
$ git branch -r
  mytest1/trunk
  mytest1/v1.1

查看分支信息
$ git branch
  b1
  master

1、如果基于master也就是svn trunk创建分支
git checkout -a b1
然后在b1分支上可以直接使用git svn rebase更新和git svn dcommit进行提交
这个时候再去master上使用git svn rebase可以直接获取到刚才在分支b1上修改的内容，
感觉不能在git分支上直接使用git svn rebase和git svn dcommit上操作，否则分支也就没有多大意义了。

也可以先在b1分支上修改完，在merge回master，然后在master上做git svn操作，这样就比较符合git思想了。

2、直接git checkout mytest1/v1.1
同样也可以直接使用git svn rebase更新和git svn dcommit进行提交，但会使分支处于Detached状态，
commit之后，切换到master后刚才游离分支就没有了。

直接从svn branch分支成checkout为git分支，还不知道这怎么操作，貌似好像不支持。


总而言之，此方式还是慎用吧，本来git和svn设计上就有很大区别，硬是用git的思想去套svn，难免会有各种别扭。


