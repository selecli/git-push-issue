解决 github push failed (remote: Permission to userA/repo.git denied to userB.)

【前言】当你看到这篇文章时，很高兴，你不用再去各大网站再去搜索这个问题的解决方案了，因为这篇文章可以帮你彻底解决问题。请耐心地阅读完。

本文假设了两个用户 userA 和 userB ，userA的github项目名为 repo

当你在使用Android Studio push项目的时候，你遇到了这个问题：

Push failed: Failed with error: fatal: unable to access 'https://github.com/userA/repo.git/': The requested URL returned error: 403
1
报了403，说明访问被拒绝。 
切换到终端（Terminal），使用命令 git push -u origin master 后，错误就更明显了：

remote: Permission to userA/repo.git denied to userB.
fatal: unable to access 'https://github.com/userA/repo.git/': The requested URL returned error: 403
1
2
意思很明白，userB没有权限对userA的repo进行push更改。 
这时你已经使用了如下命令去配置全局用户：

git config --global user.name userA
git config --global user.email userA@Email.com
1
2
并且很明确当前用户已经是userA，但还是说userB没权限。。

什么原因？ 
由于该电脑使用git bash配过SSH，系统已经将指向github.com的用户设置为了userB，每次push操作的时候，都将读取到userB的用户信息，类似于记住密码。

如何解决？ 
1、对userA生成SSH公钥，添加到userB的github后台； 
2、将userB添加为userA项目的contributer； 
3、移除计算机中的userB。

对于1和2，相信很多人不想这么做，因为一旦使用了SSH，以后的所有clone、pull、push等操作都将使用SSH传输，对以往使用过https传输的项目也得重新更改传输方式，这样会浪费一些时间。

现在详细讲下3，操作很简单：

打开 控制面板–>用户–>证书管理–>系统证书


展开 git:https://github.com 并删除之。
--------------------- 
作者：神话2009 
来源：CSDN 
原文：https://blog.csdn.net/klxh2009/article/details/76019742 
版权声明：本文为博主原创文章，转载请附上博文链接！
