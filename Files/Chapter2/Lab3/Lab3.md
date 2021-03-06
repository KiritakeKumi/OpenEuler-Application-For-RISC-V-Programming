# RISC-V下的Git练习

## 相关知识

### 版本控制
版本控制是一种记录若干文件内容变化，以便将来查阅特定版本修订情况的系统。你可以对任何类型的文件进行版本控制。如果你是位图形或网页设计师，可能会需要保存某一幅图片或页面布局文件的所有修订版本（这或许是你非常渴望拥有的功能）。采用版本控制系统（VCS）是个明智的选择。有了它你就可以将某个文件回溯到之前的状态，甚至将整个项目都回退到过去某个时间点的状态。你可以比较文件的变化细节，查出最后是谁修改了哪个地方，从而导致出现怪异问题，又是谁在何时报告了某个功能缺陷等等。使用版本控制系统通常还意味着，就算你乱来一气把整个项目中的文件改的改删的删，你也照样可以轻松恢复到原先的样子。但额外增加的工作量却微乎其微。

### 版本控制系统的分类
1.本地版本控制系统
许多人习惯用复制整个项目目录的方式来保存不同的版本，或许还会改名加上备份时间以示区别。这么做唯一的好处就是简单。不过坏处也不少：有时候会混淆所在的工作目录，一旦弄错文件丢了数据就没法撤销恢复。
为了解决这个问题，人们很久以前就开发了许多种本地版本控制系统，大多都是采用某种简单的数据库来记录文件的历次更新差异，其中最流行的一种叫做 rcs，现今许多计算机系统上都还看得到它的踪影。甚至在流行的 Mac OS X 系统上安装了开发者工具包之后，也可以使用 rcs 命令。它的工作原理基本上就是保存并管理文件补丁（patch）。文件补丁是一种特定格式的文本文件，记录着对应文件修订前后的内容变化。所以，根据每次修订后的补丁，rcs 可以通过不断打补丁，计算出各个版本的文件内容。
2.集中化的版本控制系统
集中化的版本控制系统诸如 CVS，Subversion 以及 Perforce 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。多年以来，这已成为版本控制系统的标准做法。

这种做法带来了许多好处，特别是相较于老式的本地 VCS 来说。现在，每个人都可以在一定程度上看到项目中的其他人正在做些什么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个 CVCS 要远比在各个客户端上维护本地数据库来得轻松容易。
事分两面，有好有坏。这么做最显而易见的缺点是中央服务器的单点故障。如果宕机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作。要是中央服务器的磁盘发生故障，碰巧没做备份，或者备份不够及时，就还是会有丢失数据的风险。最坏的情况是彻底丢失整个项目的所有历史更改记录，而被客户端提取出来的某些快照数据除外，但这样的话依然是个问题，你不能保证所有的数据都已经有人事先完整提取出来过。本地版本控制系统也存在类似问题，只要整个项目的历史记录被保存在单一位置，就有丢失所有历史更新记录的风险。

#### 分布式版本控制系统
在分布式版本控制系统（ Distributed Version Control System，简称 DVCS ）中，像 Git，Mercurial，Bazaar 以及 Darcs 等，客户端并不只提取最新版本的文件快照，而是把原始的代码仓库完整地镜像下来。这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。因为每一次的提取操作，实际上都是一次对代码仓库的完整备份。更进一步，许多这类系统都可以指定和若干不同的远端代码仓库进行交互。籍此，你就可以在同一个项目中，分别和不同工作小组的人相互协作。你可以根据需要设定不同的协作流程，比如层次模型式的工作流，而这在以前的集中式系统中是无法实现的。

### Git及常用命令
http://git-scm.com/doc
http://honghao460886.iteye.com/blog/1392035
http://www.bootcss.com/p/git-guide/

### SVN（摘自百度百科）
SVN是Subversion的简称，是一个开放源代码的版本控制系统，相较于RCS、CVS，它采用了分支管理系统，它的设计目标就是取代CVS。svn服务器有2种运行方式：独立服务器和借助apache运行。两种方式各有利弊，用户可以自行选择。
SVN使用模式举例。
1、从服务器下载项目组最新代码。
2、进入自己的分支，进行工作，每隔一个小时向服务器自己的分支提交一次代码（很多人都有这个习惯。因为有时候自己对代码改来改去，最后又想还原到前一个小时的版本，或者看看前一个小时自己修改了哪些代码，就需要这样做了）。
3、下班时间快到了，把自己的分支合并到服务器主分支上，一天的工作完成，并反映给服务器。
SVN的优缺点。
优点
1、管理方便，逻辑明确，符合一般人思维习惯。
2、易于管理，集中式服务器更能保证安全性。
3、代码一致性非常高。
4、适合开发人数不多的项目开发。
5、大部分软件配置管理的大学教材都是使用svn和vss。

