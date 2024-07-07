# Python3

# 安装

## [官网](https://www.python.org/downloads/)

## [conda](https://mirror.tuna.tsinghua.edu.cn/help/anaconda/)

**注意**：conda本身是一个通用的包管理系统（*general-purpose package management system*），只是可以很好的管理python的package
这儿有一篇博客解释了conda与pip的误解：https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/

+ Anaconda：是一个用于科学计算的 Python 发行版，包含了众多流行的科学计算、数据分析的 Python 包
+ Miniconda：Anaconda 的轻量级替代，只含有conda、python和一些少数必要的package
  从清华源安装会看到x86_64、aarch64等[CPU架构](https://zhuanlan.zhihu.com/p/658199487)，你可以通过命令 `uname -m`(Linux) 或 `wmic os get OSArchitecture`(Windows)查看自己的系统架构

```text
# 更新所有库
conda upgrade --all
# 更新 conda 自身
conda update conda·
```

+ 镜像

  + conda

    看清华镜像站

    ```命令
    添加镜像源
    conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
    以下命令完成配置的更新：
    conda config --set show_channel_urls yes
    显示已有镜像源
    conda config --show channels
    删除已有镜像源
    conda config --remove channels 源名称或链接
    conda config --remove-key channels  # 删除所有源
    ```

  + pip

    **常用的镜像源地址**

    ```python3
    config = {
        "清华大学": "https://pypi.tuna.tsinghua.edu.cn/simple",
        "中国科技大学": "https://pypi.mirrors.ustc.edu.cn/simple/",
        "豆瓣": "https://pypi.douban.com/simple/",
        "网易": "https://mirrors.163.com/pypi/simple/",
        "阿里云": "https://mirrors.aliyun.com/pypi/simple/",
        "华为云": "https://repo.huaweicloud.com/repository/pypi/simple",
        "腾讯云": "https://mirrors.cloud.tencent.com/pypi/simple"
    }
    ```

    **临时使用**

    ```text
    pip install xxx -i https://pypi.tuna.tsinghua.edu.cn/simple
    ```

    **设置默认**

    ```text
    # 设置默认为国内镜像的方法(需要升级到pip的10.0.0以上)
    python -m pip install --upgrade pip
    # 配置的信息可以在用户家目录的
    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
    ```

+ 配置虚拟环境
  你可以使用pip或者conda创建虚拟环境

  + pip

    打印Python 解释器搜索模块的路径列表

    ```python
    import sys
    from pprint import pprint
    pprint(sys.path)
    ```

    [**创建虚拟环境**](https://docs.python.org/zh-cn/3/library/venv.html)

    `python -m venv tutorial-env`

    这将创建 `tutorial-env` 目录，如果它不存在的话，并在其中创建包含 Python 解释器副本和各种支持文件的目录。

    虚拟环境的常用目录位置是 `.venv`（`python -m venv .venv`）。 这个名称通常会令该目录在你的终端中保持隐藏，从而避免需要对所在目录进行额外解释的一般名称。 它还能防止与某些工具所支持的 `.env` 环境变量定义文件发生冲突。

    ```shell
    python -m venv -h
    usage: venv [-h] [--system-site-packages] [--symlinks | --copies] [--clear] [--upgrade] [--without-pip]
                [--prompt PROMPT] [--upgrade-deps]
                ENV_DIR [ENV_DIR ...]
    ```

    **创建requirements.txt**

    `pip freeze > requirements.txt`

    在 Python 项目中，可以使用 requirements.txt 文件来列出项目所依赖的第三方库及其版本。这个文件使得其他人可以更容易地安装这些依赖项，以便他们可以运行你的应用程序并具有相同的环境设置。

    在生成 requirements.txt 文件之前，你需要确保已激活你的虚拟环境（如果是在虚拟环境中工作的话），并且已经安装了 Python 库。

    + 安装requirements.txt

      当需要创建这个虚拟环境的完全副本，可以创建一个新的虚拟环境，并在其上运行以下命令:

      `pip install -r requirements.txt`

  + conda

    1. 查看env

       `conda info -e`

    2. 创建env

       `conda create --prefix=D:\Code\Anaconda3\envs\py3.9.13 python=3.9.13`

       prefix是自定义位置

       ```
       conda create --prefix=D:\Code\Anaconda3\envs\Svc python=3.8.9
       ```

    **常见命令**

    + (1)查看安装了哪些包

      ```
      conda list
      ```

    + (2)查看环境列表
      如果没有安装虚拟环境，就会显示只有一个base。

      ```
      conda env list
      ```

    + (3)查看默认配置信息
      包括环境路径、下载的包的缓存位置等

      ```
      conda info
      ```

    + (4)创建虚拟环境

      ```
      conda create -n py39 python=3.9
      ```

    + (5)激活虚拟环境

      ```
      Linux环境下执行命令:source activate 虚拟环境名
      windows环境下执行命令:activate 虚拟环境名
      ```

    + (6)删除虚拟环境

      ```
      conda remove -n 虚拟环境名 --all
      ```

    + (7)安装包

      ```
      conda install package_name
      ```

    + (8)关闭虚拟环境

      ```
      Linux环境下执行命令:source deactivate
      Windows环境下执行命令:deactivate 虚拟环境名
      ```

    + (9)安装包

      ```
      conda install package_name
      ```

    + (10)关闭虚拟环境

      ```
      Linux环境下执行命令:source deactivate
      Windows环境下执行命令:deactivate 虚拟环境名
      ```

    + Ctrl+Shift+P 或者 View > Command Palette，打开命令面板
      输入`Python: Select Interpreter`

## Jupyter notebook

Jupyter Notebook 是一个开源的交互式笔记本工具，它允许用户创建和共享文档，其中包含实时的代码、可视化效果、数学方程和解释性文本。它最初是作为 IPython Notebook 而知名的，后来演变成支持多种编程语言的工具（例如 `julia`）。

推荐在vscode里安装[插件](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python-extension-pack)使用jupyter notebook，比在启动网页简单方便（idea或者说pycharm也是支持.ipynb文件的）

### 安装

+ 如果是conda安装的python，首先base环境需要安装jupyter包

  activate

  conda install jupyter

+ envs环境下使用Jupyter notebook需要ipykernel包

  + 安装ipykernel包

    `conda install -n pytorch ipykernel --update-deps --force-reinstall`

    ``--force-reinstall` 参数用于强制重新安装 ipykernel ，以解决可能出现的版本冲突问题。

    注：你如果在vscode里使用jupyter notebook就不需要下一步了（而且它一般会检测你有没有kernel，提示你是否安装）。

  + 将 "pytorch" 环境中安装的 Python 内核添加到 Jupyter Notebook 中

    `python -m ipykernel install --user --name pytorch --display-name "Python (pytorch)"`

    这样，在 Jupyter Notebook 中就可以看到一个新的内核选项，名称为 "Python (pytorch)"，它将使用 "pytorch" 环境中的 Python 解释器来执行代码。

### 原生快捷键

notebook 有很多快捷键，可以通过菜单中的 `Help->Keyboard Shortcuts` 查看，也可以直接用快捷键 `Ctrl+Shift+P` 查看。下面简单介绍一些快捷键：

- 编辑模式和命令模式可以通过 `Esc` 和 `Enter` 进行转换，一般是按 `Esc` 进入命令模式，`Enter` 进入编辑模式

在**命令模式**下：

- 在 `cell` 之间上下浏览采用上下箭头，或者 `Up` 和 `Down` 键
- `A` 表示在当前 `cell` 上方插入一个新的 `cell` ，而 `B` 则是下方插入新的`cell`
- `M` 表示变为 `Markdown cell` ，而 `Y` 是表示变为 `code cell`
- 连续按两次 `D` 是删除当前 `cell`
- `Z` 是撤销操作
- `Shift` 加上 `Up` 或者 `Down` 可以一次选择多个 `cells` ，接着采用 `Shift + M` 可以合并多个 `cells`

# 基础语法

## 编码

默认情况下，Python 3 源码文件以 **UTF-8** 编码，所有字符串都是 unicode 字符串。

## 标识符

- 第一个字符必须是字母表中字母或下划线 _ 。(意思是不能数字开头)

  ```python
  >>> 1_yeah = 'yeah'
  SyntaxError: invalid decimal literal
  ```

- 标识符的其他的部分由字母、数字和下划线组成。

- 标识符对大小写敏感。

在 Python 3 中，可以用中文作为变量名，非 ASCII 标识符也是允许的了。

```python
>>> 我是sb = 'sb'
>>> 我是sb
'sb'
```



## python保留字

保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字：

```python
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', '__peg_parser__', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## 注释

```python
# 单行注释

'''
多行注释1
'''

"""
多行注释2
"""
```

## 行与缩进

python最具特色的就是使用缩进来表示代码块，不需要使用大括号 {} ，当然也不需要分号;。

缩进的空格数是可变的，但是同一个代码块的语句必须包含相同的缩进空格数。实例如下：

```python
if True:
    print ("True")
else:
    print ("False")
```

以下代码最后一行语句缩进数的空格数不一致，会导致运行错误：

## 实例

```python
if True:
    print ("Answer")
    print ("True")
else:
    print ("Answer")
  print ("False")    # 缩进不一致，会导致运行错误
```

以上程序由于缩进不一致，执行后会出现类似以下错误：

```python
SyntaxError: unindent does not match any outer indentation level
```

## 多行语句

Python 通常是一行写完一条语句，但如果语句很长，我们可以使用反斜杠 \ 来实现多行语句，例如：

```python
total = item_one + \
        item_two + \
        item_three
```

在  [], {}, 或 () 中的多行语句，不需要使用反斜杠 \，例如：

```python
total = ['item_one', 'item_two', 'item_three',
        'item_four', 'item_five']
```

## 数字(Number)类型

python中数字有四种类型：整数、布尔型、浮点数和复数。

> [type()](https://www.runoob.com/python/python-func-type.html)函数如果你只有第一个参数则返回对象的类型，三个参数返回新的类型对象。

- **int** (整数), 如 1, 只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。

  ```python
  >>> x = 2
  >>> type(x)
  <class 'int'>
  ```

- **bool** (布尔), 如 True。

  ```python
  >>> type(True)
  <class 'bool'>
  ```

- **float** (浮点数), 如 1.23、3E-2

  ```python
  >>> type(math.pi)
  <class 'float'>
  ```

- **complex** (复数), 如 1 + 2j、 1.1 + 2.2j

  ```python
  >>> c = 1 + 2j
  >>> type(c)
  <class 'complex'>
  ```


## 字符串(String)

- Python 中单引号 ' 和双引号 " 使用完全相同。

- 使用三引号(''' 或 """)可以指定一个多行字符串。

  ```python
  # 我以为就是注释的意思，其实不是
  >>> paragraph = """这是一个段落，
  可以由多行组成"""
  >>> paragraph
  '这是一个段落，\n可以由多行组成'
  ```



- 转义符 \。

  ```python
  "\n \t \a \b"
  ```

- 反斜杠可以用来转义，使用 r 可以让反斜杠不发生转义。 如 **r"this is a line with \n"** 则 \n 会显示，并不是换行。

  ```python
  >>> print(r"this is a line with \n")
  this is a line with \n
  ```

- 按字面意义级联字符串，如 **"this " "is " "string"** 会被自动转换为 **this is string**。

  ```python
  >>> "this " "is " "string"
  'this is string'
  ```

- 字符串可以用 + 运算符连接在一起，用 * 运算符重复。

  ```python
  >>> s = 'Dad'
  >>> s * 3
  'DadDadDad'
  >>> s1 = 'Mom'
  >>> s + s1
  'DadMom'
  ```

- Python 中的字符串有两种索引方式，从左往右以 0 开始，从右往左以 -1 开始。

  ```python
  >>> S = 'The quick brown fox jumps over a lazy dog'
  >>> S[-1]
  'g'
  >>> S[0:-1] # 输出第一个到倒数第二个的所有字符
  'The quick brown fox jumps over a lazy do'
  >>> S[0:] # 输出从第一个开始后的所有字符
  'The quick brown fox jumps over a lazy dog'
  >>> S[2:5]
  'e q' # 输出从第三个开始到第五个的字符
  ```

- Python 中的字符串不能改变。

  ```python
  >>> '2312' = 123
  SyntaxError: cannot assign to literal
  ```

- Python 没有单独的字符类型，一个字符就是长度为 1 的字符串。

  ```python
  <class 'str'>
  >>> len('w')
  1
  ```

- 字符串的截取的语法格式如下：变量[头下标:尾下标:步长]

  ```python
  >>> S[1:-1:3]
  'hqcbwf m eaa ' # 输出从第二个开始到倒数第二个且每隔两个的字符（步长为3）
  ```

- **note**

  - 当字符串内容为浮点型要转换为整型时，无法直接用 int() 转换：

    ```python
    >>> a = '2.1'
    >>> print(int(a))
    ValueError: invalid literal for int() with base 10: '2.1'
    ```

    需要把字符串先转化成 float 型再转换成 int 型：

    ```python
    >>> print(int(float(a)))
    2
    ```



## 空行

函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。

空行与代码缩进不同，空行并不是 Python 语法的一部分。书写时不插入空行，Python 解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。

**记住：**空行也是程序代码的一部分。

## 同一行显示多条语句

Python 可以在同一行中使用多条语句，语句之间使用分号 ; 分割

```python
# sys.stdout.write 输出字符数 : x有3个，\n算一个，总共4个
>>> import sys; x = '111'; sys.stdout.write(x + '\n')
111
4
```

## 多个语句构成代码组

缩进相同的一组语句构成一个代码块，我们称之代码组。

像if、while、def和class这样的复合语句，首行以关键字开始，以冒号( : )结束，该行之后的一行或多行代码构成代码组。

我们将首行及后面的代码组称为一个子句(clause)。

如下实例：

```python
if expression :
   suite
elif expression :
   suite
else :
   suite
```

## print 输出

- **print** 默认输出是换行的，如果要实现不换行需要在变量末尾加上 end=""：

  > 在 Python3 中， print 函数的参数 **`end`** 默认值为 "\n"，即end="\n"，表示换行，给 **`end`** 赋值为空, 即end=""，就不会换行了

  ```python
  >>> print("s",end="");print("b")
  sb
  ```

- **note**

  - 在 print 打印的时候双引号与单引号都可以当做定界符使用，且可以嵌套。

    被嵌套的会被解释成为标点符号，反之一样。

    代码实例：

    - ```python
      print("Hello'World!")
      ```

      这句代码执行时，外侧的双引号为定界符，里面的那个单引号为标点符号。

      输出：

      ```
      Hello'World!
      ```

    - ```python
      print('Hello"World!')
      ```

      这句代码执行时，外侧的单引号为定界符，里面的那个双引号为标点符号。

      输出：

      ```
      Hello"World!
      ```

  - 要善用 help() 方法

    通过命令 **help("print")** 我们知道这个方法里第三个为缺省参数 **sep=' '**。

    ```python
    >>> help(print)
    Help on built-in function print in module builtins:

    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)

        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    ```

    所以在打印 dict 类的使用, 可以这样写:

    ```python
    >>> def getPairs(dict):
            for k,v in dict.items() :
                    print(k,v,sep=':')

    >>> getPairs({ x : x ** 3 for x in (1,2,3,4)})
    1:1
    2:8
    3:27
    4:64
    >>>
    ```

  - 类似于 C/C++ 的 **printf**，Python 的 **print** 也能实现格式化输出，方法是使用 % 操作符，它会将左边的字符串当做格式字符串，将右边的参数代入格式字符串：

    ```python
    >>> print("100 + 200 = %d" % 300) #左边的%d被替换成右边的300
    100 + 200 = 300
    >>> print("A的小写是%s" % "a") #左边的%s被替换成右边的a
    A的小写是a
    ```

    如果要带入多个参数，则需要用 () 包裹代入的多个参数，参数与参数之间用逗号隔开，参数的顺序应该对应格式字符串中的顺序：

    ```python
    >>> print("我是%s,你是%s" % ("nb","sb"))
    我是nb,你是sb
    ```

    **格式字符串**中，不同占位符的含义：

    - **%s**： 作为字符串
    - **%d**： 作为有符号十进制整数
    - **%u**： 作为无符号十进制整数
    - **%o**： 作为无符号八进制整数
    - **%x**： 作为无符号十六进制整数，a～f采用小写形式
    - **%X**： 作为无符号十六进制整数，A～F采用大写形式
    - **%f**： 作为浮点数
    - **%e，%E**： 作为浮点数，使用科学计数法
    - **%g，%G**： 作为浮点数，使用最低有效数位

## import 与 from...import

在 python 用 `import` 或者 `from...import` 来导入相应的模块。

将整个模块(somemodule)导入，格式为： `import somemodule`

从某个模块中导入某个函数,格式为： `from somemodule import somefunction`

从某个模块中导入多个函数,格式为： `from somemodule import firstfunc, secondfunc, thirdfunc`

将某个模块中的全部函数导入，格式为： `from somemodule import *`

- **note**

  - 关于 import 的小结，以 time 模块为例：

    1、将整个模块导入，例如：**`import time`**，在引用时格式为：time.sleep(1)。

    2、将整个模块中全部函数导入，例如：**`from time import *`**，在引用时格式为：sleep(1)。

    3、将模块中特定函数导入，例如：**`from time import sleep`**，在引用时格式为：sleep(1)。

    4、将模块换个别名，例如：**`import time as abc`**，在引用时格式为：abc.sleep(1)。

## 命令行参数

很多程序可以执行一些操作来查看一些基本信息，Python可以使用-h参数查看各参数帮助信息

```
$ python -h
usage: D:\Code\Anaconda3\python.exe [option] ... [-c cmd | -m mod | file | -] [arg] ...
Options and arguments (and corresponding environment variables):
-b     : issue warnings about str(bytes_instance), str(bytearray_instance)
         and comparing bytes/bytearray with str. (-bb: issue errors)
-B     : don't write .pyc files on import; also PYTHONDONTWRITEBYTECODE=x
-c cmd : program passed in as string (terminates option list)
-d     : turn on parser debugging output (for experts only, only works on
         debug builds); also PYTHONDEBUG=x
-E     : ignore PYTHON* environment variables (such as PYTHONPATH)
-h     : print this help message and exit (also --help)
-i     : inspect interactively after running script; forces a prompt even
         if stdin does not appear to be a terminal; also PYTHONINSPECT=x
-I     : isolate Python from the user's environment (implies -E and -s)
-m mod : run library module as a script (terminates option list)
-O     : remove assert and __debug__-dependent statements; add .opt-1 before
         .pyc extension; also PYTHONOPTIMIZE=x
-OO    : do -O changes and also discard docstrings; add .opt-2 before
         .pyc extension
-q     : don't print version and copyright messages on interactive startup
-s     : don't add user site directory to sys.path; also PYTHONNOUSERSITE
-S     : don't imply 'import site' on initialization
-u     : force the stdout and stderr streams to be unbuffered;
         this option has no effect on stdin; also PYTHONUNBUFFERED=x
-v     : verbose (trace import statements); also PYTHONVERBOSE=x
         can be supplied multiple times to increase verbosity
-V     : print the Python version number and exit (also --version)
         when given twice, print more information about the build
-W arg : warning control; arg is action:message:category:module:lineno
         also PYTHONWARNINGS=arg
-x     : skip first line of source, allowing use of non-Unix forms of #!cmd
-X opt : set implementation-specific option. The following options are available:

         -X faulthandler: enable faulthandler
         -X oldparser: enable the traditional LL(1) parser; also PYTHONOLDPARSER
         -X showrefcount: output the total reference count and number of used
             memory blocks when the program finishes or after each statement in the
             interactive interpreter. This only works on debug builds
         -X tracemalloc: start tracing Python memory allocations using the
             tracemalloc module. By default, only the most recent frame is stored in a
             traceback of a trace. Use -X tracemalloc=NFRAME to start tracing with a
             traceback limit of NFRAME frames
         -X importtime: show how long each import takes. It shows module name,
             cumulative time (including nested imports) and self time (excluding
             nested imports). Note that its output may be broken in multi-threaded
             application. Typical usage is python3 -X importtime -c 'import asyncio'
         -X dev: enable CPython's "development mode", introducing additional runtime
             checks which are too expensive to be enabled by default. Effect of the
             developer mode:
                * Add default warning filter, as -W default
                * Install debug hooks on memory allocators: see the PyMem_SetupDebugHooks() C function
                * Enable the faulthandler module to dump the Python traceback on a crash
                * Enable asyncio debug mode
                * Set the dev_mode attribute of sys.flags to True
                * io.IOBase destructor logs close() exceptions
         -X utf8: enable UTF-8 mode for operating system interfaces, overriding the default
             locale-aware mode. -X utf8=0 explicitly disables UTF-8 mode (even when it would
             otherwise activate automatically)
         -X pycache_prefix=PATH: enable writing .pyc files to a parallel tree rooted at the
             given directory instead of to the code tree

--check-hash-based-pycs always|default|never:
    control how Python invalidates hash-based .pyc files
file   : program read from script file
-      : program read from stdin (default; interactive mode if a tty)
arg ...: arguments passed to program in sys.argv[1:]

Other environment variables:
PYTHONSTARTUP: file executed on interactive startup (no default)
PYTHONPATH   : ';'-separated list of directories prefixed to the
               default module search path.  The result is sys.path.
PYTHONHOME   : alternate <prefix> directory (or <prefix>;<exec_prefix>).
               The default module search path uses <prefix>\python{major}{minor}.
PYTHONPLATLIBDIR : override sys.platlibdir.
PYTHONCASEOK : ignore case in 'import' statements (Windows).
PYTHONUTF8: if set to 1, enable the UTF-8 mode.
PYTHONIOENCODING: Encoding[:errors] used for stdin/stdout/stderr.
PYTHONFAULTHANDLER: dump the Python traceback on fatal errors.
PYTHONHASHSEED: if this variable is set to 'random', a random value is used
   to seed the hashes of str and bytes objects.  It can also be set to an
   integer in the range [0,4294967295] to get hash values with a
   predictable seed.
PYTHONMALLOC: set the Python memory allocators and/or install debug hooks
   on Python memory allocators. Use PYTHONMALLOC=debug to install debug
   hooks.
PYTHONCOERCECLOCALE: if this variable is set to 0, it disables the locale
   coercion behavior. Use PYTHONCOERCECLOCALE=warn to request display of
   locale coercion and locale compatibility warnings on stderr.
PYTHONBREAKPOINT: if this variable is set to 0, it disables the default
   debugger. It can be set to the callable of your debugger of choice.
PYTHONDEVMODE: enable the development mode.
PYTHONPYCACHEPREFIX: root directory for bytecode cache (pyc) files.
```

## note

- 调用 python 的 help() 函数可以打印输出一个函数的文档字符串

# 基本数据结构

## 变量

Python 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。

在 Python 中，变量就是变量，它没有类型，我们所说的"类型"是变量所指的内存中对象的类型。

等号（=）用来给变量赋值。

等号（=）运算符左边是一个变量名,等号（=）运算符右边是存储在变量中的值。例如：

```python
counter = 100          # 整型变量
miles   = 1000.0       # 浮点型变量
name    = "妇炎洁"     # 字符串
>>> type(counter)
<class 'int'>
>>> type(miles)
<class 'float'>
>>> type(name)
<class 'str'>
```

### 多个变量赋值

Python允许你同时为多个变量赋值。例如：

```python
a = b = c = 1
```

以上实例，创建一个整型对象，值为 1，从后向前赋值，三个变量被赋予相同的数值。

您也可以为多个对象指定多个变量。例如：

```python
a, b, c = 1, 2, "fuc"
>>> print(str(a) + str(b) + c)
12fuc
```

以上实例，两个整型对象 1 和 2 的分配给变量 a 和 b，字符串对象 "runoob" 分配给变量 c。

## 标准数据类型

Python3 中有六个标准的数据类型：

- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

Python3 的六个标准数据类型中：

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

## Number（数字）

Python3 支持 **int、float、bool、complex（复数）**。

在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。

像大多数语言一样，数值类型的赋值和计算都是很直观的。

- 内置的 type() 函数可以用来查询变量所指的对象类型。

  ```python
  >>> a, b, c, d = 20, 5.5, True, 4+3j
  >>> print(type(a), type(b), type(c), type(d))
  <class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
  ```

- 此外还可以用 isinstance 来判断：

  ```python
  >>> a = 111
  >>> isinstance(a, int)
  True
  ```

- isinstance 和 type 的区别在于：

  - type()不会认为子类是一种父类类型。
  - isinstance()会认为子类是一种父类类型。

  ```python
  >>> class A:
  ...     pass
  ...
  >>> class B(A):
  ...     pass
  ...
  >>> isinstance(A(),A)
  True
  >>> type(A()) == A
  True
  >>> isinstance(B(),A)
  True
  >>> type(B) == B
  False
  ```

  > A=ClassA()是把类ClassA的实例赋值给变量A
  >
  > ClassB(A)意思是类ClassB继承类ClassA的方法和属性。就是类的继承。实例A是类ClassA的实例。而类ClassB继承了类ClassA的属性和方法。

- > **注意：**Python3 中，bool 是 int 的子类，True 和 False 可以和数字相加， `True==1、False==0` 会返回 **True**，但可以通过 `is` 来判断类型。
  >
  > ```
  > >>> issubclass(bool, int)
  > True
  > >>> True==1
  > True
  > >>> False==0
  > True
  > >>> True+1
  > 2
  > >>> False+1
  > 1
  > >>> 1 is True
  > False
  > >>> 0 is False
  > False
  > ```
  >
  > 在 Python2 中是没有布尔型的，它用数字 0 表示 False，用 1 表示 True。

- 当你指定一个值时，Number 对象就会被创建：

  ```
  >>> var1 = 1
  >>> var2 = 10
  ```

- 您也可以使用del语句删除一些对象引用。

  del语句的语法是：

  ```python
  # []表示里面的内容可以省略
  del var1[,var2[,var3[....,varN]]]
  ```

  您可以通过使用del语句删除单个或多个对象。例如：

  ```python
  >>> del var1, var2
  >>> print(var1, var2)
  NameError: name 'var1' is not defined
  ```

### 数值运算

```python
>>> 5 + 4  # 加法
9
>>> 4.3 - 2 # 减法
2.3
>>> 3 * 7  # 乘法
21
>>> 2 / 8  # 除法，得到一个浮点数
0.25
>>> 2 // 8 # 取整数 取整除 - 向下取接近商的整数
0
>>> 18 % 7 # 取余（官方叫做”模运算“）
4
>>> 2 ** 10 # 乘方 返回x的y次幂
1024
```

**注意：**

- 1、Python可以同时为多个变量赋值，如a, b = 1, 2。
- 2、一个变量可以通过赋值指向不同类型的对象。
- 3、数值的除法包含两个运算符：/ 返回一个浮点数，// 返回一个整数。
- 4、在混合计算时，Python会把整型转换成为浮点数。

### 数值类型实例

| int    | float      | complex    |
| ------ | ---------- | ---------- |
| 10     | 0.0        | 3.14j      |
| 100    | 15.20      | 45.j       |
| -786   | -21.9      | 9.322e-36j |
| 080    | 32.3e+18   | .876j      |
| -0490  | -90.       | -.6545+0J  |
| -0x260 | -32.54e100 | 3e+26J     |
| 0x69   | 70.2E-12   | 4.53e-7j   |

Python 还支持复数，复数由实数部分和虚数部分构成，可以用 `a + bj`，或者 `complex(a,b)` 表示， 复数的实部 **a** 和虚部 **b** 都是浮点型。

## String（字符串）

Python中的字符串用单引号 ' 或双引号 " 括起来，同时使用反斜杠 \ 转义特殊字符。

- 字符串的截取的语法格式如下：

  ```
  变量[头下标:尾下标]
  ```

  索引值以 0 为开始值，-1 为从末尾的开始位置。

- 加号  `+`  是字符串的连接符， 星号  `*`  表示复制当前字符串，与之结合的数字为复制的次数。实例如下：

  ```python
  >>> s
  'The quick brown fox jumps over a lazy dog'
  >>> s[0:]
  'The quick brown fox jumps over a lazy dog'
  >>> s[0:-1]
  'The quick brown fox jumps over a lazy do'
  >>> s[2:6]
  'e qu'
  >>> s[-6:-1]
  'zy do'
  >>> s[-6:]
  'zy dog'
  >>> s[-1]
  'g'
  >>> s[:]
  'The quick brown fox jumps over a lazy dog'
  >>> s[:6]
  'The qu'
  >>> s[:-6]
  'The quick brown fox jumps over a la'

  >>> 'wolf' + s
  'wolfThe quick brown fox jumps over a lazy dog'
  >>> s*4
  'The quick brown fox jumps over a lazy dogThe quick brown fox jumps over a lazy dogThe quick brown fox jumps over a lazy dogThe quick brown fox jumps over a lazy dog'
  ```

+ Python 使用反斜杠 \ 转义特殊字符，如果你不想让反斜杠发生转义，可以在字符串前面添加一个 r，表示原始字符串

  另外，反斜杠(\)可以作为续行符，表示下一行是上一行的延续。也可以使用 **"""..."""** 或者 **'''...'''** 跨越多行。

  注意，Python 没有单独的字符类型，一个字符就是长度为1的字符串。

+ 与 C 字符串不同的是，Python 字符串不能被改变。向一个索引位置赋值，比如 word[0] = 'm' 会导致错误。

  ```python
  >>> s[0] = 'm'
  TypeError: 'str' object does not support item assignment
  # TypeError：“str”对象不支持项赋值
  # s[1] = 'm'也会出错
  ```

  **注意：**

  - 1、反斜杠可以用来转义，使用r可以让反斜杠不发生转义。
  - 2、字符串可以用+运算符连接在一起，用*运算符重复。
  - 3、Python中的字符串有两种索引方式，从左往右以0开始，从右往左以-1开始。
  - 4、Python中的字符串不能改变。

## List（列表）

List（列表） 是 Python 中使用最频繁的数据类型。

列表可以完成大多数集合类的数据结构实现。列表中元素的类型可以不相同，它支持数字，字符串甚至可以包含列表（所谓嵌套）。

列表是写在方括号 [] 之间、用逗号分隔开的元素列表。

和字符串一样，列表同样可以被索引和截取，列表被截取后返回一个包含所需元素的新列表。

- 列表截取的语法格式如下：

  ```
  变量[头下标:尾下标]
  ```

  索引值以 0 为开始值，-1 为从末尾的开始位置。

  加号 + 是列表连接运算符，星号 * 是重复操作。如下实例：

  ```python
  >>>  list = ['fyj', 24, 3.14]
  IndentationError: unexpected indent
  >>> list = ['fyj', 24, 3.14 ]
  >>> tinylist = ['cmd', 'ipconfig' ]
  >>> list[:]
  ['fyj', 24, 3.14]
  >>> tinylist*2
  ['cmd', 'ipconfig', 'cmd', 'ipconfig']
  >>> list + tinylist
  ['fyj', 24, 3.14, 'cmd', 'ipconfig']
  ```

- 与Python字符串不一样的是，列表中的元素是可以改变的：

  ```python
  >>> l = [1,2,3,4,5,6]
  >>> l[0] = 9
  >>> l
  [9, 2, 3, 4, 5, 6]
  >>> l[2:5] = [12,32,45,66]
  >>> l
  [9, 2, 12, 32, 45, 66, 6]
  >>> l[3:6] = []
  >>> l
  [9, 2, 12, 6]
  >>> l[2:] = [1,2,3,4,5,6,7]
  >>> l
  [9, 2, 1, 2, 3, 4, 5, 6, 7]
  ```

- List 内置了有很多方法，例如 append()、pop() 等等，这在后面会讲到。

- **注意：**

  - 1、List写在方括号之间，元素用逗号隔开。
  - 2、和字符串一样，list可以被索引和切片。
  - 3、List可以使用+操作符进行拼接。
  - 4、List中的元素是可以改变的。

- Python 列表截取可以接收第三个参数，参数作用是截取的步长，以下实例在索引 1 到索引 4 的位置并设置为步长为 2（间隔一个位置）来截取字符串：

  如果第三个参数为负数表示逆向读取，以下实例用于翻转字符串：

  ```python
  def reverseWords(input):
      inputWords = input.split(" ")
      inputWords = inputWords[-1::-1]
      output = ' '.join(inputWords)
      return output

  if __name__ == "__main__":
      input = input("请输入您要反转的句子：\n")
      rw = reverseWords(input)
      print(rw)
  ```


## Tuple（元组）

元组（tuple）与列表类似，不同之处在于元组的**元素不能修改**。元组写在小括号 () 里，元素之间用逗号隔开。

- 元组中的元素类型也可以不相同：

  ```python
  >>> tuple = ('abcd', 786, 2.23, 'filter', 70.2)
  >>> tinytuple = (123, 'filter')
  >>> tuple
  ('abcd', 786, 2.23, 'filter', 70.2)
  >>> tuple[0]
  'abcd'
  >>> tuple[1:3]
  (786, 2.23)
  >>> tuple[2:]
  (2.23, 'filter', 70.2)
  >>> tuple*3
  ('abcd', 786, 2.23, 'filter', 70.2, 'abcd', 786, 2.23, 'filter', 70.2, 'abcd', 786, 2.23, 'filter', 70.2)
  >>> tuple + tinytuple
  ('abcd', 786, 2.23, 'filter', 70.2, 123, 'filter')
  ```

- 元组与字符串类似，可以被索引且下标索引从0开始，-1 为从末尾开始的位置。也可以进行截取（看上面，这里不再赘述）。

  其实，可以把字符串看作一种特殊的元组。

  ```python
  >>> tup = (1,2,3,4,5,6)
  >>> tup
  (1, 2, 3, 4, 5, 6)
  >>> tup[1:6]
  (2, 3, 4, 5, 6)
  >>> tup[2] = 0
  TypeError: 'tuple' object does not support item assignment
  >>>
  ```

- 虽然tuple的元素不可改变，但它可以包含可变的对象，比如list列表。

  构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

  ```python
  tup1 = ()    # 空元组
  tup2 = (20,) # 一个元素，需要在元素后添加逗号

  >>> tup1 = ()
  >>> type(tup1)
  <class 'tuple'>
  >>> tup2 = (2)
  >>> type(tup2)
  <class 'int'>
  >>> tup3 = (2,)
  >>> type(tup3)
  <class 'tuple'>
  ```

  string、list 和 tuple 都属于 sequence（序列）。

- **注意：**

  - 1、与字符串一样，元组的元素不能修改。
  - 2、元组也可以被索引和切片，方法一样。
  - 3、注意构造包含 0 或 1 个元素的元组的特殊语法规则。
  - 4、元组也可以使用+操作符进行拼接。

## Set（集合）

集合（set）是由一个或数个形态各异的大小整体组成的，构成集合的事物或对象称作元素或是成员。

基本功能是进行成员关系测试和删除重复元素。

- 可以使用大括号 { } 或者 set() 函数创建集合，

  注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。

  ```python
  >>> type({})
  <class 'dict'>
  >>> type(set())
  <class 'set'>
  ```

- 创建格式：

  ```python
  parame = {value01,value02,...}
  或者
  set(value)
  ```

  ```python
  sites = {'Google', 'Taobao', 'Taobao', 'Facebook', 'Zhihu', 'Baidu'}

  print(sites)   # 输出集合，重复的元素被自动去掉

  # 成员测试
  if 'Baidu' in sites :
      print('Baidu 在集合中')
  else :
      print('Baidu 不在集合中')

  # set可以进行集合运算
  a = set('abracadabra')
  b = set('alacazam')

  print(a)
  print(a - b)     # a 和 b 的差集
  print(a | b)     # a 和 b 的并集
  print(a & b)     # a 和 b 的交集
  print(a ^ b)     # a 和 b 中不同时存在的元素

  ###### 结果
  {'Baidu', 'Zhihu', 'Google', 'Taobao', 'Facebook'}
  Baidu 在集合中
  {'r', 'b', 'd', 'c', 'a'}
  {'b', 'd', 'r'}
  {'r', 'd', 'b', 'c', 'z', 'l', 'm', 'a'}
  {'a', 'c'}
  {'r', 'z', 'l', 'd', 'm', 'b'}
  ```

### 集合的基本操作

#### 1、添加元素

**语法格式如下：**

```python
s.add( x )
```



## Dictionary（字典）

字典（dictionary）是Python中另一个非常有用的内置数据类型。

列表是有序的对象集合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。

字典是一种映射类型，字典用 { } 标识，它是一个无序的 **键(key) : 值(value)** 的集合。

键(key)必须使用不可变类型。

在同一个字典中，键(key)必须是唯一的。

- ```python
  >>> dict = {}
  >>> dict['one'] = "1 - 菜鸟教程"
  >>> dict['one']
  '1 - 菜鸟教程'
  >>> dict[2] = "2 - 菜鸟工具"
  >>> dict[2]
  '2 - 菜鸟工具'
  >>> tinydict = {'name': 'runoob', 'code': 1, 'site': 'www.runoob.com'}
  >>> tinydict
  {'name': 'runoob', 'code': 1, 'site': 'www.runoob.com'}
  >>> tinydict.keys()
  dict_keys(['name', 'code', 'site'])
  >>> tinydict.values()
  dict_values(['runoob', 1, 'www.runoob.com'])
  >>>
  ```

- 构造函数 dict() 可以直接从键值对序列中构建字典如下：

  ```python
  >>> dict([('Baidu', 1), ('Google', 2), ('Taobao', 3)])
  {'Baidu': 1, 'Google': 2, 'Taobao': 3}
  >>> {x: x**2 for x in (2,4,6)}
  {2: 4, 4: 16, 6: 36}
  >>> dict(Baidu = 1, Taobao = 2, Tencent = 3)
  {'Baidu': 1, 'Taobao': 2, 'Tencent': 3}
  ```

  {x: x**2 for x in (2, 4, 6)} 该代码使用的是字典推导式，更多推导式内容可以参考：[Python 推导式](#Py1)。

  另外，字典类型也有一些内置的函数，例如 clear()、keys()、values() 等。

  > - clear()
  >
  >   - 字典(Dictionary) clear() 函数用于删除字典内所有元素。
  >   - List clear() 函数用于清空列表，类似于 **del a[:]**。
  >   - Set clear() 方法用于移除集合中的所有元素。
  >
  > - keys()
  >
  >   字典 keys() 方法返回一个视图对象。
  >
  >   dict.keys()、dict.values() 和 dict.items() 返回的都是视图对象（ view objects），提供了字典实体的动态视图，这就意味着字典改变，视图也会跟着变化。
  >
  >   视图对象不是列表，不支持索引，可以使用 list() 来转换为列表。
  >
  >   我们不能对视图对象进行任何的修改，因为字典的视图对象都是只读的。
  >
  >   **注意：**Python2.x 是直接返回列表
  >
  > - values()
  >
  >   字典 values() 方法返回一个视图对象。
  >
  >

  **注意：**

  - 1、字典是一种映射类型，它的元素是键值对。
  - 2、字典的关键字必须为不可变类型，且不能重复。
  - 3、创建空字典使用 **{ }**。

## Python数据类型转换

有时候，我们需要对数据内置的类型进行转换，数据类型的转换，你只需要将数据类型作为函数名即可，在下一章节 Python3 数据类型转换 会具体介绍。

# 数据类型转换

有时候，我们需要对数据内置的类型进行转换，数据类型的转换，一般情况下你只需要将数据类型作为函数名即可。

Python 数据类型转换可以分为两种：

- 隐式类型转换 - 自动完成
- 显式类型转换 - 需要使用类型函数来转换

## 隐式类型转换

在隐式类型转换中，Python 会自动将一种数据类型转换为另一种数据类型，不需要我们去干预。

以下实例中，我们对两种不同类型的数据进行运算，较低数据类型（整数）就会转换为较高数据类型（浮点数）以避免数据丢失。

```python
>>> n_int = 123
>>> n_flo = 1.23
>>> n_new = n_int + n_flo

>>> type(n_int)
<class 'int'>
>>> type(n_flo)
<class 'float'>

>>> n_new
124.23
>>> type(n_new)
<class 'float'>
```

代码解析：

- 实例中我们对两个不同数据类型的变量 `num_int` 和 `num_flo` 进行相加运算，并存储在变量 `num_new` 中。
- 然后查看三个变量的数据类型。
- 在输出结果中，我们看到 `num_int` 是 `整型（integer）` ， `num_flo` 是 ` 浮点型（float）`。
- 同样，新的变量 `num_new` 是 ` 浮点型（float）`，这是因为 Python 会将较小的数据类型转换为较大的数据类型，以避免数据丢失。

我们再看一个实例，整型数据与字符串类型的数据进行相加：

```python
>>> n_int = 123
>>> n_str = '123'
>>> n_new = n_int + n_str
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

从输出中可以看出，整型和字符串类型运算结果会报错，输出 TypeError。 Python 在这种情况下无法使用隐式转换。

但是，Python 为这些类型的情况提供了一种解决方案，称为显式转换。

## 显式类型转换

在显式类型转换中，用户将对象的数据类型转换为所需的数据类型。 我们使用 int()、float()、str() 等预定义函数来执行显式类型转换。

int() 强制转换为整型：

```python
x = int(1)   # x 输出结果为 1
y = int(2.8) # y 输出结果为 2
z = int("3") # z 输出结果为 3
```

float() 强制转换为浮点型：

```python
x = float(1)     # x 输出结果为 1.0
y = float(2.8)   # y 输出结果为 2.8
z = float("3")   # z 输出结果为 3.0
w = float("4.2") # w 输出结果为 4.2
```

str() 强制转换为字符串类型：

```python
x = str("s1") # x 输出结果为 's1'
y = str(2)    # y 输出结果为 '2'
z = str(3.0)  # z 输出结果为 '3.0'
```

整型和字符串类型进行运算，就可以用强制类型转换来完成：

```python
>>> n_int = 123
>>> n_str = '123'
>>> n_new = n_int + int(n_str)
>>> n_new
246
```



# <a id = "Py1">Python 推导式</a>

Python 推导式是一种独特的数据处理方式，可以从一个数据序列构建另一个新的数据序列的结构体。

Python 支持各种数据结构的推导式：

- 列表(list)推导式
- 字典(dict)推导式
- 集合(set)推导式
- 元组(tuple)推导式

## 列表推导式

列表推导式格式为：

```python
[表达式 for 变量 in 列表]
[out_exp_res for out_exp in input_list]

或者

[表达式 for 变量 in 列表 if 条件]
[out_exp_res for out_exp in input_list if condition]
```

- out_exp_res：列表生成元素表达式，可以是有返回值的函数。
- for out_exp in input_list：迭代 input_list 将 out_exp 传入到 out_exp_res 表达式中。
- if condition：条件语句，可以过滤列表中不符合条件的值。

过滤掉长度小于或等于3的字符串列表，并将剩下的转换成大写字母：

```python
>>> names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
>>> new_names = [name.upper() for name in names if len(name)>3]
>>> new_names
['ALICE', 'JERRY', 'WENDY', 'SMITH']
```

计算 30 以内可以被 3 整除的整数：

```python
>>> multiples = [i for i in range(31) if i % 3 == 0]
>>> multiples
[0, 3, 6, 9, 12, 15, 18, 21, 24, 27, 30]
```

## 字典推导式

字典推导基本格式：

```
{ key_expr: value_expr for value in collection }
或
{ key_expr: value_expr for value in collection if condition }
```

使用字符串及其长度创建字典：

```python
>>> listdemo = ['Google','Baidu', 'Taobao']
>>> newdict = {key:len(key) for key in listdemo}
>>> newdict
{'Google': 6, 'Baidu': 5, 'Taobao': 6}
```

提供三个数字，以三个数字为键，三个数字的平方为值来创建字典：

```python
>>> dic = {x: x**2 for x in (2,4,6)}
>>> dic
{2: 4, 4: 16, 6: 36}
```

## 集合推导式

集合推导式基本格式：

```
{ expression for item in Sequence }
或
{ expression for item in Sequence if conditional }
```

计算数字 1,2,3 的平方数：

```python
>>> setnew = {x**2 for x in (1,2,3)}
>>> setnew
{1, 4, 9}
```

判断不是 abc 的字母并输出：

```python
setn = {inp for inp in 'abvcsbdvsg' if inp not in 'abc'}
setn
```

## 元组推导式（生成器表达式）

元组推导式可以利用 range 区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的元组。

元组推导式基本格式：

```
(expression for item in Sequence )
或
(expression for item in Sequence if conditional )
```

元组推导式和列表推导式的用法也完全相同，只是元组推导式是用 () 圆括号将各部分括起来，而列表推导式用的是中括号 []，另外元组推导式返回的结果是一个生成器对象。

例如，我们可以使用下面的代码生成一个包含数字 1~9 的元组：

```python
>>> tup = (x for x in range(1,10))
>>> tup
<generator object <genexpr> at 0x0000022DFFFAF120>	# 返回的是生成器对象
>>> tuple(tup)	# 使用 tuple() 函数，可以直接将生成器对象转换成元组
(1, 2, 3, 4, 5, 6, 7, 8, 9)
```

## ps:

- 语法格式：

    ```python
    结果值1 if 判断条件 else 结果2  for 变量名 in 原列表
    ```


## if else 语法

语法格式：

```python
结果值1 if 判断条件 else 结果2  for 变量名 in 原列表
```

```python
list1 = ['python', 'test1', 'test2']
# title()：首字母大写
# upper()：改为大写
# startswith()：用于检索字符串是否以指定字符串开头，如果是返回 True；反之返回 False。
list2 = [word.title() if word.startswith('p') else word.upper() for word in list1]
print(list2)
# 结果
['Python', 'TEST1', 'TEST2']
```

# 编程第一步

在前面的教程中我们已经学习了一些 Python3 的基本语法知识，下面我们尝试来写一个斐波纳契数列。

```python
# Fibonacci series: 斐波纳契数列
# 两个元素的总和确定了下一个数
>>> a, b = 0, 1
>>> while b < 10:
...     print(b, end = ',')
...     a, b = b, a+b
...
1,1,2,3,5,8,
```

其中代码 a, b = b, a+b 的计算方式为先计算右边表达式，然后同时赋值给左边，等价于：

```python
n=b
m=a+b
a=n
b=m
```

这个例子介绍了几个新特征。

第一行包含了一个复合赋值：变量 a 和 b 同时得到新值 0 和 1。最后一行再次使用了同样的方法，可以看到，右边的表达式会在赋值变动之前执行。右边表达式的执行顺序是从左往右的。

**输出变量值:**

```python
>>> i = 256*256
>>> print('i 的值为：', i)
i 的值为： 65536

>>> i = 123123
>>> print('12312',i)
12312 123123
```

# 条件控制

Python 条件语句是通过一条或多条语句的执行结果（True 或者 False）来决定执行的代码块。

## if 语句

Python中if语句的一般形式如下所示：

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

Python 中用 **elif** 代替了 **else if**，所以if语句的关键字为：**if – elif – else**。

**注意：**

- 1、每个条件后面要使用冒号 :，表示接下来是满足条件后要执行的语句块。
- 2、使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。
- 3、在 Python 中没有 switch...case 语句，但在 Python3.10 版本添加了 match...case，功能也类似，详见下文。

+ 三目运算符又称条件运算符，可以将其视为if-else结构的精简表示，常用于变量赋值和函数返回值。
     在C语言中，三目运算符使用`x = condition ? a : b`，表示当condition成立时，x取a，否则在x取b。
     在python中，三目运算符使用`x = a if condition else b`进行表述，示例如下：

## if 嵌套

在嵌套 if 语句中，可以把 if...elif...else 结构放在另外一个 if...elif...else 结构中。

```python
if 表达式1:
    语句
    if 表达式2:
        语句
    elif 表达式3:
        语句
    else:
        语句
elif 表达式4:
    语句
else:
    语句
```

## match...case

> 我的是 3.9.13，就不搞了

Python 3.10 增加了 match...case 的条件判断，不需要再使用一连串的 if-else 来判断了。

match 后的对象会依次与 case 后的内容进行匹配，如果匹配成功，则执行匹配到的表达式，否则直接跳过，_ 可以匹配一切。

语法格式如下：

```python
match subject:
    case <pattern_1>:
        <action_1>
    case <pattern_2>:
        <action_2>
    case <pattern_3>:
        <action_3>
    case _:
        <action_wildcard>
```

case _: 类似于 C 和 Java 中的 default:，当其他 case 都无法匹配时，匹配这条，保证永远会匹配成功。

# 循环语句

本章节将为大家介绍 Python  循环语句的使用。

Python 中的循环语句有 for 和 while。

## while 循环

Python 中 while 语句的一般形式：

```python
while 判断条件(condition)：
    执行语句(statements)……
```

同样需要注意冒号和缩进。另外，在 Python 中没有 do..while 循环。

以下实例使用了 while 来计算 1 到 100 的总和：

```python
n = 100

sum = 0
counter = 1
while counter <= n:
    sum = sum + counter
    counter += 1

print("1 到 %d 之和为: %d" % (n,sum))
```

### 无限循环

我们可以通过设置条件表达式永远不为 false 来实现无限循环，实例如下：

```python
var = 1
while var == 1 :  # 表达式永远为 true
   num = int(input("输入一个数字  :"))
   print ("你输入的数字是: ", num)

print ("Good bye!")
```

你可以使用  **CTRL+C** 来退出当前的无限循环。

无限循环在服务器上客户端的实时请求非常有用。

### while 循环使用 else 语句

如果 while 后面的条件语句为 false 时，则执行 else 的语句块。

语法格式如下：

```python
while <expr>:
    <statement(s)>
else:
    <additional_statement(s)>
```

expr 条件语句为 true 则执行 statement(s) 语句块，如果为 false，则执行 additional_statement(s)。

循环输出数字，并判断大小：

```python
count = 0
while count < 5:
   print (count, " 小于 5")
   count = count + 1
else:
   print (count, " 大于或等于 5")
```

### 简单语句组

类似 if 语句的语法，如果你的 while 循环体中只有一条语句，你可以将该语句与 while 写在同一行中

## for 语句

Python for 循环可以遍历任何可迭代对象，如一个列表或者一个字符串。

for循环的一般格式如下：

```python
for <variable> in <sequence>:
    <statements>
else:
    <statements>
```

- 可以用来打印序列中的元素，也可用于打印字符串中的每个字符
- 整数范围值可以配合 range() 函数使用

## for...else

在 Python 中，for...else 语句用于在循环结束后执行一段代码。

语法格式如下：

```
for item in iterable:
    # 循环主体
else:
    # 循环结束后执行的代码
```

当循环执行完毕（即遍历完 iterable 中的所有元素）后，会执行 else 子句中的代码，如果在循环过程中遇到了 break 语句，则会中断循环，此时不会执行 else 子句。

以下 for 实例中使用了 break 语句，break 语句用于跳出当前循环体，不会执行 else 子句：

```python
s = 'The quick brown fox jumps over a lazy dog'
for letter in s:
    if letter in 'abc':
        break
    print(letter,end='')

else:
    print('\nFinished\n')
# 结果
The qui
```

## range() 函数

如果你需要遍历数字序列，可以使用内置 range() 函数。它会生成数列，你也可以使用 range() 指定区间的值，也可以使 range() 以指定数字开始并指定不同的增量(甚至可以是负数，有时这也叫做'步长')

您可以结合 range() 和 len() 函数以遍历一个序列的索引:

```python
>>>a = ['Google', 'Baidu', 'Runoob', 'Taobao', 'QQ']
>>> for i in range(len(a)):
...     print(i, a[i])
...
0 Google
1 Baidu
2 Runoob
3 Taobao
4 QQ
>>>
```

还可以使用 range() 函数来创建一个列表：

```python
>>>list(range(5))
[0, 1, 2, 3, 4]
```

更多关于 range() 函数用法参考：https://www.runoob.com/python3/python3-func-range.html

## break 和 continue 语句及循环中的 else 子句

**break** 语句可以跳出 for 和 while 的循环体。如果你从 for 或 while 循环中终止，任何对应的循环 else 块将不执行。

**continue** 语句被用来告诉 Python 跳过当前循环块中的剩余语句，然后继续进行下一轮循环。

## pass 语句

Python pass是空语句，是为了保持程序结构的完整性。

pass 不做任何事情，一般用做占位语句

```python
if __name__ == "__main__":
    pass
```

## note

- 使用内置 enumerate 函数进行遍历:

  ```
  for index, item in enumerate(sequence):
      process(index, item)
  ```

  实例

  ```
  >>> sequence = [12, 34, 34, 23, 45, 76, 89]
  >>> for i, j in enumerate(sequence):
  ...     print(i, j)
  ...
  0 12
  1 34
  2 34
  3 23
  4 45
  5 76
  6 89
  ```

# 迭代器与生成器

## 迭代器

迭代是Python最强大的功能之一，是访问集合元素的一种方式。

迭代器是一个可以记住遍历的位置的对象。

迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。

迭代器有两个基本的方法：**iter()** 和 **next()**。

字符串，列表或元组对象都可用于创建迭代器：

```python
>>> list=[1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> print (next(it))   # 输出迭代器的下一个元素
1
>>> print (next(it))
2
```

迭代器对象可以使用常规for语句进行遍历：

```python
>>> list=[1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> for x in it:
...     print (x, end=" ")
...
1 2 3 4
```

也可以使用 next() 函数：

```python
import sys  # 引入 sys 模块

list = [1, 2, 3, 4]
it = iter(list)    # 创建迭代器对象

while True:
    try:
        print(next(it))
    except StopIteration:
        sys.exit()
```

### 创建一个迭代器

把一个类作为一个迭代器使用需要在类中实现两个方法 __iter__() 与 __next__() 。

如果你已经了解的面向对象编程，就知道类都有一个构造函数，Python 的构造函数为 __init__(), 它会在对象初始化的时候执行。

__iter__() 方法返回一个特殊的迭代器对象， 这个迭代器对象实现了 __next__() 方法并通过 StopIteration 异常标识迭代的完成。

__next__() 方法（Python 2 里是 next()）会返回下一个迭代器对象。

创建一个返回数字的迭代器，初始值为 1，逐步递增 1：

# 函数

## 匿名函数

Python 使用 lambda 来创建匿名函数。

所谓匿名，意即不再使用 **def** 语句这样标准的形式定义一个函数。

- lambda 只是一个表达式，函数体比 **def** 简单很多。
- lambda 的主体是一个表达式，而不是一个代码块。仅仅能在 lambda 表达式中封装有限的逻辑进去。
- lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
- 虽然 lambda 函数看起来只能写一行，却不等同于 C 或 C++ 的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

### 语法

lambda 函数的语法只包含一个语句，如下：

```python
lambda [arg1 [,arg2,.....argn]]:expression
```



# 输入和输出

1. print



2. input

   input语法

   > input([prompt])

   参数说明

   - prompt: 提示信息

   ```python
   str = input("请输入：");
   print ("你输入的内容是: ", str)
   # 输出
   '''
   请输入：内容
   '内容'
   '''
   ```

# 附件

## open函数

| 模式 | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| t    | 文本模式 (默认)。                                            |
| x    | 写模式，新建一个文件，如果该文件已存在则会报错。             |
| b    | 二进制模式。                                                 |
| +    | 打开一个文件进行更新(可读可写)。                             |
| U    | 通用换行模式（不推荐）。                                     |
| r    | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。 |
| rb   | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。 |
| r+   | 打开一个文件用于读写。文件指针将会放在文件的开头。           |
| rb+  | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。 |
| w    | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| wb   | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
| w+   | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| wb+  | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
| a    | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| ab   | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| a+   | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。 |
| ab+  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。 |

## with 关键字

Python 中的 with 语句用于异常处理，封装了 try…except…finally 编码范式，提高了易用性。

**with** 语句使代码更清晰、更具可读性， 它简化了文件流等公共资源的管理。

在处理文件对象时使用 with 关键字是一种很好的做法。

with的语法

```python
with EXPR as Variable:
    BLOCK
```

我们可以看下以下几种代码实例：

不使用 **with**，也不使用 **try…except…finally**

```python
# 不使用 with，也不使用 try…except…finally:

fp = open('./temp1.txt', 'w')
fp.write('Now the file has one more line!\n')
fp.close()
```
以上代码如果在调用 write 的过程中，出现了异常，则 close 方法将无法被执行，因此资源就会一直被该程序占用而无法被释放。 接下来我们呢可以使用 **try…except…finally** 来改进代码：

```python
# 使用 try…except…finally 来改进代码：

fp = open('./temp2.txt', 'w')
try:
    fp.write('Now the file has one more line!\n')
except:
    print('Something went wrong')
finally:
    fp.close()
```
以上代码我们对可能发生异常的代码处进行 try 捕获，发生异常时执行  except 代码块，finally 代码块是无论什么情况都会执行，所以文件会被关闭，不会因为执行异常而占用资源。

```python
# 使用 with 关键字：

with open('./temp3.txt', 'w') as fp:
    fp.write('Now the file has one more line!\n')

# 查看文件是否关闭
print(fp.closed)
```

使用 **with** 关键字系统会自动调用 f.close() 方法， with 的作用等效于 try/finally 语句是一样的。

我们还可以在执行 with 关键字后检验文件是否关闭。

with 语句实现原理建立在上下文管理器之上。

上下文管理器是一个实现 `__enter__` 和 `__exit__` 方法的类。

使用 with 语句确保在嵌套块的末尾调用 `__exit__` 方法。

这个概念类似于 try...finally 块的使用。

在文件对象中定义了 `__enter__` 和 `__exit__` 方法，即文件对象也实现了上下文管理器，首先调用 `__enter__` 方法，然后执行 with 语句中的代码，最后调用 `__exit__` 方法。 即使出现错误，也会调用 `__exit__` 方法，也就是会关闭文件流。
