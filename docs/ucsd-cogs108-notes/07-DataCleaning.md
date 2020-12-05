
# 七、数据清理

> 原文：[Data Cleaning](https://nbviewer.jupyter.org/github/COGS108/Tutorials/blob/master/07-DataCleaning.ipynb)
> 
> 译者：[飞龙](https://github.com/wizardforcel)
> 
> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

“数据清理”是查找并删除或修复“错误数据”的过程，其中“错误数据”通常指的是损坏和/或不准确的数据点。

```python
# 导入
import numpy as np
import pandas as pd
```

## 缺失值


缺失值只是缺少的数据点。可以通过多种方式指示缺失值。

值可以是字面上的空值，或编码为特殊值，例如 Python `None`或`NaN`，一个 numpy 对象（“非数字”的缩写）。

有时缺失值由任意选择的值指示，例如由某些不可能的值指示，例如`-999`。

缺失值通常需要在进行任何分析之前进行处理。

### Python - None 类型

```python
# Python 具有特殊值“None”，可以编码缺失值或 null 值
dat_none = None


#  None 实际上是它自己的类型
print(type(None))

# <class 'NoneType'>


# 请注意，“None”的作用类似于 null 类型（就好像变量不存在一样）
assert dat_none

'''
---------------------------------------------------------------------------

AssertionError                            Traceback (most recent call last)

<ipython-input-4-95ad9e3fb11e> in <module>()
      1 # Note that 'None' acts like a null type (as if the variable doesn't exist)
----> 2 assert dat_none


AssertionError: 
'''


# 由于 None 是 null 类型，因此当数据中包含 None 时，基本操作将失败
dat_lst = [1, 2, 3, None]
sum(dat_lst) / len(dat_lst)

'''
    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-5-bc3aab645ea1> in <module>()
          1 # Since None is a null type, basic operations will fail when None is in the data
          2 dat_lst = [1, 2, 3, None]
    ----> 3 sum(dat_lst) / len(dat_lst)
    

    TypeError: unsupported operand type(s) for +: 'int' and 'NoneType'
'''
```




### Numpy - NaN


```python
# Numpy也有“非数字”的特殊值 -- NaN
dat_nan = np.nan


# 它实际上是一个特殊的浮点值
type(dat_nan)

# float


# 它不会求值为 null（与 None 不同）
assert dat_nan


# Numpy 实际上有多个版本的 NaN  - 但它们实际上都是一样的。
np.nan is np.NaN is np.NAN

# True


# NaN 值不会失败（与 None 不同）但它们将返回未定义（NaN）的答案
dat_a = np.array([1, 2, 3, np.nan])
print(np.mean(dat_a))

# nan


# 你可以告诉 numpy 进行计算，忽略 NaN 值，但你必须明确告诉它这样做
np.nanmean(np.array([1, 2, 3, np.nan]))

# 2.0
```

## 数据清理的“艺术”

处理缺失数据是一个决策点：你需要做什么？
- 你丢弃了观测吗？
  - 如果这需要放弃大量观测怎么办？
- 你保留它，但在任何计算中忽略它？
  - 如果你在不同的计算中得到不同的 N，怎么办？
- 你重新编码那个数据点吗？
  - 你把它重新编码为什么？

## 不可能的值

数据清理包括检查和处理不可能的值。由于编码或数据输入错误，可能会出现不可能的值。

请注意，数据集还可能将缺失的数据编码为特殊值 - 例如，使用`-999`表示缺少的年龄。

这些都必须处理，否则会扭曲你的结果。

## Pandas 中的数据清理

示例问题：我们有两个单独的文件，它们共同拥有一组人的 id 号，年龄，体重和身高。

让我们假设最终，我们对年龄与身高的关系感兴趣（老年人萎缩真的是真的吗？？）

数据文件：
- `messy_dat.json`，有 id 和身高信息
- `messy_dat.csv`，有 id，年龄和体重信息

```python
# 加载 json 文件
df1 = pd.read_json('files/messy_dat.json')

# 由于JSON文件按字母顺序读取列，因此重新排列列
df1 = df1[['id', 'height']]


# 查看数据。 我们有 NaN 值！
df1
```

|  | id | height |
| --- | --- | --- |
| 0 | 1 | 168.0 |
| 1 | 2 | 155.0 |
| 2 | 3 | NaN |
| 3 | 4 | 173.0 |


```python
# 让我们用 pandas 来丢弃 NaN 值
# 注意 inplace 参数：这将操作我们调用的数据帧
# 而不是返回并将数据帧重新保存到新变量
df1.dropna(inplace=True)


# 丢弃 NaN 后检查数据
df1
```

|  | id | height |
| --- | --- | --- |
| 0 | 1 | 168.0 |
| 1 | 2 | 155.0 |
| 3 | 4 | 173.0 |

```python
# 读入 csv 数据文件
df2 = pd.read_csv('files/messy_dat.csv')


# 检查数据
df2
```

|  | id | age | weight |
| --- | --- | --- | --- |
| 0 | 1 | 20 | 11.0 |
| 1 | 2 | 27 | NaN |
| 2 | 3 | 25 | 14.0 |
| 3 | 4 | -999 | 12.0 |


请注意，我们有另一个 NaN 值！ 但是，它位于体重列中，我们实际上并不计划将其用于当前分析。 如果我们从这个数据框中删除 NaN，我们实际上拒绝了好的数据 - 因为我们将放弃记录 1，他实际上确实有我们需要的年龄和身高信息。

```python
# 因此，既然我们不需要它，那么让我们丢弃重量列
df2.drop('weight', axis=1, inplace=True)


# 让我们检查年龄列中是否有任何 NaN 值（我们确实需要）
# isnull() 为每个数据点返回布尔值，指示它是否为 NaN
# 我们可以对布尔数组求和，看看我们有多少个 NaN 值
sum(df2['age'].isnull())

# 0
```

我们需要的数据列中没有任何 NaN 值！ 我们继续吧！

```python
# 现在让我们将数据合并在一起
# 请注意，这里我们指定使用 'id' 列来合并数据
# 这意味着数据点将基于具有相同 ID 的数据点来合并。
df = pd.merge(df1, df2, on='id')


# 检查合并后的数据帧
df
```

|  | id | height | age |
| --- | --- | --- | --- |
| 0 | 1 | 168.0 | 20 |
| 1 | 2 | 155.0 | 27 |
| 2 | 4 | 173.0 | -999 |

```python
# 查看基本的描述性统计量，看看事情是否合理
df.describe()
```

|  | id | height | age |
| --- | --- | --- | --- |
| count | 3.000000 | 3.000000 | 3.000000 |
| mean | 2.333333 | 165.333333 | -317.333333 |
| std | 1.527525 | 9.291573 | 590.351026 |
| min | 1.000000 | 155.000000 | -999.000000 |
| 25% | 1.500000 | 161.500000 | -489.500000 |
| 50% | 2.000000 | 168.000000 | 20.000000 |
| 75% | 3.000000 | 170.500000 | 23.500000 |
| max | 4.000000 | 173.000000 | 27.000000 |

所以，看起来我们的平均年龄约是 300....

这似乎不对。在数据收集的某些时刻，缺失的年龄值似乎已编码为`-999`。我们需要处理这些数据。

```python
# 丢弃所有带有不可能年龄的行
df = df[df['age'] > 0]


# 那么实际的平均年龄是多少？
df['age'].mean()

# 23.5


# 查看清理过的数据帧！它现在准备好进行真正的分析了！
df
```


|  | id | height | age |
| --- | --- | --- | --- |
| 0 | 1 | 168.0 | 20 |
| 1 | 2 | 155.0 | 27 |

### 数据清理注解

这实际上只是数据清理的开始 - 将数据转换为适合分析的形状，可以包括任何东西

提示：

- 阅读你拥有的数据集的任何文档
  - 像缺失值这样的东西可能是任意编码的，但应该（希望）记录在某处
- 检查数据类型是否符合预期。如果你正在阅读混合类型数据，请确保最终得到正确的编码
- 可视化你的数据！看看分布是否似乎合理
- 检查基本统计量。`df.describe()`可以让你感觉到，某些东西是否真的偏斜了
- 请记住你的数据收集方式。
  - 如果任何东西来自将信息输入表格的人类，这可能需要大量清洁
    - 修复数据输入错误（错别字）
    - 使用不同的单位/格式/惯例处理输入
- 清理这类数据可能需要更多的手工工作（因为错误很可能是特殊的）

请注意，在许多实际情况中，可视地扫描数据表来查找丢失或错误的数据，可能是难以处理的，和/或非常低效。查看你的数据可能需要查看分布和描述性统计量，而不是原始数据。

Quartz 有一个有用的[错误数据指南](https://github.com/Quartz/bad-data-guide),[Pandas 教程](http://pandas.pydata.org/pandas-docs/stable/tutorials.html)有很多相关资料，包括数据清理的章节 (#7)。
