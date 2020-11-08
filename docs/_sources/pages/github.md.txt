.. sectnum::
   :start: 8

##################################
学习GitHub操作
##################################

什么是 Github?
===================
Github是一个基于git的代码托管平台，简单的说，就是负责托管用户的项目代码。Github按照组织划分，分为：企业和个人，IBMer访问的企业Github地址为：https://github.ibm.com/，个人访问的地址是：https://github.com/


便于新手学员快速掌握GitHub，熟悉GitHub操作的相关概念，我们把操作Github同操作微信进行对比：

.. list-table:: Github的操作 VS 微信的操作
   :widths: 5 10 10

   * - 操作步骤
     - 微信
     - Github
   * - | 下载客户端
     - | 下载微信客户端
       | 不同的设备，下载不同的版本
       | 即使同一个设备，有在线版的和安装版的
     - | 下载Github客户端
       | 不同的设备，下载不同的版本
       | 有图形界面的，也有命令行的(推荐)
   * - | 注册与登录
     - | 登录微信
       | 1、第一次肯定需要注册，注册的目的是需要有一个登录的账号
       | 2、对于微信，后续如果不换手机的话，不需要再输入密码了
       | 3、换了手机登录，需要再次输入密码
     - | 登录Github
       | 1、第一次肯定需要注册，注册的目的是需要有一个登录的账号
       | 2、对于Github，采用SSH的方式，在Github上配置好用户机
       |    器的密钥，这样以后不换机器的话，也就不需要输入密码了
       | 3、换了机器，登录时需要再次输入密码
   * - | 准备好素材
     - | 1、发朋友圈的图片和短视频事先是保存在手机里面的
       | 2、在手机里面编辑好素材
       | 3、发朋友圈时，图片或视频来自手机，支持在线文字编辑
     - | 1、初始化本地Github仓库
       | 2、本地必须准备好代码
       | 3、本地和Github仓库建立关联，Github页面上支持在线编辑
   * - | 准备发朋友圈
     - | 1、朋友圈界面选择手机里面的素材及编辑文字
       | 2、发朋友圈时，可以设置朋友的访问权限
       | 3、发朋友圈的过程就是本地编辑的内容提交到微信远程服务器
     - | 1、建立本地代码与Github仓库的关联
       | 2、git clone 命令就是建立好关联
       | 3、git commit 命令就是拟准备发送代码
   * - | 提交发送朋友圈
     - | 1、点击发布，本地的素材就发布到远程的朋友圈了
       | 2、一旦发布后，可以删除朋友圈
       | 3、微信好友只能看你的圈，可以留言，但是不能编辑
     - | 1、使用git push 命令提交本地代码到Github仓库
       | 2、可以设置仓库的权限，设置哪些人可以查看和提交代码
       | 3、获得权限的人，可以对你的仓库进行对应的操作


准备好Github环境
======================================
按照上述的讲解，Github环境分为2块，一是服务端必须有Github仓库，另一个就是本地的代码需要与仓库建立关联关系，请按照下面的步骤进行：

创建Github仓库
*******************

#. 如果没有Github账号，需要注册一个账号，IBMer默认的账号名是w3的账号，因此IBMer不需要再注册账号了；
#. 创建Github仓库。这点直接在Github页面上操作；参考这里：`创建Github仓库 <https://help.github.com/cn/enterprise/2.20/user/github/getting-started-with-github/create-a-repo>`_


下载本地Github客户端
*******************************
我们需要一个客户端，它负责本地代码与远程Github仓库之间的交互，比如：下载远程仓库的代码，提交代码等。客户端工具推荐选择命令行的界面。
关于安装客户端，请参考这里：`安装Github客户端 <https://help.github.com/cn/enterprise/2.20/user/github/getting-started-with-github/set-up-git#setting-up-git>`_


使用 SSH URL 克隆
*******************************
我们需要使用 SSH 连接到 GitHub，使用SSH的目的是，让Github永远记住用户的机器和身份，以后在这台机器上使用Github客户端命令时，无需输入账号和密码。
关于如何配置SSH，请参考这里：`SSH 连接到 GitHub <https://help.github.com/cn/enterprise/2.20/user/github/authenticating-to-github/connecting-to-github-with-ssh>`_


配置完成后，使用下面的命令进行检测::

    $ ssh -T git@github.ibm.com
    Hi username! You've successfully authenticated, but GitHub does not provide shell access.

如果出现类似上述的信息，表示配置成功。

