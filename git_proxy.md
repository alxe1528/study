## Windows

- msysGit中提供了`connect`命令，在`~/.ssh/config`文件中添加如下配置，就能支持`git://`的`clone/pull/push`操作了
<pre>
 ProxyCommand connect -H 130.147.222.32:808 %h %p
 Host github.com
 User git
 Port 22
 Hostname github.com
 IdentityFile ~/.ssh/id_rsa
 TCPKeepAlive yes
 IdentitiesOnly yes

 ProxyCommand connect -H 130.147.222.32:808 %h %p
 Host ssh.github.com
 User git
 Port 443
 Hostname ssh.github.com
 IdentityFile ~/.ssh/id_rsa
 TCPKeepAlive yes
 IdentitiesOnly yes
</pre>
