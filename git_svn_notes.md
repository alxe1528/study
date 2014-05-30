**Target SVN Repository url: https://localhost:8443/svn/test1**


**Tracking and contributing to the trunk of a Subversion-managed project (ignoring tags and branches):**

---

1. `Git`复制`Subversion`仓库
  - `git svn clone https://localhost:8443/svn/test1 [项目别名]`
  - 或者使用`Subversion`的某个版本号进行加速复制，则这个版本号之前的`log`信息在`Git`仓库中会丢失掉
    1. `git svn init https://localhost:8443/svn/test1 [项目别名]`
    2. `git svn fetch [-r 版本号:HEAD]` #如果使用了版本号
  - 在`clone`完成之后，可以执行`git gc`进行压缩磁盘空间

2. 拉取服务器上所有最新的改变，在此基础上衍合本地的修改
   ```
   git svn rebase
   ```

3. 如果既要向`Git`远程服务器推送内容，又要推送到`Subversion`远程服务器，则必须先向`Subversion`推送（`dcommit`），因为该操作会改变所提交的数据内容。
   ```
   git svn dcommit
   ```

4. 要在`Subversion`中建立一个新分支
   ```
   git svn branch [分支名]
   ```

5. `git svn`其它操作
   ```
   git svn show-ignore
   git svn log
   git svn info
   ```


**Tracking and contributing to an entire Subversion-managed project (complete with a trunk, tags and branches):**

---

1. `Git`复制`Subversion`仓库
   ```
   git svn clone https://localhost:8443/svn/test1 -s --prefix=mytest1/
     --prefix 用于设置在.git/refs/remotes下保存引用时的的前缀
     -s 即标准的版本库，trun/branches/tags会以git的分支展示（使用git checkout切换），而不是svn中看到的三个目录
   测试下来是不支持git svn fetch加版本号复制
   ```

2. `git config -l` 查看`svn url`信息
   ```
   svn-remote.svn.url=https://localhost:8443/svn/test1
   svn-remote.svn.fetch=trunk:refs/remotes/mytest1/trunk
   svn-remote.svn.branches=branches/*:refs/remotes/mytest1/
   svn-remote.svn.tags=tags/*:refs/remotes/mytest1/tags/*
   ```

3. 查看分支上`svn url`信息
   ```
   git svn info
   ```

4. 查看`remote`上所有`branch`信息
   ```
   $ git branch -r
     mytest1/trunk
     mytest1/v1.1
   ```

5. 基于`master`分支也就是`svn trunk`创建分支
  - `git checkout -a b1`
  - 然后在`b1`分支上可以直接使用`git svn rebase`更新和`git svn dcommit`进行提交
  - 这个时候再去`master`上使用`git svn rebase`可以直接获取到刚才在分支`b1`上修改的内容，
  - 感觉不应该在`git`分支上直接使用`git svn rebase`和`git svn dcommit`上操作，否则分支也就没有多大意义了。
  - 也可以先在`b1`分支上修改完，接着`merge`回`master`，然后在`master`上做`git svn`操作，这样就比较符合`git`思想了。

6. 直接`git checkout mytest1/v1.1`
  - 同样也可以直接使用`git svn rebase`更新和`git svn dcommit`进行提交，但会使分支处于`Detached`状态，
  - `commit`之后，切换到`master`后刚才游离分支就没有了。
  - 直接从`svn branch`分支`checkout`为`git`分支，还不知道这怎么操作，貌似好像不支持。


**总而言之，此方式还是慎用吧，本来`git`和`svn`设计上就有很大区别，硬是用`git`的思想去套`svn`，难免会有各种别扭。**