使用Github客户端命令
======================================
下面例举了日常工作中的常见操作场景，针对每种场景，使用对应的Github客户端命令。

如何从Github仓库中下载代码
*******************************
#. 找到远程Github仓库的SSH URL地址；
#. 本地打开Github客户端的命令行，输入下面的命令：

 .. code-block:: sh
   :linenos:

   git clone SSH地址 # 如：git clone git@github.ibm.com:lanzejun/h5-course.git

执行上述命令后，以上述命令中的注释命令为例，将会在当前文件夹下创建一个名为“h5-course”的文件夹。

如何更新本地代码
*******************************
本地打开Github客户端的命令行，输入下面的命令：

 .. code-block:: sh
   :linenos:

   git pull

这个命令需要经常使用，如编辑代码前，提交代码前等。该命令负责同步远程仓库，更新本地的代码。相当于刷新微信朋友圈。

如何提交本地代码
*******************************
本地代码编辑好后，需要提交代码了，具体操作步骤如下：

 .. code-block:: sh
   :linenos:

   git pull  # 提交前，更新下本地代码，看看是否有冲突
   git status # 查看改动的代码，凡是有改动的（编辑、增加、删除等），都标记为红色显示
   git add 文件名 # 文件名来自上面的步骤，文件名可以空格分开，也可以多次执行这个命令
   git commit -m '引号包围的信息' # 提交的信息一定要引号包围
   git status # 再次确认提交的代码，凡是有改动的，都标记为绿色显示
   git push # 提交代码

如何撤销本地操作
*******************************
由于各种原因，如，提交前代码时发生了冲突，改错了代码，后悔莫及的操作等，用下面的命令可以让你本地的所有的操作全部撤销，相当于回到初始 ``git clone`` 的状态。

 .. code-block:: sh
   :linenos:

   git checkout . # 撤销全部的改动，注意命令后面的点（.）
   git checkout 文件名 # 撤销某一个文件的改动，后面是具体文件的路径



.. admonition:: 注意
    
    所有的Github常用操作命令是在项目的 ``根目录下`` 执行。


多数读者使用Github的时，遇到的问题，都是卡在了最后一步（git push），可能的原因有如下几种：

#. 遇到了网络异常，如：超时错误；
#. 遇到了权限问题，这个需要联系Github仓库的创建者，让其帮忙添加权限；
#. 发生了代码冲突。
#. 其他

下面介绍发生上面场景时的解决方法。

Github常见问题解决方案
===========================
工作中，难免遇到各种各样的问题，下面例举了一些日常的案例，供参考。

发生代码冲突时如何解决
******************************************
发生代码冲突时的场景有很多，具体的来讲，就是有人和你一起修改了同一行文件（注意，如果是同一个文件里面的不同行，不会出现代码冲突）。因此，需要养成git pull的习惯，不是说，每时每刻都需要做，至少在，编辑代码前，提交代码时必须要做的。一旦发生代码冲突了，有很多解决方法，这里推荐一种以不变应万变的方法：

#. 记住和备份好你本地的修改；
#. 撤销本地的所有操作或者冲突文件的操作；
#. 重新编辑代码，提交。

SSH连接超时错误时如何解决
******************************************
有时候，经常遇到这样的错误：
ssh: connect to host github.com port 22: Connection timed out ，发生这个错误的根本原因是“不可描述原因”，解决途径就是需要换个IP地址，常见的做法有两种：

#. 切换网络到你手机的热点
#. 重启你家里的猫。注意，不是路由器。设备猫是电信、移动等运营商牵线到用户家里的第一个设备，一般装修时放在进门处的，不熟悉的，建议打电话咨询对应的移动业务运营商。


提交时，遇到pre-receive hook declined错误
*********************************************
该问题是服务端的问题，需要仓库的管理员解决。问题表现如下：

 .. code-block:: sh
   :linenos:

    $ git push
    Counting objects: 4, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 325 bytes | 325.00 KiB/s, done.
    Total 4 (delta 2), reused 0 (delta 0)
    remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
    To github.ibm.com:lanzejun/h5-course.git
    ! [remote rejected] master -> master (pre-receive hook declined)
    error: failed to push some refs to 'git@github.ibm.com:lanzejun/h5-course.git'

上述错误，导致使用该仓库的参与者（包含仓库的作者）不能修改文件了，比如尝试在线修改文件，发生如图所示的错误：

 .. image:: ./images/github-issue1.png
   :width: 440px


