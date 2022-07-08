# 第一章 第四讲  Linux和openEuler的发展历史



## 概述

![Linux官方的吉祥物，一只叫Tux的企鹅](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/NewTux.svg/150px-NewTux.svg.png)

Linux是一种自由和开放源码的类UNIX操作系统。该操作系统的内核由林纳斯·托瓦兹在1991年10月5日首次发布，在加上用户空间的应用程序之后，成为Linux操作系统。
Linux也是自由软件和开放源代码软件发展中最著名的例子。
只要遵循GNU 通用公共许可证（GPL），任何个人和机构都可以自由地使用Linux的所有底层源代码，也可以自由地修改和再发布。
大多数Linux系统还包括像提供GUI的X Window之类的程序。除了一部分专家之外，大多数人都是直接使用Linux 发行版，而不是自己选择每一样组件或自行设置。

Linux严格来说是单指操作系统的内核，因操作系统中包含了许多用户图形接口和其他实用工具。如今Linux常用来指基于Linux的完整操作系统，内核则改以Linux内核称之。由于这些支持用户空间的系统工具和库主要由理查德·斯托曼于1983年发起的GNU计划提供，自由软件基金会提议将其组合系统命名为GNU/Linux，但Linux不属于GNU计划，这个名称并没有得到社群的一致认同。

Linux最初是作为支持英特尔x86架构的个人电脑的一个自由操作系统。目前Linux已经被移植到更多的计算机硬件平台，远远超出其他任何操作系统。Linux可以运行在服务器和其他大型平台之上，如大型计算机和超级计算机。世界上500个最快的超级计算机已100％运行Linux发行版或变种。Linux也广泛应用在嵌入式系统上，如手机（Mobile Phone）、平板电脑（Tablet）、路由器（Router）、电视（TV）和电子游戏机等。在移动设备上广泛使用的Android操作系统就是创建在Linux内核之上。

通常情况下，Linux被打包成供个人计算机和服务器使用的Linux发行版，一些流行的主流Linux发布版，包括Debian（及其派生版本Ubuntu、Linux Mint）、Fedora（及其相关版本Red Hat Enterprise Linux、CentOS）和openSUSE等。Linux发行版包含Linux内核和支撑内核的实用程序和库，通常还带有大量可以满足各类需求的应用程序。个人计算机使用的Linux发行版通常包含X Window和一个相应的桌面环境，如GNOME或KDE。桌面Linux操作系统常用的应用程序，包括Firefox网页浏览器、LibreOffice办公软件、GIMP图像处理工具等。由于Linux是自由软件，任何人都可以创建一个符合自己需求的Linux发行版。

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Linux_kernel_ubiquity.svg/1920px-Linux_kernel_ubiquity.svg.png)

## 历史

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Linus_Torvalds_%28cropped%29.jpg/170px-Linus_Torvalds_%28cropped%29.jpg)

1991年，林纳斯·托瓦兹在赫尔辛基大学上学时，对操作系统很好奇。他对MINIX只允许在教育上使用很不满（在当时MINIX不允许被用作任何商业使用），于是他便开始写他自己的操作系统，这就是后来的Linux内核。

林纳斯·托瓦兹开始在MINIX上开发Linux内核，为MINIX写的软件也可以在Linux内核上使用。后来使用GNU软件代替MINIX的软件，因为使用从GNU系统来的源代码可以自由使用，这对Linux的发展有益。使用GNU GPL协议的源代码可以被其他项目所使用，只要这些项目使用同样的协议发布。为了让Linux可以在商业上使用，林纳斯·托瓦兹决定更改他原来的协议（这个协议会限制商业使用），以GNU GPL协议来代替。之后许多开发者致力融合GNU元素到Linux中，做出一个有完整功能的、自由的操作系统。

