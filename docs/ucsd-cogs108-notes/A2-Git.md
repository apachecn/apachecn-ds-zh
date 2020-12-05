
# 附录二、git/Github 版本控制工具

> 原文：[Version Control with git/Github](https://nbviewer.jupyter.org/github/COGS108/Tutorials/blob/master/A2-Git.ipynb)
> 
> 译者：[飞龙](https://github.com/wizardforcel)
> 
> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

版本控制反映了一组与管理文件相关的实践，特别是管理不同版本的文件。

你可以在[维基百科](https://en.wikipedia.org/wiki/Version_control)或[ git 文档](https://git-scm.com/book/en/v2/)上阅读版本控制的更多信息。

<img src="img/git.png" width="400px">

Git 是一个版本控制系统：一种在多个位置跟踪文件变化的工具。

点击访问 [git](https://git-scm.com/doc)。Git 是一个开源软件项目。

<img src="img/github.png" width="400px">

Github 是基于 Web 的 Git 版本，以及版本控制仓库或互联网托管服务。这是一个地方，放置使用 git 跟踪的代码。

点击 [Github](https://github.com/)。注意 Github 是一家公司。

## Git 图形用户界面（GUI）

<img src="img/sourcetree.png" width="500px">

有几种方法可以使用 git，包括：

- 从命令行输入命令
- 使用图形程序启动 git 命令
  - 这种程序被称为“图形用户界面”（GUI）。
  - 它基本上只是意味着，你可以单击按钮来执行操作，而不是写出命令

无论哪种方式，底层命令和执行的代码都是相同的。在幕后，这一切都归约为同样的事情。

你应该使用你最熟悉的方法。如果你已经了解了一些命令行编程，那么从命令行使用 git 会很有用，因为通常会有更多功能可供你使用，具有更具体的控制。如果你对命令行不是很熟悉，那么使用 GUI 要简单得多。

如果你打算使用 GUI，我们建议你使用 SourceTree。

SourceTree 教程文档可在[此处](https://confluence.atlassian.com/get-started-with-sourcetree)获得。

## 本地 VS 远程

git 主要做的是保持同一个存储库的两个（或更多）版本一致。

存储库只是文件的集合，就像计算机上的文件夹。

我们将这些副本称为：

- “本地”副本，它是计算机上存储库的副本（对你而言是“本地”副本）
- “远程”副本，它是其他地方的存储库的副本，例如在 Github 上

通常有一个特定的代码副本称为`master`，这意味着它是相关存储库的主版本。最典型的情况是，这是 Github 上代码的副本 - 因此 Github 上有一个`master`代码副本，并且一个或多个人也有本地代码副本，并带有本地更新。当想要共享本地更新时，可以将它们发送给`master`，以便为每个人更新代码的主要版本。

在这里，我们将考虑上面描述的，具有两个存储库副本的情况。 这里描述的内容都可以扩展到代码的多个副本，包括存储库的多个不同远程副本。

作为版本控制系统，git 的主要功能是自动检查存储库的每个副本中的所有文件，跟踪发生的任何更改。然后，它提供了工具，在有变化时在不同副本之间进行同步。

## 从 Github 获取代码

最典型的是，Github 上有可用的代码，你希望获得本地副本，使用代码并可能更新代码，然后将更新发送回 Github。

首先，你需要获取代码的本地副本。Git 将生产存储库的副本称为`clone`。

从命令行，要将 Github 存储库克隆到你的计算机，请使用带有存储库 URL 的`clone`命令。

- `$ git clone 'repo_url'`

# 跟踪和传播更改

获得连接到远程存储库的本地副本后，更改可以分为两个方向：

- 将你在本地进行的更改发送到远程
- 使用远程更改更新本地副本

## 从本地 -> 远程跟踪和发送更改

处理本地文件时，git 有多个“级别”。这些多个级别可用于组织更改，放入组织良好的操作中。

典型的工作流程是：

- 添加`add`：选择你希望 git 跟踪哪些文件的哪些更改
  - 你可以将多个文件一起添加，每个文件都有自己的更改
- 提交`commit`：创建一个检查点，保存添加到一起的所有文件
  - 这些更改将与更改内容的消息（提交日志）一起“保存”
- 推送`push`：将更改发送到遥控器

首先，在本地 git 存储库中，你对文件进行了一些更改。

你现在可以添加文件。这需要针对我们要记录的，每个你更改的文件进行：

- `$ git add 'f_name'`

添加一个或多个文件后，使用提交`commit`保存这些文件的状态：

- `$ git commit -m 'Commit message'`

`-m`标志是直接使用命令编写提交消息的选项。如果你不添加它，git 会把你送到一个文本编辑器，你可以在那里写提交消息。你应始终添加已更改/添加内容的信息性消息。

通过详细消息进行小的，增量的更改和提交，通常意味着你的 Github 日志可以作为项目的历史记录，跟踪你已完成的工作。

如果一切突然损坏，这也允许你回退到旧版本的代码。

提交的更改仍存储在本地副本中。要更新远程存储库，你必须推送：

- `$ git push`

你不必在每次提交后推送，`git push`可以同时推送许多提交。

## 从远程获取更改 -> 本地

Git 使用`pull`（拉取）来指代，使用来自远程副本的更改更新本地副本。

在命令行上，如果远程分支上有更改，请使用`git pull`将这些更改复制到本地。

- `$ git pull`

## Git 速查表

最常见的 git 功能是：

- `git status`
    - 检查 git 存储库的状态
- `git add 'file'`
    - 将文件添加到暂存区域
- `git commit -m 'message'`
    - 在暂存区域中记录所有更改的“保存点”。
- `git push`
    - 将提交复制到远程
- `git diff 'file'`
    - 检查自上次提交以来文件中的更改
- `git clone 'repo'`
    - 创建 git 存储库的本地副本
- `git pull`
    - 从远程更新 git 存储库的本地副本

## 高级 Git：分支和合并

Git 还有许多其他功能，包括[分支](https://git-scm.com/book/en/v1/Git-Branching/)和[合并](https://git-scm.com/docs/git-merge)，当你习惯使用 git 并着手更大的项目时，值得探索它。

## 外部资源和教程

有许多使用 Github 的教程，包括[交互式教程](https://try.github.io/levels/1/challenges/1)和 [Hello World](https://guides.github.com/activities/hello-world/)，两者都是由 Github 制作的。还有其他一些有用的指南和教程，包括 [LifeHacker](http://lifehacker.com/5983680/how-the-heck-do-i-use-github)，[Atlassian](https://www.atlassian.com/git/tutorials) 和 [neuroplausible](http://neuroplausible.com/github) 上提供的这些指南和教程。
