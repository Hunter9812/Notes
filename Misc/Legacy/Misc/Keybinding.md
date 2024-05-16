# 软件

## VsCode

https://blog.csdn.net/javanbme/article/details/111597518

### 常用快捷键

- 窗口操作
  - 文件之间切换:   Ctrl+Tab
  - 切出一个新的编辑器窗口（最多3个):   Ctrl+\
  - 切换左中右3个编辑器窗口的快捷键:   Ctrl+1  Ctrl+2  Ctrl+3
- 代码编辑
  - 裁剪尾随空格：<c-k c-x>
  - 代码格式化:   Shift+Alt+F
  - 向上或向下移动一行:   Alt+Up 或 Alt+Down
  - 向上或向下复制一行:   Shift+Alt+Up 或 Shift+Alt+Down
  - 在当前行下方插入一行:   Ctrl+Enter
  - 在当前行上方插入一行:   Ctrl+Shift+Enter
  - 删除当前行:   Ctrl+Shift+K

3. 批量操作

```txt
查找:  Ctrl+F

查找文件:  Ctrl+P

查找替换:  Ctrl+H

多行合并:  Ctrl+J

单词选择:  (局部) Ctrl+D  选中你需要的单词  多次按快捷键会自动往下寻找

单词选择:  (全局) Ctrl + Shift + L  选中你需要的单词

快速复制行:  Alt + Shift + 下键

多行光标:  按住Ctrl + Alt,再按键盘上向上或者向下的键,可以使一列上出现多个光标

自定义列光标: 按住Alt，用鼠标左键点击，可以出现多个光标，输入的代码可以在光标处同时增加

多行选中:  多行光标定位后按住Shift 左右键控制选中

多行变一行: 多行选中按Ctrl + J
```

## Intellij IDEA

1. alt + 鼠标左键 : 整行编辑

1. 生成返回值对象

   ```
   1、先创建一个对象
   2、把光标定格在需要生成返回值对象语句的前面或者后面
   3、右键选择依次点击 Refactor------>Extract------>Variable，也可以使用快捷键ctrl+alt+v
   4、可以自定义生成返回值对象
   ```

2. 捕获异常(try catch)

   ```
   使用快捷键Ctrl+Alt+t 有的使用快捷键Ctrl+Alt+t不行,就使用快捷键Ctrl+Win+Alt+t
   ```

3. 代码进行上下移动

   ```
   Shift+Alt +方向上下键

   上下移动
   【Alt】+【Shift】+【↑，↓】：选中代码上下移动
   【Ctrl】+【Shift】+【↑，↓】：
   1、选中代码中不包含⽅法名，选中代码在所在⽅法中上下移动
   选中的148⾏代码不包含⽅法名，选中代码在所在⽅法内部（147-149⾏之间）上下移动
   2、选中代码中包含⽅法名，选中代码带着所属的整个⽅法上下移动
   选中的146⾏代码包含⽅法名，所属的整个⽅法（145⾏-150⾏）代码上下移动
   ```

4. 调⽤Generate⽣成GetterSetter快捷键

   ```
   快捷键：Alt+Insert
   ```

5. 各种for循环

   ```
   1. 直接输入  for / fori
   直接输入for
       ①. for:  for ()
       ②. fori:  for (int i = 0; i< ; i++) { }
   2.  数字.for :
   数字.for
       ①. 数字.fori:     i自增
       ②. 数字. forr:    i自减
   3. 直接输入iter  增强for循环
   iter增强for循环

   4. 直接输入 itit  生成iterator 迭代
    itit  生成iterator 迭代

   5. 直接输入 itli 生成List的遍历
   itli 生成List的遍历

   6. 直接输入 itve  生成Vector数组迭代
   itve 生成Vector数组迭代

   7. 直接输入  ittok  生成String token遍历
   ittok  生成String token遍历

   8.  直接输入 iten 生成enumeration遍历
   iten 生成enumeration遍历

   9.  直接输入 itco 生成Collection迭代
   itco 生成Collection迭代

   10. 直接输入 itar 生成array for代码块
   for (int i = 0; i < array.length; i++) {
       = array[i];
   }
   ```