Linux的第一个版本在1991年9月被大学FTP server管理员Ari Lemmke发布在互联网上，最初Torvalds称这个内核的名称为"Freax"，意思是自由（"free"）和奇异（"freak"）的结合字，并且附上"X"这个常用的字母，以配合所谓的类Unix的系统。但是FTP服务器管理员嫌原来的命名“Freax”的名称不好听，把内核的称呼改成“Linux”，当时仅有10000行代码，仍必须执行于Minix操作系统之上，并且必须使用硬盘引导；随后在10月份第二个版本（0.02版）发布，同时这位芬兰赫尔辛基的大学生在comp.os.minix上发布一则消息

Hello everybody out there using minix- I'm doing a (free) operation system (just a hobby, won't be big and professional like gnu) for 386(486) AT clones.

Linux的标志和吉祥物是一只名字叫做Tux的企鹅，标志的由来有一说是因为Linus在澳洲时曾被一座动物园里的企鹅咬了一口，便选择企鹅作为Linux的标志，但更容易被接受的说法是：企鹅代表南极，而南极又是全世界所共有的一块陆地。这也就代表Linux是所有人的Linux。

1994年3月，Linux1.0版正式发布，Marc Ewing成立Red Hat软件公司，成为最著名的Linux经销商之一。早期Linux的引导管理程序（boot loader）使用LILO（Linux Loader），早期的LILO存在着一些难以容忍的缺陷，例如无法识别1024柱面以后的硬盘空间，后来的GRUB（GRand Unified Bootloader）克服这些缺点，具有‘动态搜索内核文件’的功能，可以让用户在引导的时候，自行编辑引导设置系统文件，透过ext2或ext3文件系统中加载Linux Kernel（GRUB通过不同的文件系统驱动可以识别几乎所有Linux支持的文件系统，因此可以使用很多文件系统来格式化内核文件所在的扇区，并不局限于ext文件系统）。

今天由Linus Torvalds带领下，众多开发人员共同参与开发和维护Linux内核。理查德·斯托曼领导的自由软件基金会，继续提供大量支持Linux内核的GNU组件。一些个人和企业开发的第三方的非GNU组件也提供对Linux内核的支持，这些第三方组件包括大量的作品，有内核模块和用户应用程序和库等内容。Linux社区或企业都推出一些重要的Linux发行版，包括Linux内核、GNU组件、非GNU组件，以及其他形式的软件包管理系统软件。



## 常见发行版

### Debian

![Debian OpenLogo](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4a/Debian-OpenLogo.svg/80px-Debian-OpenLogo.svg.png)

Debian是完全由自由软件组成的类UNIX操作系统，其包含的多数软件使用GNU通用公共许可协议授权，并由Debian计划的参与者组成团队对其进行打包、开发与维护。

Debian计划最初由伊恩·默多克于1993年发起，Debian 0.01版在1993年9月15日发布，而其第一个稳定版本则在1996年发布。

该计划的具体工作在互联网上协调完成，由Debian计划领导人带领一个志愿者团队开展工作，并以三份奠基性质的文档作为工作指导：Debian社群契约、Debian宪章和Debian自由软件指导方针。操作系统版本定期进行更新，候选发布版本将在经历过一定时间的冻结之后进行发布。

作为最早的Linux发行版之一，Debian在创建之初便被定位为在GNU计划的精神指导下进行公开开发并自由发布的项目。该决定吸引自由软件基金会的注意与支持，他们为该项目提供从1994年11月至1995年11月为期一年的赞助。赞助终止后，Debian计划创立非营利机构Software in the Public Interest以提供支持并令其持有Debian商标作为保护机构。Debian也接受世界多个非营利组织的资金支持。

### Ubuntu

![Ubuntu-logo-2022.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/Ubuntu-logo-2022.svg/250px-Ubuntu-logo-2022.svg.png)


Ubuntu是基于Debian，以桌面应用为主的Linux发行版。Ubuntu有三个正式版本，包括桌面版、服务器版及用于物联网设备和机器人的Core版。前述三个版本既能安装于实体电脑，也能安装于虚拟电脑。从17.10版本开始，Ubuntu以GNOME为默认桌面环境。