缺点
1、服务器压力太大，数据库容量暴增。
2、如果不能连接到服务器上，基本上不可以工作，看上面第二步，如果服务器不能连接上，就不能提交，还原，对比等等。
3、不适合开源开发（开发人数非常非常多，但是Google app engine就是用svn的）。但是一般集中式管理的有非常明确的权限管理机制（例如分支访问限制），可以实现分层管理，从而很好的解决开发人数众多的问题。


### SSH连接
提示：GitHub建议使用强密码保护SSH密钥。更多信息见 Working with SSH key passphrases。
SSH为一项创建在应用层和传输层基础上的安全协议，为计算机上的Shell（壳层）提供安全的传输和使用环境。
传统的网络服务程序，如rsh、FTP、POP和Telnet其本质上都是不安全的；因为它们在网络上用明文传送数据、用户帐号和用户口令，很容易受到中间人（man-in-the-middle）攻击方式的攻击。就是存在另一个人或者一台机器冒充真正的服务器接收用户传给服务器的数据，然后再冒充用户把数据传给真正的服务器。
而SSH是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。利用SSH协议可以有效防止远程管理过程中的信息泄露问题。通过SSH可以对所有传输的数据进行加密，也能够防止DNS欺骗和IP欺骗。
SSH之另一项优点为其传输的数据可以是经过压缩的，所以可以加快传输的速度。SSH有很多功能，它既可以代替Telnet，又可以为FTP、POP、甚至为PPP提供一个安全的“通道”。
www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html
www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html
### Telnet
    Telnet协议是TCP/IP协议族中的一员，是Internet远程登陆服务的标准协议和主要方式。它为用户提供了在本地计算机上完成远程主机工作的能力。在终端使用者的电脑上使用telnet程序，用它连接到服务器。终端使用者可以在telnet程序中输入命令，这些命令会在服务器上运行，就像直接在服务器的控制台上输入一样。可以在本地就能控制服务器。要开始一个telnet会话，必须输入用户名和密码来登录服务器。Telnet是常用的远程控制Web服务器的方法。
http://www.cnblogs.com/joeblackzqq/archive/2012/04/27/2474011.html


### Github
    GitHub 是一个共享虚拟主机服务，用于存放使用Git版本控制的软件代码和内容项目。它由GitHub公司（曾称Logical Awesome）的开发者Chris Wanstrath、PJ Hyett和Tom Preston-Werner使用Ruby on Rails编写而成。
GitHub同时提供付费账户和为开源项目提供的免费账户。根据在2009年的Git用户调查，GitHub是最流行的Git存取站点。[2]除了允许个人和组织建立和存取代码库以外，它也提供了一些方便社会化软件开发的功能，包括允许用户跟踪其他用户、组织、软件库的动态，对软件代码的改动和 bug 提出评论等。GitHub也提供了图表功能，用于显示开发者们怎样在代码库上工作以及软件的开发活跃程度。
GitHub也提供一个粘贴箱风格的站点Gist，供软件代码库使用的Wiki，以及通过git版本库进行编辑和管理的网页托管功能。
http://www.cnblogs.com/fnng/archive/2012/01/07/2315685.html


### 开源项目托管
http://blog.csdn.net/tommengdle/article/details/6342414



### 国内代码托管平台
http://segmentfault.com/a/1190000000374128





## 任务1：熟悉Git基本操作

描述：熟悉Git的基本操作。

要求：完成所有的操作任务，每个主要环节截屏作为任务成果。

输出： 每个任务至少有一个截屏图片。

操作步骤（六个子任务）：

参照如下链接，完成“安装git”至“标签管理”共六项操作任务。

 http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000






## 任务2：生成SSH密钥并添加到Gitlab账号

描述：检查计算机现有SSH密钥；生成新的SSH密钥并添加到GitHub账户。

要求：成功使用SSH连接到GitHub。

输出：操作过程中的截屏。

**操作步骤**

1）检查SSH密钥

首先需要检查计算机上现有的SSH密钥。打开终端并输入：

![img](clip_image001.png)

检查是否存在 id_rsa.pub 或 id_dsa.pub。如果不存在任何一个则执行步骤2，否则可以直接跳到步骤3。

2）生成新的SSH密钥

为了生成新的SSH密钥，在终端中执行一下命令。确保邮箱地址换成正在使用的有效邮箱。当提示“enter a file in which to save the key”直接按回车继续，使用默认设置。

![img](clip_image002.png)之后会提示输入密钥的密码。可以提供密码或直接回车跳过。

![img](clip_image003.png)程序将输入类似以下内容：

![img](clip_image004.png)将新密钥加入ssh-agent：

![img](clip_image005.png)

3）将SSH密钥添加到GitHub

运行以下命令将密钥复制到剪贴板。

![img](clip_image006.png)或者，可以打开~/.ssh/id_rsa.pub 文件，手动将其内容复制到剪贴板。

