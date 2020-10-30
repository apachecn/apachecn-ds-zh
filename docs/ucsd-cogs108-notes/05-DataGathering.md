
# 五、数据收集

> 原文：[Data Gathering](https://nbviewer.jupyter.org/github/COGS108/Tutorials/blob/master/05-DataGathering.ipynb)
> 
> 译者：[飞龙](https://github.com/wizardforcel)
> 
> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)

数据收集只是将数据收集在一起的过程。

本笔记本涵盖了可用于收集分析数据的策略。

如果你想继续进行数据分析（使用提供的数据），你可以转到下一个教程，稍后再回到本教程。

数据收集可以包括启动数据收集项目，网络抓取，从数据库中提取，批量下载数据等任何内容。

它甚至可能只是简单地打电话给某人询问你是否可以使用他们的一些数据。

## 在哪里获取数据

### 网络

网络上绝对是数据或获取数据的方式，可以通过托管**数据仓库**，从中下载数据，通过**API**，从特定应用程序请求特定数据，或作为数据本身，你可以使用**网络爬虫**直接从网站提取数据。

### 除了网络

并非所有数据都在网络上编入索引或可访问，至少不是公开的。

有时查找数据意味着在任何地方追逐数据。

如果你需要某些特定数据，你可以尝试找出可能拥有该数据的人，并与他们联系，看看它是否可用。

### 数据收集技巧

根据你的收集方法，你可能需要执行以下某些组合：

- 从仓库下载数据文件
- 将数据文件读入 python
- 使用 API
- 查询数据库
- 打电话给某人，让他们给你发一个硬盘

## 数据仓库


数据仓库基本上只是存储数据的地方。出于我们的目的，它是一个可以从中下载数据的地方。

[项目材料](https://github.com/COGS108/Projects)中包含了一个精选列表，他包含良好的数据源。

## 数据库

数据库是有组织的数据集合。 更正式地说，“数据库”是指一组相关数据及其组织方式。

### 结构化查询语言 - SQL

SQL（发音为“sequel”）是一种用于与数据库“通信”的语言，用于查询从中请求特定数据。

[这里](http://www.sqlcourse.com/intro.html)有一个 SQL 的实用介绍和教程，以及[这里](http://www.cheat-sheets.org/sites/sql.su/）和[这里](http://www.sqltutorial.org/wp-content/uploads/2016/04/SQL-cheat-sheet.pdf)有一些有用的“备忘单”。

SQL 是与关系数据库交互的标准且最流行的方式。

注意：其余教程都没有假定或需要任何 SQL 知识。

如果需要，或者它是否与访问要分析的数据相关，可以查看它，但这组教程不需要它。

## 应用程序接口 (API)

API 基本上是软件与软件通信的一种方式 - 它是为软件设计的应用程序/网站/数据库的接口。

有关API的简单说明请参见[这里](https://medium.freecodecamp.com/what-is-an-api-in-english-please-b880a3214a82)；更广泛，更技术性的概述参见[这里](https://medium.com/@mattburgess/apis-a-basic-primer-f8250602597d)。

API提供了许多功能 - 你可以向应用程序发送请求开执行各种操作。 事实上，任何设计用于以编程方式使用的接口都是 API，包括例如用于使用代码包的接口。

API 执行和提供的许多功能之一是，查询和访问特定应用/数据库中的数据的方法。使用 API 进行数据收集的好处是，它们通常以结构良好的格式返回数据，这些格式相对容易分析。

### 从 Python 启动 URL 请求


```python
# 导入
# requests 允许你从 python 发出 http 请求
import requests
import pandas as pd
```

实际上，API 通常是返回原始数据（json 或 XML）的特殊 URL，而不是为人类读者呈现的网页（html）。查找特定 API 的文档，了解如何发送请求来访问所需数据。例如，让我们试试 Github API。

```python
# 使用 Github API 从特定用户请求数据
page = requests.get('https://api.github.com/users/tomdonoghue')


# 在这种情况下，我们得到的内容是一个 json 文件
page.content

# b'{"login":"TomDonoghue","id":7727566,"avatar_url":"https://avatars0.githubusercontent.com/u/7727566?v=4","gravatar_id":"","url":"https://api.github.com/users/TomDonoghue","html_url":"https://github.com/TomDonoghue","followers_url":"https://api.github.com/users/TomDonoghue/followers","following_url":"https://api.github.com/users/TomDonoghue/following{/other_user}","gists_url":"https://api.github.com/users/TomDonoghue/gists{/gist_id}","starred_url":"https://api.github.com/users/TomDonoghue/starred{/owner}{/repo}","subscriptions_url":"https://api.github.com/users/TomDonoghue/subscriptions","organizations_url":"https://api.github.com/users/TomDonoghue/orgs","repos_url":"https://api.github.com/users/TomDonoghue/repos","events_url":"https://api.github.com/users/TomDonoghue/events{/privacy}","received_events_url":"https://api.github.com/users/TomDonoghue/received_events","type":"User","site_admin":false,"name":"Tom","company":"UC San Diego","blog":"tomdonoghue.github.io","location":"San Diego","email":null,"hireable":null,"bio":"Cognitive Science Grad Student @ UCSD. \\r\\nOn Twitter @TomDonoghue","public_repos":13,"public_gists":0,"followers":13,"following":35,"created_at":"2014-05-28T20:20:48Z","updated_at":"2018-01-09T04:15:59Z"}'


# 我们可以用 pandas 读取 json 数据
pd.read_json(page.content, typ='series')

'''
avatar_url             https://avatars0.githubusercontent.com/u/77275...
bio                    Cognitive Science Grad Student @ UCSD. \r\nOn ...
blog                                               tomdonoghue.github.io
company                                                     UC San Diego
created_at                                          2014-05-28T20:20:48Z
email                                                               None
events_url             https://api.github.com/users/TomDonoghue/event...
followers                                                             13
followers_url          https://api.github.com/users/TomDonoghue/follo...
following                                                             35
following_url          https://api.github.com/users/TomDonoghue/follo...
gists_url              https://api.github.com/users/TomDonoghue/gists...
gravatar_id                                                             
hireable                                                            None
html_url                                  https://github.com/TomDonoghue
id                                                               7727566
location                                                       San Diego
login                                                        TomDonoghue
name                                                                 Tom
organizations_url          https://api.github.com/users/TomDonoghue/orgs
public_gists                                                           0
public_repos                                                          13
received_events_url    https://api.github.com/users/TomDonoghue/recei...
repos_url                 https://api.github.com/users/TomDonoghue/repos
site_admin                                                         False
starred_url            https://api.github.com/users/TomDonoghue/starr...
subscriptions_url      https://api.github.com/users/TomDonoghue/subsc...
type                                                                User
updated_at                                          2018-01-09T04:15:59Z
url                             https://api.github.com/users/TomDonoghue
dtype: object
'''
```

这个[列表](http://www.webopedia.com/TERM/A/API.html)包含常用和可用 API 的集合。

## 网络抓取

网络抓取是指你（以编程方式）从网站提取数据。[Wikipedia](https://en.wikipedia.org/wiki/Web_scraping) 有一个关于网页抓取的有用页面。

请注意，以下部分使用`BeautifulSoup`模块，该模块不是标准 anaconda 发行版的一部分。

如果你没有`BeautifulSoup`，并希望让它运行此部分，你可以取消注释下面的单元格并运行它，来当前的 Python 环境中安装`BeautifulSoup`。 你只需要这样做一次。

```python
# 导入 sys
# !conda install --yes --prefix {sys.prefix} beautifulsoup4


# 导入 BeautifulSoup
from bs4 import BeautifulSoup


# 设置我们希望抓取的页面的 URL
site_url = 'https://en.wikipedia.org/wiki/Data_science'

# 启动 URL 请求，来获取页面
page = requests.get(site_url)


# 打印出已爬取网页的前 1000 个字符
page.content[0:1000]

# b'<!DOCTYPE html>\n<html class="client-nojs" lang="en" dir="ltr">\n<head>\n<meta charset="UTF-8"/>\n<title>Data science - Wikipedia</title>\n<script>document.documentElement.className = document.documentElement.className.replace( /(^|\\s)client-nojs(\\s|$)/, "$1client-js$2" );</script>\n<script>(window.RLQ=window.RLQ||[]).push(function(){mw.config.set({"wgCanonicalNamespace":"","wgCanonicalSpecialPageName":false,"wgNamespaceNumber":0,"wgPageName":"Data_science","wgTitle":"Data science","wgCurRevisionId":822535327,"wgRevisionId":822535327,"wgArticleId":35458904,"wgIsArticle":true,"wgIsRedirect":false,"wgAction":"view","wgUserName":null,"wgUserGroups":["*"],"wgCategories":["Use dmy dates from December 2012","Information science","Computer occupations","Computational fields of study","Data analysis"],"wgBreakFrames":false,"wgPageContentLanguage":"en","wgPageContentModel":"wikitext","wgSeparatorTransformTable":["",""],"wgDigitTransformTable":["",""],"wgDefaultDateFormat":"dmy","wgMonthNames":["","Ja'
```

请注意，抓取的网页的来源是一堆杂乱的 HTML。

那里有很多信息，但没有明确的组织。虽然页面中有一些结构，由 HTML 标签等描述，但我们只需要使用它们来解析数据。 我们可以使用 BeautifulSoup 来做到这一点，它接收这样的杂乱文档，并根据指定的格式解析它们。

```python
# 使用 Beautiful Soup 和 html 解析器解析网页
soup = BeautifulSoup(page.content, 'html.parser')


# 有了解析的 soup 对象，我们可以选择网页的特定片段

# 打印页面标题
print('TITLE: \n')
print(soup.title)

# 打印第一个 p 标签
print('\nP-TAG:\n')
print(soup.find('p'))

'''
TITLE: 

<title>Data science - Wikipedia</title>

P-TAG:

<p><b>Data science</b>, also known as <b>data-driven science</b>, is an interdisciplinary field of scientific methods, processes, and systems to extract [knowledge](/wiki/Knowledge) or insights from [data](/wiki/Data) in various forms, either structured or unstructured,<sup class="reference" id="cite_ref-:0_1-0">[[1]](#cite_note-:0-1)</sup><sup class="reference" id="cite_ref-2">[[2]](#cite_note-2)</sup> similar to [data mining](/wiki/Data_mining).</p>
'''
```

从 soup 对象中，你可以更有条理地探索页面，并以这种方式提取你感兴趣的特定成分。

请注意，在其他方面它仍然是“混乱的”，因为可能会或可能不会有关于页面布局的系统结构，并且仍然可能需要大量工作才能从中提取你想要的特定信息。

### API vs 网络抓取

网络抓取与使用 API 不同，即使可以通过互联网访问许多 API。网络抓取的不同之处在于，你（以编程方式）访问互联网，并提取感兴趣的数据。

注意：

请注意，从网站上抓取数据本身（不使用 API）通常可能是一个复杂的项目 - 网站抓取可能需要进行大量调整才能获得所需的数据。

请注意，网站上显示的数据可能结构不合理，或者采用有组织的格式，便于分析。

如果你尝试抓取网站，还要确保你可以抓取数据，并遵循网站服务条款。