Ubuntu是著名的Linux发行版之一，也是目前最多用户的Linux版本。Ubuntu每六个月（即每年的四月与十月）发布一个新版本，长期支持（LTS）版本每两年发布一次。普通版本一般只支持9个月，但LTS版本一般能提供5年的支持。



Ubuntu由英国Canonical公司发布，他们提供商业支持。它是基于自由软件，其名称来自非洲南部祖鲁语或科萨语的“Ubuntu”一词（译为乌班图），意思是“人性”、“我的存在是因为大家的存在”，是非洲传统的一种价值观。

Canonical由南非企业家Mark Shuttleworth创立。Canonical通过销售与Ubuntu相关的技术支持和其他服务来产生收益。Ubuntu项目公开承诺开源软件开发的原则；鼓励人们使用自由软件，研究它的运作原理，改进和分发。

### CentOS

![Centos-logo-light.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Centos-logo-light.svg/200px-Centos-logo-light.svg.png)

CentOS（Community Enterprise Operating System）是Linux发行版之一，它是来自于Red Hat Enterprise Linux（RHEL）依照开放源代码规定发布的源代码所编译而成。由于出自同样的源代码，因此有些要求高度稳定性的服务器以CentOS替代商业版的Red Hat Enterprise Linux使用。
两者的不同，在于CentOS并不包含封闭源代码软件。CentOS 对上游代码的主要修改是为了移除不能自由使用的商标。2014年，CentOS宣布与Red Hat合作，但CentOS将会在新的委员会下继续运作，并不受RHEL的影响。

CentOS和RHEL一样，都可以使用Fedora EPEL来补足软件。

CentOS开发团队于2020年12月8日宣布，传统的CentOS 8将仅维护至2021年底，之后仅维护CentOS Stream，使其变为滚动发行的散布版（CentOS 7仍将持续维护至原本的支持周期结束）。

### Arch Linux

![Arch Linux logo.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/7/74/Arch_Linux_logo.svg/250px-Arch_Linux_logo.svg.png)

Arch Linux是一个独立开发的 x86-64 通用 GNU/Linux 发行版，它致力于通过滚动发布来提供大多数软件的最新稳定版本。默认安装是一个最小的基本系统，由用户配置添加有意需要的内容。Arch Linux 使用pacman作为包管理器。

Arch Linux采用滚动更新。Arch Linux 努力维护其软件的最新稳定版本，只要可以合理地避免系统包损坏。

Arch Linux 以社区 Wiki 的形式提供文档，称为 ArchWiki（页面存档备份，存于互联网档案馆）。

Arch Linux 项目注力于简洁主义，其贡献在于对发行版的组件提供具有良好注释的配置文件，而非带有图形界面的配置工具。因此该发行版被称为适合“不惧怕命令行的中高级Linux用户”。

### openSUSE

![OpenSUSE Logo.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/OpenSUSE_Logo.svg/150px-OpenSUSE_Logo.svg.png)

openSUSE，前身为SUSE Linux和SuSE Linux Professional，是一个Linux发行版计划，由SUSE Linux GmBH与其他公司赞助。
openSUSE在全世界被广泛使用，尤其是在德国。它的开发重心是为软件开发者和系统管理者创造适用的开放源代码的工具，并提供易于使用的桌面环境和功能丰富的服务器环境。
openSUSE针对桌面环境进行了一系列的优化，是一个对Linux新手较为友好的Linux发行版。

## 应用


Linux发行版一直被用来作为服务器的操作系统，并且已经在该领域中占据重要地位。根据2006年9月Netcraft的报告显示，十个最大型的网络托管公司有八个公司在其Web服务器运行Linux发行版。

Linux发行版也经常使用作为超级计算机的操作系统，2010年11月公布的超级计算机前500强，有459个（91.8％）运行Linux发行版。曾经是世界上最强大的超级计算机——IBM的红杉（IBM Sequoia），已于2011年交付劳伦斯利福摩尔国家实验室，并于2012年6月开始运作，也是选择Linux作为操作系统。