## Eclipse

1. alt+/：自动补全。

   ctrl+/：注释

   ctrl+1：获取输入建议。

   ctrl+enter：可以直接在代码中间切换到下一行。

   ctrl+shit+f：自动格式化代码。

   输入main后+ctrl+/：快速输入main方法。

   输入syso+ctrl+/：快速输入System.out.println();

   ctrl+D：直接删除选中的那行或多行代码。

   ctrl+alt+向上方向键或向下方向键：将光标所在行的代码快速向上或向下复制一行。

   双击开始或结束的大括号、引号、小括号：快速选中符号内的内容。

   双击单词：快速选中该单词。

   ctrl+enter:快速切换到下一行

   ctrl+shift+o:自动引包

   shift+alt+s：快速打出getter/setter/构造方法/toString方法等。

   ```
   建一个set和get方法，快捷键为“alt+shift+s”,然后再按一下“r”。
   建一个无参函数，快捷键为“alt+shift+s”,然后再按一下“c”。
   建一个有参函数，快捷键为“alt+shift+s”,然后再按一下“o”。
   ```

   ctrl+shift+s：保存所有文件

2. 工具栏 -> windows -> Preferences
   Java -> Editor -> Concent Assist -> Auto Activation -> Auto activation triggers for Java:(为Java添加自动激活触发器)
   添加以下

   ```
   .1234567890abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
   ```

3. eclipse设置滚动大小

4. 生成返回值对象

   ```
   把鼠标光标移动到分号后面,同时按住ctrl+1,选中Assign statement to new local varible,
   也可以选中下面那个什么Assign statement to new field,但是后面那个是添加类似于全局变量的变量。具体需要选中哪个看你自己需求。这样就可以在Eclipse中快速添加返回值对象
   ```



## Typora

**一：菜单栏**

 文件：alt+F
 编辑：alt+E
 段落：alt+P
 格式：alt+O
 视图：alt+V
 主题：alt+T
 帮助：alt+H

**二：文件**

 新建：Ctrl+N
 新建窗口：Ctrl+Shift+N
 打开：Ctrl+O
 快速打开：Ctrl+P
 保存：Ctrl+S
 另存为：Ctrl+Shift+S
 偏好：Ctrl+,
 关闭：Ctrl+W

**三：编辑**

 撤销：Ctrl+Z
 重做：Ctrl+Y
 剪切：Ctrl+X
 复制：Ctrl+C
 粘贴：Ctrl+V
 复制为MarkDown：Ctrl+Shift+C
 粘贴为纯文本：Ctrl+Shift+V
 全选：Ctrl+A
 选中当前行/句：Ctrl+L
 选中当前格式文本：Ctrl+E
 选中当前词：Ctrl+D
 跳转到文首：Ctrl+Home
 跳转到所选内容：Ctrl+J
 跳转到文末：Ctrl+End
 查找：Ctrl+F
 查找下一个：F3
 查找上一个：Shift+F3
 替换：Ctrl+H

