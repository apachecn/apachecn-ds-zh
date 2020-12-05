
# 六、数据整理

> 原文：[Data Wrangling](https://nbviewer.jupyter.org/github/COGS108/Tutorials/blob/master/06-DataWrangling.ipynb)
> 
> 译者：[飞龙](https://github.com/wizardforcel)
> 
> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

“数据整理”通常是指将原始数据，转换为可用于你感兴趣的分析的可用形式，包括加载，聚合和格式化。

注意：在整个笔记本中，我们将使用 '!' 运行 shell 命令`cat`，来打印出示例数据文件的内容。

## Python I/O


Python 有一些基本的 I / O （输入/输出）工具。



这是 I / O 的官方 Python [文档](https://docs.python.org/3/library/io.html)。

```python
# 查看示例数据文件
!cat files/dat.txt

'''
First line of data

Second line of data
'''


# 首先，显式打开文件对象进行读取
f_obj = open('files/dat.txt', 'r')

# 然后，你可以遍历文件对象，抓取每行数据
for line in f_obj:
    # 请注意，我正在删除每行末尾的新行标记（'\n'）
    print(line.strip('\n'))

# 完成后，必须关闭文件对象
f_obj.close()

'''
First line of data
Second line of data
'''


# 由于打开和关闭文件基本上总是在一起，因此有一个快捷方式来完成它们
# 使用 'with' 关键字打开文件，文件对象将在代码块的末尾自动关闭
with open('files/dat.txt', 'r') as f_obj:
    for line in f_obj:
        print(line.strip('\n'))
        
'''
First line of data
Second line of data
'''
```

    

Python 的 I / O是一种非常“低级”的读取数据文件的方法，并且通常需要大量工作来整理读取文件的细节 - 例如，在上面的示例中，明确地处理新行字符。

只要你有合理的结构化数据文件，使用标准化的文件类型，你就可以使用更高级的函数来处理很多这些细节 - 例如，将数据直接加载到 pandas 数据对象中。

## Pandas I/O


Pandas 有一系列函数，可以将标准文件类型的整个文件自动读取到 pandas 对象中。


这是 I / O 的官方 Pandas [文档](http://pandas.pydata.org/pandas-docs/stable/io.html)。

```python
import pandas as pd


# Tab 补全来检查所有可用的读取函数
pd.read_
```

## 文件类型


存在许多不同的标准化（和非标准化）文件类型，其中可以存储数据。在这里，我们将从检查 CSV 和 JSON 文件开始。

### CSV 文件

“逗号分隔值”文件存储数据，以逗号分隔。把它们想象成列表。

这是[维基百科](https://en.wikipedia.org/wiki/Comma-separated_values)中 CSV 文件的更多信息。

```python
# 我们来看一下 csv 文件（以纯文本打印）
!cat files/dat.csv

'''
1, 2, 3, 4

5, 6, 7, 8

9, 10, 11, 12
'''
```

#### Python 中的 CSV 文件

```python
# Python 有一个专门用于处理 csv 的模块
import csv


# 我们可以使用 csv 模块读取我们的文件
with open('files/dat.csv') as csvfile:
    csv_reader = csv.reader(csvfile, delimiter=',')
    for row in csv_reader:
        print(', '.join(row))
        
'''
1,  2,  3,  4
5,  6,  7,  8
9,  10,  11,  12
'''
```

#### Pandas 中的 CSV 文件

```python
# Pandas 也具有直接加载 csv 数据的函数
pd.read_csv?


# 让我们读入我们的 csv 文件
pd.read_csv(open('files/dat.csv'), header=None)
```

|  | 0 | 1 | 2 | 3 |
| --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 |
| 1 | 5 | 6 | 7 | 8 |
| 2 | 9 | 10 | 11 | 12 |


### JSON 文件


JavaScript 对象标记文件可以存储层次化键/值对。把它们想象成字典。

这是来自 [wikipedia](https://en.wikipedia.org/wiki/JSON) 的 JSON 文件的更多信息。


```python
# 我们来看一下 json 文件（以纯文本打印）
!cat files/dat.json

'''
{

  "firstName": "John",

  "age": 53

}
'''


# 将 json 看做与字典相似
d = {'firstName': 'John', 'age': '53'}
print(d)

# {'firstName': 'John', 'age': '53'}
```


#### Python 中的 JSON 文件


```python
# Python 还有一个用于处理 json 的模块
import json


# 加载 json 文件
with open('files/dat.json') as dat_file:    
    dat = json.load(dat_file)


# 检查加载的数据类型
print(type(dat))

# <class 'dict'>
```

#### Pandas 中的 JSON 文件

```python
# Pandas 还支持读取 json 文件
pd.read_json?


# 你可以使用 pandas 读取 json 格式的字符串
# 请注意，这里我指定将其作为 pd.Series 读取，因为只有一行数据
pd.read_json('{ "first": "Alan", "place": "Manchester"}', typ='series')

'''
first          Alan
place    Manchester
dtype: object
'''


# 用 pandas 读入我们的 json 文件
pd.read_json(open('files/dat.json'), typ='series')

'''
age            53
firstName    John
dtype: object
'''
```

