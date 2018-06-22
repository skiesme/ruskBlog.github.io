---
layout: post
title: 'Mac中的常用软件和工具'
date: 2018-03-16
author: 如花与食客
catalog: true
tags: 
    - Mac
---

# Mac中的常用软件和工具
> 决定整理一篇Mac使用指南，部分内容来自[强迫症的 Mac 设置指南](https://github.com/macdao/ocds-guide-to-setting-up-mac)

## ** Daily-Tools **

### [HomeBrew](https://brew.sh/)
包管理工具，官方称之为The missing package manager for OS X。

安装步骤见官网。

有了 brew 以后，要下载工具，比如 MySQL、Gradle、Maven、Node.js 等工具，就不需要去网上下载了，只要一行命令就能搞定：
```
brew install mysql gradle maven node
```
PS：安装 brew 的时候会自动下载和安装 Apple 的 Command Line Tools。

---

### [Homebrew-Cask](https://caskroom.github.io/)
brew-cask 允许你使用命令行安装 OS X 应用。比如你可以这样安装 Chrome：``brew cask install google-chrome``。还有 Evernote、Skype、Sublime Text、VirtualBox 等都可以用 brew-cask 安装。

brew-cask 是社区驱动的，如果你发现 brew-cask 上的应用不是最新版本，或者缺少你某个应用，你可以自己提交 pull request。

安装步骤见官网。

应用也可以通过 App Store 安装，而且有些应用只能通过 App Store 安装，比如 Xcode 等一些 Apple 的应用。App Store 没有对应的命令行工具，还需要 Apple ID。倒是更新起来很方便。

几乎所有常用的应用都可以通过 brew-cask 安装，而且是从应用的官网上下载，所以你要安装新的应用时，建议用 brew-cask 安装。如果你不知道应用在 brew-cask 中的 ID，可以先用``brew cask search``命令搜索。

---

### [iTerm2](https://www.iterm2.com/)

iTerm2 是最常用的终端应用，是 Terminal 应用的替代品。提供了诸如Split Panes等一群实用特性。它默认的黑色背景让我毫不犹豫的抛弃了 Terminal。

安装：
```
brew cask install iterm2
```
感谢 brew-cask，我们可以通过命令行自动安装 iTerm2 了。

在终端里，除了可以用⌃E等快捷键（详见其他快捷键）之外，还可以使用``⌥B``、``⌥F``等快捷键（具体可以参考这里）。前提是这样设置一下：

选择``Iterm菜单 > Preferences > Profiles``，选择你在使用的 ``Profile（默认是Default）``，在Keys标签页中把``Left option (⌥) key acts as``和``Right option (⌥) key acts as``都设置成+ESC。

在打开新的窗口/标签页的时候，默认情况下新窗口总是 HOME 目录，还需要我每次敲命令才能进入工作目录。如果想要这个新窗口在打开的时候就自动进入工作目录，需要如下设置：

选择``Iterm菜单 > Preferences > Profiles``，选择你在使用的`` Profile（默认是Default）``，在``General``标签页中的``Working Directory``部分中选择``Reuse previous seesion's directory``。

至此，Terminal 应用已经出色的完成了其历史使命。后面命令行就交给 iTerm2 啦。

在 iTerm2 中双击会自动选中对应的词，三击会选中对应的整行。选中的内容会自动进入剪贴板，不需要再按``⌘C``复制。

---

### [Oh-My-Zsh](http://ohmyz.sh/)
默认的 Bash 是黑白的，没有色彩。而 Oh My Zsh 可以带你进入彩色时代。Oh My Zsh 同时提供一套插件和工具，可以简化命令行操作。后面我们会看到很多介绍，你会看到我爱死这家伙了。

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
> 安装方法最好以官网为准。

目前我使用的插件有：``git z sublime history rbenv bundler rake``

Oh My Zsh 使用了 Z shell（zsh），一个和 Bash 相似的 Shell，而非 Bash。
在 Z shell 中，是最重要的配置文件。Oh My Zsh 在安装的时候会把当前环境的``$PATH``写入``~/.zshrc``中。这并不是我期望的行为，因为使用了 brew，我们基本不再需要去定制``$PATH``，而 Oh My Zsh 提供的默认``$PATH``值``$HOME/bin:/usr/local/bin:$PATH``是非常合适的一个值，它把``$HOME/bin``加入了``$PATH``，可以让我们把自己用的脚本放到``$HOME/bin``下。
所以建议把``~/.zshrc``重置：
```
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```

> 主题的选择可参考：[iTerm2 + oh my zsh +agnoster 打造最强Mac终端 - 思过崖](http://www.siguoya.name/pc/home/article/256)
> 

---

### [Boostnote](https://boostnote.io/)
支持：
* Markdown
* Snippet Note

Boostnote 是一款专门为程序员朋友量身打造的笔记软件，除了日常笔记记录，最大的用处就是帮你记录无数的代码资源，你甚至可以以一个单个笔记为单位，在里面创建多个 Tab，以组成一个独立的 Code 项目。软件支持收藏、标签、分组、搜索、栏目切换等笔记应用应有的功能。
> 更多使用方法可看：[Boostnote：为程序员量身定做的笔记应用](https://www.waerfa.com/boostnote-review)

---

### [Sourcetree](https://www.sourcetreeapp.com/)
SourceTree 是 Atlassian 公司出品的一款优秀的 Git 图形化客户端。如果你发现命令行无法满足你的要求，可以试试 SourceTree。

安装：
```
brew cask install sourcetree
```
用 brew-cask 安装会自动增加命令行工具``stree``到``$PATH``里。在命令行中输入``stree``可以快速用 SourceTree 打开当前 Git 仓库。详细用法请参见``stree --help``。

---

### [Alfred](https://www.alfredapp.com/)
Mac 用户不用鼠标键盘的必备神器，配合大量 Workflows，习惯之后可以大大减少操作时间。

上手简单，调教成本在后期自定义 Workflows，不过有大量雷锋使用者提供的现成扩展，访问这里挑选喜欢的，并可以极其简单地根据自己的需要修改。

安装:
```
brew cask install alfred
```

> 玩法推荐：[你绝不能错过的效率神器 —— Alfred](https://www.cnblogs.com/chanshuyi/p/the_efficient_app_alfred.html)

### [MindNode](https://mindnode.com/)
> [MindNode for Mac - 官方介绍](https://mindnode.com/mindnode/mac)

MindNode，这是一款横跨 Mac 和 iOS 的双平台应用。

它可能是你见过最精美的思维导图应用。恰到好处的配色，顺滑的动画，以及自适应匹配版式，带来视觉享受的同时，也是对用户体验的一种加分。

---
### [OmniPlan](https://www.omnigroup.com/omniplan/)
> 最NB的项目管理流程软件.

OmniPlan for mac 是Mac OS X平台的的一款非常强大的项目管理软件，它提供的功能包含了自定检视
表、阶层式的纲要模式、成本追踪、里程碑、任务限制与相关性、资源分配、时程控制、Gantt 图表、违反事项显示、关键路径等等

除了附带项目策划专业用户需要的Gnatt图等多种功能外，OmniPlan可直接运行Windows下的 MicrosoftProject文件，也可以导入Microsoft Project的XML和Fasttrack Schedule文件。同时，OmniPlan可输出到iCal, CSV, MPX, XML, HTML等数据来辅助各项功能。

---
### [Maipo](http://weiboformac.sinaapp.com/)
全功能新浪微博 macOS 客户端，有自己的Timeline。

---
### [CleanMyMac](http://www.mycleanmymac.com/)
CleanMyMac是一个系统清理工具，删除系统缓存文件 , 多余的应用程序语言包 , PowerPc软件运行库等。 是个给你的硬盘瘦身的好工具。

---
### [Bartender3](https://www.macbartender.com/)
Bartender是一款非常实用的Menubar菜单栏管理小助手。随着Mac使用时间的增长，那原本简洁的菜单栏也自然而然会慢慢变长，加上某些应用 的菜单栏也有一定的长度，这时候用Bartender来对杂乱的菜单栏进行管理是再好不过的了。

---
### [Irvue](https://itunes.apple.com/cn/app/irvue-unsplash-wallpapers/id1039633667?mt=12)
> 自动更换壁纸的代表

Irvue 主打功能就是会定期的给你的 Mac 换上不同壁纸，用户可以设置图片的自动更换频率，比如每 30 分钟、1 小时、2 小时，甚至更长，当然你也可以手动切换壁纸。如果遇到自己喜欢的图片，你可以下载它，它会自动被存在照片里面的「Irvue」文件夹中。如果遇到不喜欢的照片，也可将其拉入黑名单。

Irvue 支持更改存储壁纸的路径、支持用热键切换壁纸、支持多屏使用同一张壁纸等。总的来说，Irvue 是一款设置省心，但是能带给大家一抹不经意小惊喜的应用，值得一直使用。

Irvue 的壁纸来源为 Unsplash，Unsplash 是一个高质量的照片分享网站，所有照片采用 Creative Commons Zero 授权，可以随意使用，Irvue 会将这些图片铺设为适合 Mac 屏幕的样式。

---
### [fish-shell](http://fishshell.com/)
简介
fish 可以根据输入自动匹配历史命令。它的一大特点是开箱即用，没有zsh那些繁琐的配置。

安装
在终端里使用Homebrew安装，直接输入 ``brew install fish`` 等待安装完成即可。安装完了以后还不能用，因为没把fish添加到 mac 的 shell 列表里，切换到 fish shell 时显示找不到fish shell，所以我们要先添加 fish 并设置一下 shell 。首先，用 shell 命令 ``sudo vim /etc/shells`` 在 vim 中打开 Mac 的 shell 列表，执行结果如下：
```
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```
按``i``键，进入插入模式，然后在列表末尾加上``/usr/local/bin/fish``。最后文件内容如下：
```
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
/usr/local/bin/fish
```
最后，按 ``esc`` 键跳到命令模式，输入``:wq`` 命令保存文件并退出vim。当前模式还是 bash shell 模式，要切换到 fish shell 需要输入 ``fish`` 命令。每次都输入命令切换 shell 比较繁琐，我们可以通过如下命令从 bash 切换到 fish ：
```
chsh -s /usr/local/bin/fish
```
也可以通过如下命令切回到 bash：
```
chsh -s /bin/bash
```

---
### WindowTidy
Window Tidy是一款Mac平台的增强型窗口控制工具，支持通过选取网格区域和拖拽到区域位置两种方式动态的调整窗口的位置和大小，可以任意自定义位置和大小配置，自由度很高，基本可以满足所有人的各种不同实际使用需求了。

软件特点
* 直观的界面与 OS X 无缝集成。
* 布局可以添加、 删除和定制。
* 指定的外观和位置弹出的版式图标。
* 配置 Option 键 ⌥，要么显示 / 隐藏版式图标，同时拖动。
* 独立网格的大小，为每个布局的。
* 优雅的多显示器支持 。
* 菜单选项，以便将活动窗口移动到当前屏幕。
* 快速布局选项应用一个新的布局，而不将其添加到列表中。
* 奖金功能允许 windows 被捕获到粘贴板只是将它们拖至布局。
* 分配键盘快捷方式是不方便使用鼠标的个别布局。

---
### IINA
IINA Mac版是一个基于 mpv、契合 macOS 设计风格、力求做到最佳用户体验、轻便且功能强大的视频播放器。为最新 Mac 系统而生，支持 Touch Bar、兼容 MPV 脚本、几乎支持所有格式、网络播放，是一款拥有优雅外观的视频播放器。

---
### DiskDrill
Disk Drill Pro是Mac上的数据恢复软件，使用Disk Drill Pro可以帮助我们恢复误删除的任何数据，比如照片、视频、音乐、文档等等，支持FAT / NTFS / HFS +等磁盘分区格式，支持本地硬盘和移动硬盘，还可以恢复iPhone和iPad的上的数据，功能十分强大！亲测十分有用！

---

## ** Develop-Tools **
---
### SublimeText
Sublime Text 是一个代码编辑器.也是HTML和散文先进的文本编辑器。漂亮的用户界面和非凡的功能，例如迷你地图，多选择，Python的插件，代码段，等等。完全可自定义键绑定，菜单和工具栏。
Sublime Text的主要功能包括：拼写检查，书签，完整的 Python API ， Goto 功能，即时项目切换，多选择，多窗口等等。
#### Sublime Text 2
安装：
```
brew cask install sublime-text
```
#### [Sublime Text 3](http://xclient.info/s/sublime-text.html?_=ae79901439c1042a991c0e690ef6899e)

插件：
具体插件可根据自身需求自行添加。

---
### [VSCode](https://code.visualstudio.com/)
Visual Studio Code（以下简称vscode）是一个轻量且强大的代码编辑器，支持Windows，OS X和Linux。内置JavaScript、TypeScript和Node.js支持，而且拥有丰富的插件生态系统，可通过安装插件来支持C++、C#、Python、PHP等其他语言。

据vscode的作者介绍，这款产品可能是微软第一款支持Linux的产品。
微软对于vscode的定位如下图，位于编辑器与IDE之间，但是更像一个编辑器。有人说是披着编辑器外衣的IDE，我觉得是披着IDE外衣的编辑器。

插件：
具体插件可根据自身需求自行添加。

---
### [Reveal](https://revealapp.com/)
Reveal是Mac OS X平台上的一款方便开发者调试IOS应用的开发软件，reveal能够在运行时调试和修改iOS应用程序。Reveal能连接到应用程序，并允许开发者编辑各种用户界面参数，而且会立即反应在程序的UI上。

> 具体使用方法参考：[IOS UI 界面调试工具 Reveal 使用教程](https://juejin.im/entry/57c53bff8ac2470063550be2)

---
### [Dash](https://kapeli.com/dash)
超棒的Mac平台的API文档浏览器和代码片段的管理工具，可以帮助你储存的代码片段,以及即时搜索和浏览文档几乎任何API文档。

---
### [Navicat Premium](http://www.navicat.com.cn/store/navicat-premium)
Navicat Premium 是一套数据库开发工具，让你从单一应用程序中同时连接 MySQL、MariaDB、SQL Server、Oracle、PostgreSQL 和 SQLite 数据库。它与 Amazon RDS、Amazon Aurora、Amazon Redshift、SQL Azure、Oracle Cloud 和 Google Cloud 等云数据库兼容。你可以快速轻松地创建、管理和维护数据库。

---
### [PPRows](https://github.com/jkpang/PPRows)
在 Mac 上计算你写了多少行代码：
* 支持检测参与计算的代码文件夹数量以及代码行数；
* 支持同时检测多文件 / 多文件夹代码；
* 支持自定义检测的文件类型，例如: C，Swift，OC，Java... 类型的代码文件；
* 支持自定义需要忽略检测的文件夹, 例如: iOS 工程中的 Pods 文件夹；
* 支持中文与英文，跟随系统语言变化 (v1.1.0 起支持)；
* 支持忽略代码中的空行，代码行数计算更精确(v1.2.0 起支持)。

---
### [Charles](https://www.charlesproxy.com/)
Charles是一款用于HTTP信息抓包工具，可以快速有效的获得HTTP信息，非常利于开发者的网页开发和调试修改等！Charles 有着可视化的操作界面，非常利用编辑者的使用和调试！

你打开他，然后点选``Proxy`` –> ``Mac OS X Proxy``。然后就可以看到你网络请求的数据了。在第一次打开的时候他会很温馨的提示你要不要设置为系统代理的。

对于iOS开发来说，截取到iPhone上的网络请求是很有用的。同理，也是可以获取到anroid设备的请求。

---
### WoodPecker
《 WoodPecker 》是一款方便 iOS 开发者开发调试 App 的Mac 应用。
可以帮 iOS 开发者：
轻松操作沙盒文件，可在 Mac 端查看，编辑，更新 App 沙盒文件，支持常见文本、图片、sqlite 等文件格式。

监控 App 的网络请求，将 App 内的所有网络请求同步到 Mac 客户端显示，无需设置代理。
在 Mac 上控制 App 内 WebView 执行 Javascript，方便在线调试 App 内网页。

另外，还有友好的插件支持：
《 WoodPecker 》的核心在于提供一套稳定、易用的通信 Api，让开发者可以轻松在 Mac 和 App 之间传递数据，并在 Mac 上提供友好的显示支持，所以从开发初期就提供了完整的插件支持。现在开发者可以很方便定制自己的工具，与现有开发流程相互配合。

安装方式：
Mac AppStore 搜索 WoodPecker 即可。
- - -

## ** Design-Tools **
### [Sketch](https://www.sketchapp.com/)
Sketch是最强大的移动应用矢量绘图设计工具，对于网页设计和移动设计者来说，比PhotoShop好用N倍！尤其是在移动应用设计方面，Sketch的优点在于使用简单，学习曲线低，并且功能更加强大易用。能够大大节省设计师的时间和工作量，非常适合进行网站设计、移动应用设计、图标设计等。

使用时可配合使用插件管理工具：[Sketch Toolbox](http://sketchtoolbox.com/)

---
### [Axure RP](https://www.axure.com)
Axure RP是一个专业的快速原型设计工具，让负责定义需求和规格、设计功能和界面的专家能够快速创建应用软件或Web网站的线框图、流程图、原型和规格说明文档。作为专业的原型设计工具，它能快速、高效的创建原型，同时支持多人协作设计和版本控制管理。