**四：段落**

 标题：Ctrl+1/2/3/4/5
 段落：Ctrl+0
 增大标题级别：Ctrl+=
 减少标题级别：Ctrl±
 表格：Ctrl+T
 代码块：Ctrl+Shift+K
 公式块：Ctrl+Shift+M
 引用：Ctrl+Shift+Q
 有序列表：Ctrl+Shift+[
 [无序列表](https://so.csdn.net/so/search?q=无序列表&spm=1001.2101.3001.7020)：Ctrl+Shift+] 增加缩进：Ctrl+] 减少缩进：Ctrl+[

**五：格式**

 加粗：Ctrl+B
 斜体：Ctrl+I
 下划线：Ctrl+U
 代码：Ctrl+Shift+`
 删除线：Alt+Shift+5
 超链接：Ctrl+K
 图像：Ctrl+Shift+I
 清除样式：Ctrl+

**六：视图**

 显示隐藏侧边栏：Ctrl+Shift+L
 大纲视图：Ctrl+Shift+1
 文档列表视图：Ctrl+Shift+2
 文件树视图：Ctrl+Shift+3
 源代码模式：Ctrl+/
 专注模式：F8
 打字机模式：F9
 切换全屏：F11
 实际大小：Ctrl+Shift+0
 放大：Ctrl+Shift+=
 缩小：Ctrl+Shift±
 应用内窗口切换：Ctrl+Tab
 打开DevTools：Shift+F12



（切换粗体，斜体，代码范围，删除线和标题）

Keyboard shortcuts (toggle bold, italic, code span, strikethrough and heading)

1. Ctrl + B **切换粗体 (Toggle blod)**
2. Ctrl + I **切换斜体 (Toggle italic)**
3. Ctrl + Shift + ] **切换标题 (上层)[Toggle heading(uplevel)]**
4. Ctrl + Shift + [ **切换标题 (下层)[Toggle heading(downlevel)]**
5. Ctrl + M **切换数学环境 (Toggle math environment)**
6. Alt + C **选中/取消任务列表项**
7. Ctrl + Shift + v **切换预览**
8. Ctrl + k v **切换预览到侧面**

   **小技巧:** 最近发现 markdown 不能换行, 可以使用`<br>`



**Keyboard Shortcuts**

| Key                                                          | Command                                           |
| ------------------------------------------------------------ | ------------------------------------------------- |
| Ctrl + B                                                     | 粗体 Toggle bold                                  |
| Ctrl + I                                                     | 斜体 Toggle italic                                |
| Ctrl + Shift + ]                                             | 改变标题层级 (上层) Toggle heading (uplevel)      |
| Ctrl + Shift + [                                             | 改变标题层级 (下层) Toggle heading (downlevel)    |
| Ctrl + M                                                     | 切换数学环境 Toggle math environment              |
| Alt + C                                                      | 标记或取消任务列表项 Check/Uncheck task list item |
| Ctrl + Shift + V                                             | 切换预览 Toggle preview                           |
| Ctrl + K V                                                   | 切换预览到旁边 Toggle preview to side             |
| Alt + Shift + F                                              | 格式化列表 table formatter                        |
| **这个列表我就用到了最后一个快捷方式, 强迫症问题一下子解决了** |                                                   |



## Navicat

1.ctrl+r 运行当前查询窗口的所有[sql语句](https://so.csdn.net/so/search?q=sql语句&spm=1001.2101.3001.7020)

**2.ctrl+shift+r 只运行选中的sql语句**

3.ctrl+/ 注释sql语句

4.ctrl+shift +/ 解除注释

5.ctrl+q 打开查询窗口

6.ctrl+n 打开一个新的查询窗口

7.ctrl+w 关闭当前查询窗口

8.ctrl+l 删除一行

9.Shift+Home 鼠标在当前一行末尾，按快捷选中当前一行

10.F6: 打开一个mysql命令行窗口

11.F7: 运行从光标当前位置开始的一条完整sql语句

12.大小写转换快捷键

​    Ctrl+Shift+U 转为大写
​    Ctrl+Shift+L 转为小写

## Adobe

**PS**

1. Ctrl + N 新建
2. Ctrl + O 打开
3. D 重置默认背景板
4. Ctrl + Alt + I 设置画布大小
5. Ctrl + S 存储
6. Ctrl + K 首选项
7. Ctrl + Shift + Alt + K 快捷键设置
8. Ctrl + Alt + Y（自定义） 历史记录
9. F7 图层
10. Ctrl + Shift + N 新建图层
11. 隐藏目标图层以外的图层 按住Alt键点击眼睛
12. 复制图层 按住Alt键拖拽图层
13. Ctrl + J 新建拷贝图层在原图层上方

# 浏览器

- 地址栏
  - alt +  <enter> 在新前台标签页打开地址或搜索
  - shift + <enter> 在新窗口打开地址或搜索
- <a-s> + < / >

**基础**

| **Ctrl+N**                                                   | 打开新窗口。                                 |
| ------------------------------------------------------------ | -------------------------------------------- |
| **Ctrl+T**                                                   | 打开新标签页。                               |
| 按 **Ctrl+O**，然后选择文件。                                | 在谷歌浏览器中打开计算机中的文件。           |
| 按住 **Ctrl** 键的同时点击链接。或用鼠标中键（或鼠标滚轮）点击链接。 | 从后台在新标签页中打开链接。                 |
| 按住 **Ctrl+Shift** 的同时点击链接。或按住**Shift** 键的同时用鼠标中键（或鼠标滚轮）点击链接。 | 在新标签页中打开链接并切换到刚打开的标签页。 |
| 按住 **Shift** 键的同时点击链接。                            | 在新窗口中打开链接。                         |
| **Ctrl+Shift+T**                                             | 重新打开上次关闭的标签页。                   |
| 将链接拖到标签页中。                                         | 在标签页中打开链接。                         |
| 将链接拖到标签栏的空白区域。                                 | 在新标签页中打开链接。                       |
| 将标签页拖出标签栏。                                         | 在新窗口中打开标签页。                       |
| 将标签页从标签栏拖到现有窗口中。                             | 在现有窗口中打开标签页。                     |
| 拖动标签页时按 **Esc** 键。                                  | 将标签页恢复到原先的位置。                   |
| **Ctrl+1** 到 **Ctrl+8**                                     | 切换到标签栏中指定位置编号所对应的标签页。   |
| **Ctrl+9**                                                   | 切换到最后一个标签页。                       |
| **Ctrl+Tab** 或 **Ctrl+PgDown**                              | 切换到下一个标签页。                         |
| **Ctrl+Shift+Tab** 或 **Ctrl+PgUp**                          | 切换到上一个标签页。                         |
| **Alt+F4**                                                   | 关闭当前窗口。                               |
| **Ctrl+W** 或 **Ctrl+F4**                                    | 关闭当前标签页或弹出窗口。                   |
| **用鼠标中键（或鼠标滚轮）点击标签页。**                     | 关闭所点击的标签页。                         |
| 右键点击或者点击并按住浏览器工具栏中的“后退”或“前进”箭头。   | 在新标签页中显示浏览历史记录。               |
| 按 **Backspace** 键，或同时按 **Alt** 和向左箭头键。         | 转到当前标签页的上一页浏览历史记录。         |
| 按 **Shift+Backspace**，或同时按 **Alt** 和向右箭头键。      | 转到当前标签页的下一页浏览历史记录。         |
| 按住 **Ctrl** 键的同时点击工具栏中的后退箭头、前进箭头或转到按钮。或用鼠标中键（或鼠标滚轮）点击任一按钮。 | 从后台在新标签页中打开按钮所对应的目标网页。 |
| **双击标签栏的空白区域。**                                   | 最大化或最小化窗口。                         |
| **Alt+Home**                                                 | 在当前窗口打开主页。                         |


# window 10

- Win+Q 或者 Win+S 搜索
- Win + K 连接设备
- Win + A 打开通知栏
- Ctrl + Shift + N 新建文件夹
- win + <up>/<down> 放大缩小窗口

- 移动复制

  1、用鼠标左键选中文件拖动是复制：同一个磁盘盘符内的拖动操作是移动，不同的磁盘盘符之间的拖动是复制操作，
  2、用鼠标右键选中文件拖动是移动：不区分是否在同一个磁盘盘符内或不同的磁盘盘符之间的拖动。
  PS：桌面一般是c盘，从D、E等盘拖动到桌面是不同的盘符之间的拖动，是复制操作。如果想移动可以右键点击文件选择“剪切”或用鼠标右键选中文件拖动是移动。
  3、按住Ctrl键拖动是创建复制，按住Alt键拖动是创建链接

- 在指定文件夹打开cmd

  在平时我们在windows环境中要打开cmd并进入一个指定的文件夹，需要先打开cmd，进入指定的分区，然后再一步步地cd到指定的文件夹，这些操作是有些繁琐的，那么下面介绍两种快捷地进入指定文件夹的cmd的方法。
  **方法一**

  先打开指定的文件夹（explore中），然后选中地址栏（此时默认选中了地址栏中的所有路径，将其覆盖即可），然后输入cmd，回车，便可以打开对应路径的cmd窗口了。
  **方法二**

  与方法一同样，先进入需要的文件夹，按住shift键，右键空白区域，在选项中，有一个在此处打开Powershell窗口的选项，点击即可。

  注：如果对于Powershell并不熟悉，可以简单地认为Powershell是cmd的一个加强版，即cmd能做的事情，Powershell都可以做。

## 命令运行框

常用

- `shell:Start Menu` 打开开始菜单文件夹

**cmd**---------打开Windows控制台命令窗口

**write**----------打开写字板

**notepad**--------打开记事本

**mspaint**--------打开画图工具

**calc**-----------启动计算器

**utilman**--------辅助工具管理器

**osk**------------打开屏幕键盘

**Clipbrd**--------剪贴板查看器

**mstsc**----------远程桌面连接

**magnify**--------放大镜实用程序

**taskmgr**--------任务管理器

**explorer**-------打开资源管理器

**regedit.exe**----注册表

**regedt32**-------注册表编辑器

**progman**--------程序管理器

**devmgmt.msc**--- 设备管理器

**compmgmt.msc**---计算机管理

**mplayer2**-------打开系统播放器

**wmplayer**-------打开系统播放器

**dvdplay**-------打开系统播放器

**rononce -p** ----15秒关机

**tsshutdn**-------60秒倒计时关机命令

**winver**---------检查Windows版本

**wmimgmt.msc**----打开windows管理体系结构(WMI)

**wscript**--------windows脚本宿主设置

**wiaacmgr**-------扫描仪和照相机向导（要安装了才能使用）

**Msconfig.exe**---系统配置实用程序

**mmc**------------打开控制台

**mobsync**--------同步命令

**dxdiag**---------检查DirectX信息

**diskmgmt.msc**---磁盘管理实用程序

**dcomcnfg**-------打开系统组件服务

**net stop messenger**-----停止信使服务

**net start messenger**----开始信使服务

**nslookup**-------网络管理的工具向导

**ntbackup**-------系统备份和还原

**narrator**-------屏幕“讲述人”

**ntmsmgr.msc**----移动存储管理器

**ntmsoprq.msc**---移动存储管理员操作请求

**netstat -an**----(TC)命令检查接口

**syncapp**--------创建一个公文包

**sysedit**--------系统配置编辑器

**sigverif**-------文件签名验证程序

**shrpubw**--------创建共享文件夹

**secpol.msc**-----本地安全策略

**services.msc**---本地服务设置

**sfc.exe**--------系统文件检查器

**eventvwr**-------事件查看器

**eudcedit**-------造字程序

**perfmon.msc**----计算机性能监测程序

**chkdsk.exe**-----Chkdsk磁盘检查

**certmgr.msc**----证书管理实用程序

**charmap**--------启动字符映射表

**cliconfg**-------SQL SERVER 客户端网络实用程序

**cleanmgr**-------垃圾整理

**ciadv.msc**------索引服务程序

**lusrmgr.msc**----本机用户和组

**logoff**---------注销命令

**iexpress**-------木马捆绑工具，系统自带

**Nslookup**-------IP地址侦测器

**fsmgmt.msc**-----共享文件夹管理器

# Linux

## Ubuntu

    Super 键：打开活动搜索界面
    Ctrl+Alt+T：打开 Ubuntu 终端窗口
    Super+L 或 Ctrl+Alt+L：锁屏
    Super+D or Ctrl+Alt+D：显示桌面
    Super+A：显示应用程序菜单
    Super+Tab 或 Alt+Tab：在运行中的应用程序间切换
    Super+箭头：移动窗口位置
    Super+M：切换到通知栏
    Super+空格：切换输入法（用于多语言设置）
    Alt+F2：运行控制台
    Ctrl+Q：关闭应用程序窗口
    Ctrl+Alt+箭头：切换工作区
    Ctrl+Alt+Del：注销
    DIY 快捷键
