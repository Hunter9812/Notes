[oeasy](http://oeasy.org)老师的vim教程

# .vimrc

```vimrc
# 将ESC键映射为两次j键
inoremap jj <Esc>
noremap ; :
# 强制起手式
map <Left> <Nop>
map <Right> <Nop>
map <Up> <Nop>
map <Down> <Nop>
```

# vim基本模式

+ 正常模式、命令模式 (Normal-mode)
  + esc 退回到命令模式 `Normal mode`，或者 ctrl+c 回到命令模式 `Normal mode`
+ 插入模式 (Insert-mode)
+ 命令行模式(Command-Line mode)
  + 一般是通过 : 执行单行命令，通过 / 和 ? 进行搜索
+ 可视模式 (Visual-mode)
  + 在正常模式按下`v, V, <Ctrl>+v`，可以进入可视模式。
+ 选择模式 (Select mode)
+ 多行命令执行模式 (Ex[Execute] mode)
  + 在 `Normal` 正常模式下使用 gQ 进入
  + 使用 `:visual` 退出

# 常用命令

+ 使用 h（左）、j（下）、k（上）、l（右） 移动光标
+ Shift + zz：保存退出
+ Shift + zq：不保存退出

# 组合

- vim快速选中、删除、复制、修改引号或括号内的内容

  分别更改这些配对标点符号中的文本内容
  ci’、ci”、ci(、ci[、ci{、ci< -

  分别删除这些配对标点符号中的文本内容
  di’、di”、di(或dib、di[、di{或diB、di< -

  分别复制这些配对标点符号中的文本内容
  yi’、yi”、yi(、yi[、yi{、yi< -

  分别选中这些配对标点符号中的文本内容
  vi’、vi”、vi(、vi[、vi{、vi< -

# 分屏

- **水平方向分屏打开新文件**

  :sp linuxmi.py

  :split linuxmi.py

- **垂直方向分屏打开新文件**

  :vsp linux.py

  :vsplit linux.py

- :sview linux.py ->只读分屏打开文件

  另外，打开窗口编辑一个新的文件时，可以用以下命令：

  :new

- **从命令行直接打开多个文件且是分屏**

  vim -On file1, file2 ... ->垂直分屏

  vim -on file1, file2 ... ->水平分屏

- **横屏/竖屏分屏打开当前文件**

  ctrl+w s
  ctrl+w v

- **切换分屏**

  ctrl+w h,j,k,l
  ctrl+w 上下左右键






# 初步接触

## 使用帮助

### 使用帮助文件📕

什么不会就 `:help` 什么

`:help` 命令有两种写法

- 完整 `:help`
- 简写 `:h`

```bash
#使用 help 查询帮助
:help Normal
#或者把 help 简写成 h
:h Normal
```

###  vim 的 6 种基本模式

- 正常模式

    ```
    (Normal mode)
    ```

    - 也叫默认模式。
    - 进入 `vim` 时默认的模式所有输入的键都直接对应着命令
    - 也被叫做命令模式.

- 插入模式

    ```
    (Insert mode)
    ```

    - 任何键盘录入都会插入到当前文档中

- 可视模式

    ```
    (Visual mode)
    ```

    - 很像正常模式
    - 但是移动命令会改变选中的一块高亮区域
    - 执行的命令会对选定范围进行

- 选择模式

    ```
    (Select mode)
    ```

    - 可以用鼠标或光标键高亮选择文本
    - 任何输入都会替换选择的高亮文本
    - 并进入插入模式

- 命令行模式

    ```
    (Command-Line mode)
    ```

    - 可以窗口下方执行一条命令
    - 一般是通过 : 执行单行命令
    - 通过 / 和 ? 进行搜索

- Ex mode

    ```
    (多行命令执行模式)
    ```

    - `Ex` 指的是 `Execute`
    - 在 `Normal` 正常模式下使用 gQ 进入
    - 使用 `:visual` 退出

## 打开文件

使用 `:file`

- 可以在状态栏看到当前文件的信息
- `:file` 有详细的帮助吗？
- 输入命令 `:h :file`，查一下

- ```
    :f[ile]
    ```

    可简写为

    - `:fi`
    - `:f`

- 使用 ctrl+G 也有同样的作用

## 深入帮助

## 起源

- `vim` 起源于 `vi`
- `vi` 早期是 Bill Joy 在 `adm3A` 上制作和使用的
- `adm3A` 是一台终端
- `adm3A` 的键盘没有方向键
- 所以这个习惯就延续的到了今天⚠️

### 键盘核心区

**可以使用 h、j、k、l 按键控制光标。**

- 在使用 vim 时，咱们可以把手放在键盘核心区有助于提高效率
    - 将左手食指放在 f 上
    - 将右手食指放在 j 上

### 键盘跳转

+ 运行 `:help` 回到主题开头
+ 我们可以看到 `bars` 这样的链接
+ 使用 h、j、k、l 移动光标
+ 把光标移动到链接上
+ 是 ctrl+] 就可以**跳入链接**
+ ctrl+o 可以**跳出链接**，回到原位置 `older position`

### 两套手册

- 在翻阅 vim 的 manual 的时候
- 我们发现 vim 有两套 manual

一套是用户手册

- 像一本书一样
- 从头读到尾
- 从简单到复杂
- 适合初学

另一套是引用手册

- 精确的描述每个主题
- 以及主题内容是如何工作的
- 适合查询

# 插入模式

按下 i 进入插入模式

输入完成之后，又想要移动位置怎么办呢？

- esc 退回到命令模式 `Normal mode`
- 或者 ctrl+c 回到命令模式 `Normal mode`

# 基础模式

# 保存修改

## 保存文件

 `saveas {file}`：`另存为`

## 直接存储

### write 命令

- 复杂写法是 `:write`
- 简单写法是 `:w`

### vim的报错

- 再修改一下文件
    - `[+]` 又出来了
- 如果没有保存文件就想`:q`的话
- 会报 `E37` 错误

### 查询报错

- 我们明确地知道错误是E37
- 那么我们就查询报错信息
- 我们可以直接`:h E37`查询这个错误的详细信息

# 从头插入

## 插入命令

- 首先我们可以查询这个插入命令的帮助📕
- `:help insert`
- 简写为 `:h i`

### 切换模式

- 我们可以 i 进入插入模式
- esc 回到正常模式
- 然后反复切换
- 观察状态栏下面的提示
    - `--插入--` 就是插入模式
    - 啥都没有就是正常模式

### 重复插入

- 我们可以先点击 i 进入插入模式
- 输入 `oeasy 空格`
- ctrl+c 回到正常模式
- 在正常模式下，按下 . 可以重复刚才的操作
- 再按下 . 可以再重复刚才的操作
- 还按下 . 可以还重复刚才的操作
- 这个 . 是什么意思
- `:h .`

### 撤销插入

- 在正常状态下按下

    u

    可撤销操作

    - 按一次u撤销一步
    - 再按u再撤销
    - 还按u还撤销
    - 一直u按到头，就撤销到头

### 重做

- 反悔是重做
- 就在 `u` 的帮助下面有介绍
- ctrl+r
- 在正常状态下按 ctrl+r 可撤销撤销操作
- 就是重做
    - 按一次 u 撤销一步
    - 再 ctrl+r 再撤销撤销
    - 按一次 u 撤销一步
    - 再 ctrl+r 再撤销撤销
    - 好像可以来回来去拉锯

## 在前方插入

- 比如我们的光标当前所在的位置，在 `用` 字的位置
- 按下 i 进入到插入模式
- 然后就在绿色的光标前面插入字符
- 这就是所谓的 `before cursor` 的意思
- 就是插在光标之前

### 插在最前面

- 在 `:h i` 帮助的周围可以有命令 `I`
- 如果我们使用大写的 `I`，不管你的光标在什么位置
- 插入位置在光标所在行所有文本的 **最** 前面
- 然后切换到插入模式

## 追加文本

- `i` 和 `a` 都是 `Insert mode commands`
- 插入位置
    - `i` 是 `before cursor` 在光标前插
    - `a` 是 `after cursor` 在光标后插
- 对应命令
    - `i` 意思是 `insert`
    - `a` 意思是 `append`

+ 用 `A` 在本行 **最后** 插入
+ `:h A`
+ 就像用 `I` 在本行最前面插入一样

### 追加写入

如果我们保存了当前文件 `oeasy.log`

然后退出了 vi

然后重新进入 vi

在一个未命名文件中写一些东西，比如

- `oeasyo2zo3z`

```
:w >> oeasy.log
```

- 这就是用追加的方式去写这个log文件
- log中的东西还都有
- 最新的追加在最后

与 `:w oeasy.log` 对比

- `:w oeasy` 是覆盖写入
- `>>` 意味着追加写入

## 换行插入

### **下方** 插新行

- 当前绿色的光标在第6行中间
    - 如果不显示行号，就输入 `:set nu`
    - 当前模式是正常模式
- 如果我按下 o
    - 就会在第 7 行插入一个新行
    - 并且模式进入插入模式
- 按 ctrl+c
    - 可以回正常模式
- o、ctrl+c
    - 可以反复切换

### **上方** 插新行

- u 回到最初
- 回到第 6 行中间位置
- 我按下 O
    - 就在第 6 行插入一个空行
    - 原来的第 7 行，变成了第 6 行
    - 并把模式改为输入模式

# 基础移动

## 基本移动

### 模式切换小技巧

- 比如你在一句话的中间，并处于插入模式，此时你想要写下一行
    - 从插入模式到正常模式要用 esc
    - 但是 esc 距离基本起手势太遥远了
    - 可以用 ctrl + c 来替代
    - 左手小拇指 ctrl + c
    - 然后 A 回车
- 可这仍然很慢
- 有没有更有效率的方法呢？

### 插入-普通模式

- ```
    插入普通模式
    ```

    - 就是让你执行一次 `普通模式` 的命令
    - 比如插入模式下
    - 光标在行中间
    - ctrl + o进入插入普通模式
    - o
    - 然后继续保持在 `插入模式`
