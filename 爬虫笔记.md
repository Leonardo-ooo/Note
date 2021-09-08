爬虫笔记



```python
#爬虫简单流程
baseurl = "https://movie.douban.com/top250"
#1.爬取网页
#2.解析数据
#3.保存数据
```

urllib库

```python

#get方式获取请求
urllib.request.urlopen(__url)	
#post方式获取请求
#必须发送给服务器一些数据（bytes类型）
#发送给服务器的信息必须为byte类型
#将dict类型参数转化为query_string格式（key=value&key=value），并且将中文转码，最终会转换为bytes(字节流）类型
data = urllib.parse.urlencode("utf-8")
urllib.request.urlopen(__url, data)


#模拟浏览器以post的方式发送请求
#建立一个headers字典
headers = {xx:xx}
#创建一个request对象
request = urllib.request.Request(url=baseurl, headers=head, method="POST")
#发起请求并保存响应数据
response = urllib.request.urlopen(request, timeout=1)

response.read().decode('utf-8')	#获取网页源码，编码方式为utf-8
response.status	#获取https状态码
response.getheaders()	#获取响应头列表，列表元素为元组
```

bs4库

```python
- Tag
- NavigableString
- BeatifulSoup
- Comment


#用二进制方式读取html文件，读到的内容放入BeautiSoup解析器解析生成一个bs4对象
file = open("xxx.html", "rb")
#测试发现第一个参数不是二进制编码也可以？但会出现中文乱码
bs = BeautifulSoup(file.read(), "html.parser")


#bs里有各种Tag属性，作用是读取第一次出现的对应标签的所有内容
print(bs.title)
#输出：<title>百度一下，你就知道</title>
#也可以获取Tag里的Tag
bs.div.div.a


#bs的Tag属性里有NavigableString，即跳过标签显示标签间内容的字符串(也会跳过标签内的标签)
print(bs.title.string)
#如果该标签内容为注释，那么得到的类型为Comment，得到的结果为去掉<!-- -->的字符串
#输出：百度一下，你就知道


#Tag属性里还有attributes属性，用来获取对应标签的所有属性及其属性值的字典
print(a.attrs)
#输出：{'class': ['toindex'], 'href': '/'}

```

BeautifulSoup.Tag对象的常用属性

```python
#stripped_strings 和string一样，但是去除多余的空白内容
#strings 获取子孙节点的内容的生成器（迭代器）
#contents获取所有内容的列表
#children获取所有子节点的生成器(迭代器)
#descendants获取所有子孙节点的生成器(迭代器)
#parent获取父亲标签
#parents递归获取所有父亲标签
#previous_sibling获取同级的上一个节点
#previous_siblings获取所有同级前面节点的生成器
#next_sibling	同上理
#next_sibling	同上理
```

BeautifulSoup文档搜索方法

```python
#查找符合条件的节点，返回列表
#name参数表示标签，attrs表示属性，text表示内容
find_all(self, name=None, attrs={}, recursive=True, text=None,limit=None, **kwargs)
#name参数为标签名；attrs参数为属性的字典；
#kwargs参数为关键字参数，可以指定固定属性的值
find_all(class_=True) #查找带class属性的标签(class加下划线避免与py关键字冲突)


#find_all(函数名不要括号) 函数定义参数为tag(find_all方法自动传入)，返回值为bool， 获取所有符合条件的标签列表。
def f(tag):
    return tag.has_attr("style")
a = bs.find_all(f)
print(a)
#输出所有带有style属性的标签


#选择器select()返回标签
select("Tag"), select(".class")，select("#id")
select("Tag[class='xxx']")	#通过属性查找
select("Tag > Tag") #查找子节点
select("Tag ~ Tag") #向下查找兄弟节点
```

re正则

```python
#匹配包含__str的文本
compile("__str")
# .表示任何单个字符
# []字符集，对单个字符给出取值范围
# [^]非字符集，对单个字符给出排除范围
# *前一字符出现任意次（包括0次）
# +前一字符出现一次或任意次
# {m} 前一个字母必须出现m次
# {m, n} 前一个字母必须出现m到n次
# ?前一字符出现一次或不出现
# |左右表达式任意一个
#() 内部只能使用|
# ^xxx  xxx必须为字符串开头
# xxx$  xxx必须为字符串结尾
# \d 数字，等价于[0-9]
# \w 单词字符，等价于[A-Za-Z0-9]
#\s 空白字符


#返回一个匹配正则_str的Match对象，若不匹配则返回None
re.compile("_str").search("xxx") 
re.search("_str", "xxx") 

#返回一个匹配正则_str的列表
re.findall("_str", "xxx") 

#找到xxx中正则_str，用 s 替换后的字符串
re.sub("_str", "s", "xxx")
```

