# requests 模块

Python 内置了 requests 模块，该模块主要用来发 送 HTTP 请求，requests 模块比 urllib 模块更简洁。

## 简单的爬取

```python
import requests

if __name__ == "__main__":

    # 1. 指定url
    url = 'https://www.baidu.com/'

    # 2. 发起请求
    res = requests.get(url=url)

    # 3. 获取响应数据
    r_text = res.content.decode()

    # 4. 持久化存储
    with open('./baidu.html', 'w', encoding=res.apparent_encoding) as fp:

        # fp.write(res.text)
        fp.write(r_text)

    # 打印响应内容
    # res.text乱码根据网页自动选择编码容易出错
    # res.content.decode() decode默认utf-8码解决乱码问题
    # * 拓展 decode是解码   res.content是二进制数据
    print(res.content)  # 二进制    数据 图片 音频 视频都是二进制数据,这些数据不能用decode()

    print('done!')
```

## UA伪装

> UA：UserAgent(请求载体的身份标识)
>
> UA检测：门户网站的服务器会检测对应请求的载体身份标识,如果检测到请求的载体身份标识为某一款浏览器
>
> 说明该请求是一个正常的请求。但是，如果检测到请求的戴体身份标识不是基于某一款浏览器的，
>
> 则表示该请求为不正常的请求(爬虫)，则服务器端就很有可能拒绝该次请求。

UA伪装：让爬虫对应的请求载体身份标识伪装成某一款浏览器

```python
# UA伪装：将对应的User-Agent封装到一个字典中
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0'
}
```

## 动态爬取

```python
import requests

if __name__ == "__main__":
    # url = "https://search.bilibili.com/all?keyword={query}"
    url = "https://search.bilibili.com/all"

    # 处理url携带的参数：封装到字典中
    key = input("Enter a keyword:")
    param = {
        'keyword': key
    }
    res = requests.get(url=url, params=param)

    filename = key + '.html'

    with open(file='./Temp/' + filename, mode='w', encoding='utf-8') as fp:
        fp.write(res.content.decode())
    print('done!')
```



# XPath

## 术语

**节点（Node）**

在 XPath 中，有**七种类型的节点：元素、属性、文本、命名空间、处理指令、注释以及文档（根）节点**。XML 文档是被作为节点树来对待的。树的根被称为文档节点或者根节点。

请看下面这个 XML 文档：

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<bookstore>
<book>
  <title lang="en">Harry Potter</title>
  <author>J K. Rowling</author> 
  <year>2005</year>
  <price>29.99</price>
</book>
</bookstore>
```

上面的XML文档中的节点例子：

```
<bookstore> （文档节点）
<author>J K. Rowling</author> （元素节点）
lang="en" （属性节点） 
```

**基本值（或称原子值，Atomic value）**

基本值是无父或无子的节点。

基本值的例子：

```
J K. Rowling
"en"
```

**项目（Item）**

项目是基本值或者节点。

### 节点关系

**父（Parent）**

每个元素以及属性都有一个父。

在下面的例子中，book 元素是 title、author、year 以及 price 元素的父：

```xml
<book>
  <title>Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>
```

**子（Children）**

元素节点可有零个、一个或多个子。

在下面的例子中，title、author、year 以及 price 元素都是 book 元素的子：

```xml
<book>
  <title>Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>
```

**同胞（Sibling）**

拥有相同的父的节点

在下面的例子中，title、author、year 以及 price 元素都是同胞：

```xml
<book>
  <title>Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>
```

**先辈（Ancestor）**

某节点的父、父的父，等等。

在下面的例子中，title 元素的先辈是 book 元素和 bookstore 元素：

```xml
<bookstore>

<book>
  <title>Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>

</bookstore>
```

**后代（Descendant）**

某个节点的子，子的子，等等。

在下面的例子中，bookstore 的后代是 book、title、author、year 以及 price 元素：

```xml
<bookstore>

<book>
  <title>Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>

</bookstore>
```

## 语法

### XML 实例文档

我们将在下面的例子中使用这个 XML 文档。

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>

<bookstore>

<book>
  <title lang="eng">Harry Potter</title>
  <price>29.99</price>
</book>

<book>
  <title lang="eng">Learning XML</title>
  <price>39.95</price>
</book>

</bookstore>
```

### 选取节点

XPath 使用路径表达式在 XML 文档中选取节点。节点是通过沿着路径或者 step 来选取的。

**下面列出了最有用的路径表达式：**

| 表达式   | 描述                                                       |
| -------- | ---------------------------------------------------------- |
| nodename | 选取此节点的所有子节点。                                   |
| /        | 从根节点选取。                                             |
| //       | 从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。 |
| .        | 选取当前节点。                                             |
| ..       | 选取当前节点的父节点。                                     |
| @        | 选取属性。                                                 |

**实例**

在下面的表格中，我们已列出了一些路径表达式以及表达式的结果：

| 路径表达式      | 结果                                                         |
| --------------- | ------------------------------------------------------------ |
| bookstore       | 选取 bookstore 元素的所有子节点。                            |
| /bookstore      | 选取根元素 bookstore。 注释：假如路径起始于正斜杠( / )，则此路径始终代表到某元素的绝对路径！ |
| bookstore/book  | 选取属于 bookstore 的子元素的所有 book 元素。                |
| //book          | 选取所有 book 子元素，而不管它们在文档中的位置。             |
| bookstore//book | 选择属于 bookstore 元素的后代的所有 book 元素，而不管它们位于 bookstore 之下的什么位置。 |
| //@lang         | 选取名为 lang 的所有属性。                                   |

### 谓语（Predicates）

谓语用来查找某个特定的节点或者包含某个指定的值的节点。

谓语被嵌在方括号中。

**实例**

在下面的表格中，我们列出了带有谓语的一些路径表达式，以及表达式的结果：

| 路径表达式                         | 结果                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| /bookstore/book[1]                 | 选取属于 bookstore 子元素的第一个 book 元素。                |
| /bookstore/book[last()]            | 选取属于 bookstore 子元素的最后一个 book 元素。              |
| /bookstore/book[last()-1]          | 选取属于 bookstore 子元素的倒数第二个 book 元素。            |
| /bookstore/book[position()<3]      | 选取最前面的两个属于 bookstore 元素的子元素的 book 元素。    |
| //title[@lang]                     | 选取所有拥有名为 lang 的属性的 title 元素。                  |
| //title[@lang='eng']               | 选取所有 title 元素，且这些元素拥有值为 eng 的 lang 属性。   |
| /bookstore/book[price>35.00]       | 选取 bookstore 元素的所有 book 元素，且其中的 price 元素的值须大于 35.00。 |
| /bookstore/book[price>35.00]/title | 选取 bookstore 元素中的 book 元素的所有 title 元素，且其中的 price 元素的值须大于 35.00。 |