![U.S. Department of Energy - Science - 477 022 010 (9444538239).jpg](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/U.S._Department_of_Energy_-_Science_-_477_022_010_%289444538239%29.jpg/1280px-U.S._Department_of_Energy_-_Science_-_477_022_010_%289444538239%29.jpg)

在智能手机、平板电脑等移动设备方面，Linux也得到重要发展，基于Linux内核的Android操作系统已经超越Apple的iOS操作系统，成为当今全球最流行的智能手机操作系统。在2010年第三季度，销售全球的全部智能手机中使用Android的占据25.5%（所有的基于Linux的手机操作系统在这段时间为27.6%）。

Linux的低成本、强大的定制功能以及良好的移植性能，使得Linux在嵌入式系统方面也得到广泛应用。思科在网络防火墙和路由器也使用了定制的Linux。


## openEuler

EulerOS是华为基于CentOS源代码，面向企业应用环境开发的一个商用Linux发行版。

2019年9月，华为宣布EulerOS开源，开源名称为openEuler（开源欧拉）。华为在Gitee上附源代码发布EulerOS的社区版本openEuler。

2021年11月初，华为向开放原子开源基金会（OpenAtom Foundation）捐赠了EulerOS。



## 黑客文化


本讲向大家介绍了Linux的历史，其实在创建Linux历史中做出很大贡献的人大多数是我们心目中的黑客。

黑客在美国有两个词hacker和cracker，这两个词是有明确的区别。对系统搞破坏的、搞数据偷窃等的人称为cracker。而hacker一般指对操作系统有研究、做出创造性贡献的人。

在上世纪 Dennis Ritchie 开始就有了黑客文化，这种文化可以概括为对技术和自由的极致追求。

这里主要有四个方面： 

   
   1. 坚持开放，反对封闭  这里举例子来说明，贝尔实验室开发的Multics限制人们使用，当时AT&T提出版权制度，微软也是，我们一直看   	不到Windows操作系统的源码。对黑客来说，这些就是他的敌人。  

   2. 追求自由，反对限制  这就是我们前面提到的Copyright，Copyleft。   还有，Richard Stallman 提出的Free as in freedom，这是指软件无论是否收费，必须要保证我的自由，总而言之，要的是自由。free在英文里有两种意思，自由或免费。Richard Stallman等人明确提出freesoftware中的free是自由，不是免费的意思。     

   3. 敢于独立创造，不迷信权威  这里举一个例子，年仅22岁的Linus和 学术泰斗Andrew S. Tanenbaum曾经有一场纯粹的技术论战。Linus认为Linux是一个单体内核操作系统即是宏内核操作系统，Tanenbaum认为微内核操作系统Minix比宏内核操作系统Linux更优越，宏内核操作系统无论从架构还是设计理念上是过时的，而且Tanenbaum从学术方面做了一个论证，证明Linux不具有扩展性，不能适应于未来的发展趋势。但是Linus没有畏惧于Tanenbaum的学术权威，他认为Minix不具有实用性，设计理念虽好，但在硬件平台上无法达到宏内核的性能。最后论战结果是谁都不服谁。后来的20年中实践证明Linux比Minix实用性上要好很多。 

   4. 视物质财富如粪土  这对真正黑客来说是这样的。他们对财富看得非常单薄，对他们自己的贡献或荣誉看得很重。  我们平时看到的微软是缩写成MS，但在黑客社区将微软称之为M$，就是many dollar，就是很多钱，黑客们觉得这样是很愚昧的。他们只是把在社区的贡献得到的认可看得很重要。  Linux创始人Linus本人现在还活跃在Linux内核社区里，在社区里起辅导作用。社区里有人把发现的一些很隐蔽的bug发给他，他能够在很短的时间内看出bug发生在内核哪一行，这是很不容易的。  为什么说不容易了。  大家知道现在Linux内核有多少行代码？是1500多万行。可以想象Linus对这1500万行了如指掌。Linus对Linux贡献很大，但他本人并没有从Linux得到太多财富，也不像比尔盖茨成为世界首富。这就是黑客文化。  
