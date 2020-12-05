
# 附录一、有用的 Python 数据科学包

> 原文：[Useful Python Packages for Data Science](https://nbviewer.jupyter.org/github/COGS108/Tutorials/blob/master/A1-PythonPackages.ipynb)
> 
> 译者：[飞龙](https://github.com/wizardforcel)
> 
> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

以下是 Python 中可能对数据科学有用的包一般概述。

有关更广泛/更全面的 Python 生态系统列表，请查看[ Awesome Python ](https://github.com/vinta/awesome-python)列表。

# 数据科学模块

这些包都包含在 anaconda 发行版中。

### 核心包

- [scipy](https://www.scipy.org) - 数学，科学和工程。
- [numpy](http://www.numpy.org) - 数组和数组运算的数值计算。
- [pandas](https://pandas.pydata.org) - 数据结构和数据分析。
- [scikit-learn](http://scikit-learn.org/stable/) - 机器学习和数据分析。
    
### 文本挖掘

- [nltk](http://www.nltk.org) - 自然语言处理。
- [gensim](https://radimrehurek.com/gensim/) - 主题建模。

### 数学和统计学

- [sympy](http://www.sympy.org/en/index.html) - 符号数学。
- [statsmodels](http://www.statsmodels.org/stable/index.html) - 统计建模。

### 网络爬虫

- [requests](http://docs.python-requests.org/en/master/) - HTTP 请求。
- [scrapy](https://scrapy.org) - 网络爬虫。
    
### 可视化库

- [matplotlib](https://matplotlib.org) - 2D 绘图库。
- [seaborn](https://seaborn.pydata.org/) - 可视化（基于 Matplotlib）
- [bokeh](http://bokeh.pydata.org/en/latest/) - 交互式可视化。
    
### 图论/网络

- [networkx](https://networkx.github.io/) - 网络分析
- [graph-tool](https://graph-tool.skewed.de/) - 图的操作和分析
    
### 深度学习

- [theano](http://deeplearning.net/software/theano/) - 多维数组的数学运算。
- [tensorflow](https://www.tensorflow.org/) - 使用数据流图进行数值计算。
- [keras](https://keras.io) - 高级神经网络库。

# 标准库的有用部分

标准库中的完整软件包列表在[这里](https://docs.python.org/3.6/library/index.html)。

### 基本工具

- [os](https://docs.python.org/3.6/library/os.html) - 杂项操作系统操作。
- [sys](https://docs.python.org/3.6/library/sys.html) - 系统操作。
- [datetime](https://docs.python.org/3.6/library/datetime.html) - 日期时间操作。
- [glob](https://docs.python.org/3.6/library/glob.html) - 搜索路径名称。

### 实用函数

- [math](https://docs.python.org/3.6/library/math.html) - 数学函数。
- [random](https://docs.python.org/3.6/library/random.html) - （伪）随机数生成器。
- [re](https://docs.python.org/3.6/library/re.html) - 正则表达式。

### 文件格式

- [json](https://docs.python.org/3.6/library/json.html) - 支持处理 JSON 文件。
- [csv](https://docs.python.org/3.6/library/csv.html) - 支持处理 CSV 文件

### 数据对象

- [collections](https://docs.python.org/3.6/library/collections.html) - 容器数据类型。
- [pickle](https://docs.python.org/3.6/library/pickle.html) - 序列化和反序列化（保存和加载复杂对象）。