在Github网站个人页面中，执行如下操作，将其加入Github。

l 页面右上角的用户栏中，点击账户设置。

![Account settings button](clip_image007.png)

l 点击左侧导航栏中的[SSH Keys](https://github.com/settings/ssh)。

![SSH Keys menu](clip_image008.png)

l 点击Add SSH key。

![SSH Key button](clip_image010.png)

l 在Title栏中添加密钥描述，将密钥复制到“Key”一栏。

![The key field](clip_image012.png)

l 点击**Add key**。

![The Add key button](clip_image013.png)

输入GitHub密码以确认操作。

4）为了确认之前的操作成功，尝试使用SSH连接到GitHub。当执行这一操作时会被提示输入建立SSH密钥时提供的密码（如果当时输入了密码）。

 

打开终端并输入：

![img](clip_image014.png)有可能会看到以下出错信息：

![img](clip_image015.png)这是在一些Linux版本中的已知问题。参考[帮助文档](https://help.github.com/articles/error-agent-admitted-failure-to-sign)以查找解决方案。

也可能会看到如下提示信息：

![img](clip_image016.png)确认fingerprint与创建SSH密钥时所给出的内容一致，然后输入“yes”。

![img](clip_image017.png)如果username是你的用户名，说明已经成功设置了SSH密钥。

如果收到了一个包含“access denied”的提示信息，可以[阅读这些内容加以诊断](https://help.github.com/articles/error-permission-denied-publickey)。



## 任务3：在Gitlab中建立仓库并提交文档

描述：

在Github中新建仓库Hello-World；
在本地新建文档“README.txt”并提交；（git commit）
将文档“README.txt”推送到远程仓库。（git remote add）

要求：

成功新建仓库，在仓库Hello-World中存在文档“README.txt”。
对操作过程进行截屏。



**输出结果**

1）操作过程截屏及最终结果截屏

![Your README has been created](clip_image002.jpg)

 

**操作步骤**

1）在GitHub中建立新的仓库，点击“New Repository”。

![Click "New Repository](clip_image004.jpg)

2）填入页面所需信息。完成后点击“Create Repository”。

![Fill in the info](clip_image006.jpg)

3）在仓库中建立README，创建README文件

打开终端并输入以下命令：

![img](clip_image007-165846181476216.png)编辑README文件，添加“Hello World!”作为内容。

2）提交README文件

![img](clip_image008-165846181476217.png)3）推送提交

以上步骤都是在本地完成的。为了将仓库与GitHub同步，需要将本地仓库与远程仓库管理并推送内容。

![img](clip_image009.png)

git push -u origin master –f

http://www.cnblogs.com/daemon369/p/3204646.html

 

（提示： 远程URL地址应该与GitHub上建立的仓库相对应，并保证大小写一致。）

在GitHub仓库中应该可以看到提交的README文件。

![Your README has been created](clip_image010.jpg)




## 任务4：在Github中Fork一个仓库

描述：

以项目“Spoon-Knife”为例，Fork这个仓库，下载到本地；
推送提交自己对项目的更改；（git push）
从远端拉取项目库的内容；（git fetch，git merge）
取消关注，删除Fork；

要求：

成功完成以上任务，对过程进行截屏。

**操作步骤**

1）Fork “Spoon-Knife”仓库

为了fork该项目，点击其仓库中的“Fork”按钮。

![Click "Fork"](clip_image001-165846189460925.png)

2）克隆fork到本地

执行以下命令：

![img](clip_image002-165846189461026.png)/索赔3）设置仓库远程映射

当仓库被克隆下来后，它有一个默认的远程源 origin 指向刚fork到自己账户的仓库，而不是项目自己原本的仓库。为了跟踪项目源仓库，需要添加另一个远程源 upstream：

![img](clip_image003-165846189461027.png)

4）推送提交，对项目做出了修改后，可以提交到fork过来的仓库。

![img](clip_image004-165846189461028.png)5）拉取项目自身仓库的内容

当你fork的项目的源仓库内容由更新时，可以通过以下命令将其更新到本地。

![img](clip_image005-165846189461030.png)Pull requests

如果希望项目的原作者能够将你的修改合并到项目源仓库中，可以向其发送[pull request](https://help.github.com/articles/using-pull-requests)。

6）取消关注源仓库

当你fork了一个热门仓库时，很多该仓库的更新信息都会发送到你的账号。如果不想看到这些信息，在项目源仓库中点击“Watch”按钮，选择“Not Watching”。

![Click "Unwatch"](clip_image007-165846189461029.png)

7）删除fork

可以使用与删除普通仓库一样的步骤删除fork过来的仓库。




## 任务5(可选)：掌握分支管理相关命令

每4个人一组，在gitlab上协同开发，具体开发内容，每个组自己决定。

描述：熟悉掌握分支管理相关内容；

要求：用到分支管理的所有操作命令。