按照github官方文档的描述：`Working with pre-receive hooks <https://help.github.com/en/enterprise/2.20/user/github/collaborating-with-issues-and-pull-requests/working-with-pre-receive-hooks>`_ ，笔者在github上找不到如何删除pre-receive hooks，截图如下：

 .. image:: ./images/github-issue2.png
   :width: 800px

过了5小时后，该仓库莫名其妙的自己修复了。下面是操作的示例：

 .. code-block:: sh
   :linenos:

    $ git push
    Counting objects: 3, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 326 bytes | 326.00 KiB/s, done.
    Total 3 (delta 1), reused 0 (delta 0)
    remote: Resolving deltas: 100% (1/1), completed with 1 local object.
    remote: detect-secrets-stream (beta) ver=164-1ac7e673b9acf31ed1ba86a8422cf59cb8a848be
     FAQ: https://ibm.biz/detect-secrets-stream-faq
    remote: 
    remote: Successfully send push metadata.
    remote: Push info collect pre-receive hook finished within 3 seconds.
    To github.ibm.com:lanzejun/h5-course.git
      a972bf4..c539695  master -> master

综上所述，基本上断定，上述问题是github.ibm.com服务器那边的程序造成的，解决思路只能依靠服务器那边的设置。同时在这个故障发生期间，笔者发现，在github上的图像也被莫名其妙的替换成方块人了，等待故障解决后，图像又还原了。


部署Angular应用到GitHub页面服务器
=======================================
GitHub页面（GitHub Pages）服务是一个静态站点的服务托管平台，它直接从 GitHub 上的仓库获取 HTML、CSS 和 JavaScript 文件，在构建过程中通过静态站点生成器发布静态应用。GitHub页面服务作为一个免费的服务平台，它只支持静态网站(HTML, CSS, JavaScript)，没有服务端，所以不支持服务端的语言(不支持Java，PHP，Python)。针对学习用户，发布 Angular 应用到GitHub页面服务器，是非常不错的选择。下面，我们介绍两种方式如何将Angular的应用部署到GitHub页面服务上。

手工发布到GitHub页面服务器
*****************************
手工发布应用到GitHub页面服务器的方式，同样适合非Angular工程，换句话说，这种方法支持所有的静态资源站点。
下面步骤是指导用户手工发布Angular应用到GitHub页面服务上。

1. 需要创建一个 GitHub 账号，然后为项目创建一个仓库。记下 GitHub 中的用户名（user_name）和仓库名（repository_name）；
2. 克隆仓库到本地，在根目录下创建Angular工程；
3. 使用 Angular CLI 命令 ng build 来构建这个 GitHub 项目，命令如下：

 .. code-block:: sh

   ng build --prod --output-path docs --base-href=/user_name/repository_name/  # 注意base-href值的前后有个"/"(斜杠)

4. 当构建完成后，复制一份 docs/index.html 文件，命令为 docs/404.html。注意：index.html和404.html文件内容相同，在同一目录下；
5. 提交代码到GitHub仓库；
6. 进入GitHub项目的Setting页中，把该项目配置为从 docs 目录下发布。

完成上述步骤后，可以通过URL https://pages.github.com/user_name/repository_name/ 中查看部署好的页面。

.. admonition:: 注意

  把上述步骤中出现的的user_name和repository_name替换为实际的用户名和仓库名。如果使用的是企业github，请将github.com替换成企业地址。

自动发布到GitHub页面服务
***********************************************
Angular CLI命令为市面上流行的平台提供了对应的脚手架命令，用来发布发布Angular工程到其平台上，这些平台包括Azure、GitHub Pages和NPM等。其中angular-cli-ghpages命令用于发布Angular工程到GitHub页面服务上，angular-cli-ghpages命令的使用步骤如下：

1. 同手工发布类似，也是需要一个 GitHub 账号，然后为项目创建一个仓库。记下 GitHub 中的用户名（user_name）和仓库名（repository_name）；
2. 克隆仓库到本地，在根目录下创建Angular工程；
3. 安装GitHub页面服务提供的脚手架命令，命令如下：

 .. code-block:: sh

  ng add angular-cli-ghpages

4. 使用 ng deploy 命令来构建这个 GitHub 项目，命令如下：

 .. code-block:: sh

   ng deploy --base-href=/repository_name/ # 注意repository_name前后有个"/"(斜杠)
  
5. 提交代码到GitHub仓库。
   
完成上述步骤后，可以通过URL https://user_name.github.io/repository_name/ 中查看部署好的页面。

.. admonition:: 注意

  把上述步骤中出现的的user_name和repository_name替换为实际的用户名和仓库名。