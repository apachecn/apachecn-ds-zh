
# 一、Jupyter 笔记本

> 原文：[Jupyter Notebooks](https://nbviewer.jupyter.org/github/COGS108/Tutorials/blob/master/01-JupyterNotebooks.ipynb)
> 
> 译者：[飞龙](https://github.com/wizardforcel)
> 
> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

这是 Jupyter 笔记本的快速介绍。


Jupyter 笔记本是一种将可执行代码，代码输出和文本组合到一个连接文件中的方法。


项目 Jupyter 的官方文档在[这里](https://jupyter-notebook.readthedocs.io/en/stable/)，他们也有一些示例笔记本在[这里](https://github.com/jupyter/notebook/tree/master/docs/source/examples/Notebook)。


## 菜单选项和快捷方式

要快速浏览 Jupyter 用户界面，请单击“帮助”菜单，然后单击“用户界面浏览”。

还有大量有用的键盘快捷键。单击“帮助”菜单，然后单击“键盘快捷键”来查看列表。

## 单元格

笔记本的主要组织结构是“单元格”。


单元格，可以是 markdown（文本），就像这一个或代码单元格（我们会看到他们）。

### Markdown 单元格

Markdown 单元格用于传达有关我们笔记本的信息。

它们执行基本的文本格式化，包括斜体，粗体，标题，链接和图像。

双击本节中的任何单元格以查看纯文本的外观。运行单元格，然后查看格式化的 Markdown 文本的外观。

```md
# 这是标题

## 这是较小的标题

### 这是更小的标题
```

我们可以将我的文本斜体化，像`*这样*`或`_这样_`。

我们可以像`**这样**`或像`__这样__`加粗我的文本。

这是一个无序的项目列表：

```md
* 这是一个项目
* 这是一个项目
* 这是一个项目
```

这是一个有序的项目列表：

```md
1. 这是我的第一个项目
2. 这是我的第二个项目
3. 这是我的第三个项目
```

我们可以使用缩进来获得嵌套列表：

```md
* 这是一个项目
* 这是一个项目
	* 这是一个项目
	* 这是一个项目
* 这是一个项目
```

我们还可以组合有序和无序列表：

```md
1. 这是我的第一个项目
2. 这是我的第二个项目
	* 这是一个项目
	* 这是一个项目
3. 这是我的第三个项目
```

我们可以这样链接到这个`[有用的 markdown 速查表](https://www.markdownguide.org/cheat-sheet/)`。

如果我们不对链接使用 markdown 语法，它只会将链接本身显示为链接文本：`https://www.markdownguide.org/cheat-sheet/`

### LaTeX 格式文本

```tex
$$ P(A \mid B) = \frac{P(B \mid A) \, P(A)}{P(B)} $$
```

### 代码单元格


```python
# 代码单元格中可以输入注释。
a = 1
b = 2


# 单元格也可以有输出，打印输出到单元格下方。
print(a + b)

# 3


my_string = 'hello world'


print(my_string)

# hello world


# TAB 补全，print(my_string.upper())
my_string.upper()

# 'HELLO WORLD'


my_list = ['a','b','c']


print(my_list)

# ['a', 'b', 'c']
```

## 访问文档


Jupyter 有很多有用的快捷方式。在函数或类之后添加一个 '?' 获取带有文档的窗口，或者两个 '??' 来拉出源代码。

```python
# 为示例导入 NumPy
import numpy as np


# 检查 NumPy 数组的文档
np.array?


# 检查 numpy append 函数的完整源代码
np.append??


# 获取你创建的变量的信息
my_string?
```

## 自动补全


Jupyter还具有[ tab 补全](https://en.wikipedia.org/wiki/Command-line_completion)功能，可以自动不全你输入的内容，和/或用于探索可用的代码。

```python
# 移动光标到点号之后，按 Tab 键
# 将出现一个下拉菜单，显示所有可能的补全
np.


# 自动填充不一定在点号处。移至 'ra' 的末尾并按 Tab 键查看补全选项。
ra


# 如果只有一个选项，tab 补全将自动补全你输入的内容。
ran
```

## 内核和命名空间

你不需要按顺序运行单元格！这对于灵活地测试和开发代码很有用。

单元格左侧方括号中的数字表示哪个单元格已运行以及按什么顺序运行。

但是，它也很容易丢失已经声明/导入的内容，导致运行单元格时的意外行为。

内核是将笔记本连接到计算机后台来执行代码的东西。

清除并重新启动内核非常有用。你可以从顶部的“内核”下拉菜单执行此操作，也可以选择清除所有输出。

## 魔术命令


“魔术命令”是 IPython / Jupyter 中一种特殊的（命令行）语法，用于运行特殊功能。它们可以在某行和/或整个单元上运行。

iPython [文档](http://ipython.readthedocs.io/en/stable/interactive/magics.html)提供了魔术命令的更多信息。

魔术命令旨在简洁地解决标准数据分析中的各种常见问题。魔术命令有两种形式：行魔术，由单个`%`前缀表示并在单行输入上操作，以及单元魔术，由双`%%`前缀表示，并在多行输入上操作。

```python
# 访问快速参考清单
%quickref


# 你可以查看可用的魔术命令列表
%lsmagic

'''
Available line magics:
%alias  %alias_magic  %autocall  %automagic  %autosave  %bookmark  %cat  %cd  %clear  %colors  %config  %connect_info  %cp  %debug  %dhist  %dirs  %doctest_mode  %ed  %edit  %env  %gui  %hist  %history  %killbgscripts  %ldir  %less  %lf  %lk  %ll  %load  %load_ext  %loadpy  %logoff  %logon  %logstart  %logstate  %logstop  %ls  %lsmagic  %lx  %macro  %magic  %man  %matplotlib  %mkdir  %more  %mv  %notebook  %page  %pastebin  %pdb  %pdef  %pdoc  %pfile  %pinfo  %pinfo2  %popd  %pprint  %precision  %profile  %prun  %psearch  %psource  %pushd  %pwd  %pycat  %pylab  %qtconsole  %quickref  %recall  %rehashx  %reload_ext  %rep  %rerun  %reset  %reset_selective  %rm  %rmdir  %run  %save  %sc  %set_env  %store  %sx  %system  %tb  %time  %timeit  %unalias  %unload_ext  %who  %who_ls  %whos  %xdel  %xmode

Available cell magics:
%%!  %%HTML  %%SVG  %%bash  %%capture  %%debug  %%file  %%html  %%javascript  %%js  %%latex  %%markdown  %%perl  %%prun  %%pypy  %%python  %%python2  %%python3  %%ruby  %%script  %%sh  %%svg  %%sx  %%system  %%time  %%timeit  %%writefile

Automagic is ON, % prefix IS NOT needed for line magics.
'''


# 查看当前工作目录
%pwd

# '/Users/shannonellis/Desktop/Teaching/COGS108/Tutorials'


# 所有变量
%who

# a	 b	 my_list	 my_string	 np	 


# 所有变量；更多信息
%whos

'''
Variable    Type      Data/Info
-------------------------------
a           int       1
b           int       2
my_list     list      n=3
my_string   str       hello world
np          module    <module 'numpy' from '/an<...>kages/numpy/__init__.py'>
'''


# 历史
%hist

'''
    ### Markdown 单元
    # 历史
    %hist
    # 指定你正在编写 HTML
    %%HTML
    <p>This is a paragraph</p>
    %%bash
    # 等价地，（对于 bash）使用 %% bash cell 魔术，将单元格作为 bash 运行（命令行）
    pwd
    # 在代码单元格中，可以键入注释
    a = 1
    b = 2
    # 单元格也可以有输出，打印输出到单元格下方。
    print(a + b)
    my_string = 'hello world'
    print(my_string)
    # Tab 补全，print(my_string.upper())
    my_string.upper()
    my_list = ['a','b','c']
    print(my_list)
    # 为示例导入 NumPy
    import numpy as np
    # 检查 NumPy 数组的文档
    np.array?
    # 检查 NumPy append 函数的完全源代码
    np.append??
    # 获取你创建的变量的信息
    my_string?
    # 移动光标到点号之后，按 Tab 键
    # 将出现一个下拉菜单，显示所有可能的补全
    np.
    # 在代码单元格中，可以键入注释
    a = 1
    b = 2
    # 单元格也可以有输出，打印输出到单元格下方。
    print(a + b)
    my_string = 'hello world'
    print(my_string)
    # tab 补全，print(my_string.upper())
    my_string.upper()
    my_list = ['a','b','c']
    print(my_list)
    # 为示例导入 NumPy 
    import numpy as np
    # 检查 NumPy 数组的文档
    np.array?
    # 检查 NumPy append 函数的完全源代码
    np.append??
    # 获取你创建的变量的信息
    my_string?
    # 移动光标到点号之后，按 Tab 键
    # 将出现一个下拉菜单，显示所有可能的补全
    np.
    # 访问快速参考清单
    %quickref
    #  你可以检查可用魔术命令的列表
    %lsmagic
    # 查看当前工作目录
    %pwd
    # 所有变量
    %who
    # 所有变量；更多信息
    %whos
    # 历史
    %hist
    # 例如，我们可以计算创建大型列表所需的时间
    %timeit list(range(100000))
    %%timeit
    # 例如，我们可以为整个单元格计时
    a = list(range(100000))
    b = [n + 1 for n in a]
    # 你可以通过在行的开头添加 '!' 来运行终端命令
    !pwd
    # 注意，在这种情况下，'!pwd' 等同于魔术 '%pwd'。
    # '!' 语法更通用，允许你通过命令行运行任何你想要的东西
    %%bash
    # 等价地，（对于 bash）使用 %% bash cell 魔术，将单元格作为 bash 运行（命令行）
    pwd
    # 列出目录中的文件
    !ls
    # 修改当前目录
    !cd .
    # 历史
    %hist
'''
```

### 行魔术


行魔术使用单个 '%'，并应用于单行。

```python
# 例如，我们可以计算创建大型列表所需的时间
%timeit list(range(100000))

# 1.6 ms ± 26.8 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```


### 单元魔术

单元魔术使用双“%%”，并应用至整个单元。

```python
%%timeit
# 例如，我们可以为整个单元格计时
a = list(range(100000))
b = [n + 1 for n in a]

# 6.59 ms ± 97.6 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
```


### 运行终端命令

笔记本的另一个好处是能够运行终端命令。

```python
# 你可以通过在行的开头添加 '!' 来运行终端命令
!pwd

# 注意，在这种情况下，'!pwd' 等同于魔术 '%pwd'。
# '!' 语法更通用，允许你通过命令行运行任何你想要的东西

# /Users/shannonellis/Desktop/Teaching/COGS108/Tutorials
```

```bash
%%bash
# 等价地，（对于 bash）使用 %% bash cell 魔术将单元格作为 bash 运行（命令行）
pwd

# /Users/shannonellis/Desktop/Teaching/COGS108/Tutorials
```

```py
# 列出目录中的文件
!ls

'''
00-Introduction.ipynb              13-OrdinaryLeastSquares.ipynb

01-JupyterNotebooks.ipynb          14-LinearModels.ipynb

02-DataAnalysis.ipynb              15-Clustering.ipynb

03-Python.ipynb                    16-DimensionalityReduction.ipynb

04-DataSciencePython.ipynb         17-Classification.ipynb

05-DataGathering.ipynb             18-NaturalLanguageProcessing.ipynb

06-DataWrangling.ipynb             A1-PythonPackages.ipynb

07-DataCleaning.ipynb              A2-Git.ipynb

08-DataPrivacy&Anonymization.ipynb LICENSE

09-DataVisualization.ipynb         README.md

10-Distributions.ipynb             [34mfiles[m[m

11-TestingDistributions.ipynb      [34mimg[m[m
'''


# 修改当前目录
!cd .
```

有关更多有用信息，请查看 Jupyter 笔记本[提示与技巧](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/)，以及有关[笔记本如何工作](http：//jupyter.readthedocs.io/en/latest/architecture/how_jupyter_ipython_work.html)的更多信息。
