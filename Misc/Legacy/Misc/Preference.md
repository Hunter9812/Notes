﻿﻿﻿# IDE

## VsCode

+ **vscode 配置新建文件夹快捷键**

  (when 属性 实现快捷键仅在在获取左侧项目栏文件夹焦点情况下生效)

  https://www.jianshu.com/p/5d6bb30bd326?utm_campaign=maleskine

  ```json
  // keybindings.json
  // Place your key bindings in this file to override the defaults
  [
     {
        "key": "a",
        "command": "explorer.newFile",
        "when": "explorerResourceIsFolder"
     },
     {
        "key": "shift+a",
        "command": "explorer.newFolder",
        "when": "explorerResourceIsFolder"
     }
  ]
  ```

+ **密钥`externalConsole`已弃用 请改用“console”**

  具体解决办法是：`将launch.json里的cppvsdbg中原来的"externalConsole":true改成"console":"externalTerminal"`

+ **修改vscode默认html快捷模板**

  VsCode 可以通过 `! + tab` 方式快速生成html结构，这是大家都知道的事情。
  我习惯使用 live server 插件来做前端页面的服务器环境测试，但一个比较让人讨厌的地方在于，在服务器环境下，浏览器总是会自动请求 `favicon.ico` 文件，加载失败还会在控制台输出 404 错误提示。
   在忍了一段时间之后终于还是忍不住了，于是百度了一下修改默认模板的方法，记录下来，方便以后查阅。

  > 注意： vscode 版本不同，要修改的文件有所不同，但大概的方向是一致的。

  ------

  **较老一些版本的修改路径**

  通过以下路径找到模板文件：



  ```cmd
  {VScode安装路径}\resources\app\extensions\emmet\node_modules\vscode-emmet-helper\out\expand\expand-full.js
  ```

  打开 `expand-full.js` 文件，查找 '!' 或者 'doc' ，定位到模板语法位置，大概内容是这样：



  ```xml
  "!!!":"{<!DOCTYPE html>}",doc:"html[lang=${lang}]>(head>meta[charset=${charset}]+meta[http-equiv='X-UA-Compatible'][content='IE=edge']+meta:vp
  ```

  注意这只是片段，前后还有其他代码。
   doc: 后面就是html结构模板了，要添加或者删除什么，只需要遵守 emmet 语法即可。
   建议先备份一下，再修改。

  **`修改之后要关闭模板文件和vscode，再重新打开vscode 才会生效。`**

------

  **较新版本的修改路径**

  通过以下路径找到模板文件：



  ```cmd
  {VScode安装路径}\resources\app\extensions\emmet\dist\node\emmetNodeMain.js
  ```

  打开 `emmetNodeMain.js` 文件。
   接下来的步骤与上面是相同的。

------

  如果你的版本与上面的两种方式的路径都不相同，可以自己尝试查找名称中有 emmet 的文件夹，基本上模板就在这个文件夹中了。

  解决请求 favicon.ico 失败的 404 错误的方法是添加以下标签内容到模板的head中：



  ```html
  <link rel="icon" href="data:image/ico;base64,=">
  ```

  这是html文件中的修改方式，如果要修改 vscode 模板，按照上面说的找到 html 结构片段，然后在已有的 emmet 语法中新增：



  ```js
  link[rel='icon'][href='data:image/ico;base64,=']
  ```

  我是添加在 viewport 标签下面的，新增之后的大概的代码片段是这样：



  ```ruby
  meta:vp+title{${1:Document}})+link[rel='icon'][href='data:image/ico;base64,=']+body
  ```

  我还将lang的值改成了 zh-CN, 最终的效果：



  ```html
  <!DOCTYPE html>
  <html lang="zh-CN">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <link rel="icon" href="data:image/ico;base64,=">
  <body>

  </body>
  </html>
  ```

  **上面补充**

  英文lang=en修改为中文lang=zh-CN
  第一步：先把vscode编辑器打开，进入设置中
  第二步：搜索设置项emmet.variables第三步：点击下面的添加项，把默认的en修改成zh-CN

  ![增加项后默认会出现，把en改成zh-CN确认保存.png](https://www.mainblog.cn/zb_users/upload/2021/07/202107031026477662745.png)
  第四步：基本就OK了，仅需回去新建一个html文档测试一下修改的效果就好。

+ **VS code 中的各种变量 ${file},${fileBasename}**

  2017年08月24日 11:14:07 [bailsong](https://me.csdn.net/bailsong) 阅读数：7108



   from: https://blog.csdn.net/bailsong/article/details/77527773

  这几天刚刚接触vscode ，用它写c,在编译的时候需要设置tasks.json,其中遇到了各种${},比如${file},${fileBasename}等等等等，

  神烦，网上搜不到，最终还是在VS code的帮助里边找的，先把链接贴上https://code.visualstudio.com/docs/editor/tasks#vscode

  介绍一下有关 文件之类的，

  ```txt
  ${workspaceRoot} 当前打开的文件夹的绝对路径+文件夹的名字
  ${workspaceRootFolderName}  当前打开的文件夹的名字
  ${file} 当前打开正在编辑的文件名，包括绝对路径，文件名，文件后缀名
  ${relativeFile} 从当前打开的文件夹到当前打开的文件的路径
  如 当前打开的是test文件夹，当前的打开的是main.c，并有test / first / second / main.c
  那么此变量代表的是  first / second / main.c
  ${fileBasename} 当前打开的文件名+后缀名，不包括路径
  ${fileBasenameNoExtension} 当前打开的文件的文件名，不包括路径和后缀名
  ${fileDirname} 当前打开的文件所在的绝对路径，不包括文件名
  ${fileExtname} 当前打开的文件的后缀名
  ${cwd} the task runner's current working directory on startup
  不知道怎么描述，这是原文解释，
  跟 cmd 里面的 cwd 是一样的
  ${lineNumber} 当前打开的文件，光标所在的行数
  ```

   以上只是一部分，具体请到连接处。

  要注意的是，大小写不能错，一个字都不能错，而且还没有提示。

  说了这么多，你一定发现有几个字出现的挺多，"当前打开的" ，确实挺多的。希望对你有帮助。

+ **[vscode插件之C/C++](https://www.cnblogs.com/hugechuanqi/p/10503072.html)**

  1、给C/C++调试器配置`launch.json`

  - `launch.json`用于在VS Code中配置调试器；带着关于生成器几乎所有需要的信息。
  - 需要将用于计划调试的可执行文件的路径填充在program字段；必须在launch和attach配置信息中填充。
  - 生成的文件包含两个部分，一个为launch配置调试，一个为attach配置调试。

  2、配置VS Code的调试行为

  - 调试期间可以通过设置和改变下列选项来控制VS Code的行为：

  1. program：指定执行debugger的完整路径。
  2. symbolSearchPath：告诉windows调试器搜索`.pdb`文件的路径。如果有多个路径，则用分号分开，例如：`C:\\Symbols;C:\\SymbolDir2`。
  3. additionalSOLibSearchPath：告知GDB或者LLD去搜索`.so`文件的路径。如果有多个路径，用`;`隔开。
     - GDB：UNIX及UNIX-like下的调试工具。
     - LLDB：LLDB是个开源的内置于XCode的具有REPL(read-eval-print-loop)特征的Debugger，其可以安装C++或者Python插件。LLDB是个开源的内置于XCode的具有REPL(read-eval-print-loop)特征的Debugger，其可以安装C++或者Python插件。
  4. externalConsole
     - windows：如果设置为`True`，它将生成外部控制台；如果设置为`false`，则将会使用VS Code的集成终端；
     - Linux：如果设置为`True`，它将通知VS Code去生成一个外部控制台；如果设置为`false`，则将会使用VS Code的集成终端；
  5. avoidWindowsConsoleRedirection：为了在Windows上支持VSCode与gdb的集成终端，扩展将控制台重定向命令添加到debuggee的参数中，以便在集成终端中显示控制台输入和输出。将此选项设置为`true`将禁用它。
  6. logging：可选标志，以确定应该将哪些类型的消息记录到调试控制台。
     - exceptions：默认为`true`，确定是否应该将异常消息记录到调试控制台。
     - moduleLoad：默认为`true`，确定是否应该将模块加载事件记录到调试控制台。
     - programOutput：默认为`true`，确定是否应该将程序输出记录到调试控制台。
     - engineLogging：默认为`false`，确定是否应该将诊断引擎日志记录到调试控制台。
     - trace：默认为`false`，确定是否应该将诊断适配器命令跟踪记录到调试控制台。
     - traceResponse：默认为`false`，确定是否应该将诊断适配器命令和响应跟踪记录到调试控制台。
  7. visualizerFile：调试时`.natvls`文件将被使用。
  8. showDisplayString：当指定visualizerFile时，showDisplayString将启用显示字符串，打开此选项会导致调试期间性能下降。

  举例：

  ```vscode,material
  {
     "name": "C++ Launch (Windows)",
     "type": "cppvsdbg",
     "request": "launch",
     "program": "C:\\app1\\Debug\\app1.exe",
     "symbolSearchPath": "C:\\Symbols;C:\\SymbolDir2",
     "externalConsole": true,
     "logging": {
         "moduleLoad": false,
         "trace": true
      },
     "visualizerFile": "${workspaceRoot}/my.natvis",
     "showDisplayString": true
  }
  ```

  3、配置目标应用

  下列选项可让你在目标应用程式启动时修改其状态：

  1. args：启动程序时传递给程序的命令行参数的JSON数组。例如 ["arg1", "arg2"]，如果要转义字符，则需要对其进行两次转义。例如["{\"arg\": true}]将向您的应用程序发送{"arg1": true}。
  2. cwd：设置调试器启动的应用程序的工作目录。
  3. enviroment：要添加到程序环境中的环境变量。

  举例：

  ```vscode,material
  {
     "name": "C++ Launch",
     "type": "cppdbg",
     "request": "launch",
     "program": "${workspaceRoot}/a.out",
     "args": ["arg1", "arg2"],
     "environment": [{"name": "squid", "value": "clam"}],
     "cwd": "${workspaceRoot}"
  }
  ```

  4、自定义GDB或者LLDB

  下列选项可让你改变GDB或者LLDB的行为：

  1. MIMode：指示VS代码将连接到的调试器。必须设置为gdb或lldb。这是根据每个操作系统预先配置的，可以根据需要进行更改。
  2. miDebuggerPath：调试器(如gdb)的路径。当只指定可执行文件时，它将为调试器搜索操作系统的路径变量(Linux和Windows上的GDB, OS X上的LLDB)。
  3. miDebuggerArgs：传递给调试器的其他参数(如gdb)。
  4. stopAtEntry：如果设置为true，调试器应该在目标的入口点停止(在附加时忽略)。默认值为false。
  5. setupCommands：要执行的命令的JSON数组，以便设置GDB或LLDB。例如:"setupCommands":  [{"text": "target-run"， "description": "run target"， " ignorefailure ":  false}]
  6. customLaunchSetupCommands：如果提供了，这将用一些其他命令替换用于启动目标的默认命令。例如，这可以是“-target-attach”以便附加到目标进程。空命令列表将用空命令替换启动命令，如果将启动选项作为命令行选项提供给调试器，这将非常有用。例如:“customLaunchSetupCommands”:[{“text”:“target-run”，“description”:“run target”，“ignorefailure”:false}]。
  7. launchCompleteCommand：调试器完全设置好后要执行的命令，以便使目标进程运行。允许的值是“执行器运行”、“执行器继续”、“None”。默认值是“execl -run”。

  举例：

  ```vscode,material
  {
     "name": "C++ Launch",
     "type": "cppdbg",
     "request": "launch",
     "program": "${workspaceRoot}/a.out",
     "stopAtEntry": false,
     "customLaunchSetupCommands": [
        { "text": "target-run", "description": "run target", "ignoreFailures": false }
     ],
     "launchCompleteCommand": "exec-run",
     "linux": {
        "MIMode": "gdb",
        "miDebuggerPath": "/usr/bin/gdb"
     },
     "osx": {
        "MIMode": "lldb"
     },
     "windows": {
        "MIMode": "gdb",
        "miDebuggerPath": "C:\\MinGw\\bin\\gdb.exe"
     }
  }
  ```

  5、调试dump（转储）文件

  C/ c++扩展允许调试Windows上的dump文件以及Linux和OS X上的core dump文件

  1. dumpPath：如果要调试Windows转储文件，请将此设置为转储文件的路径，以便在启动配置中启动调试。
  2. coreDumPath：要调试指定程序的核心转储文件的完整路径。将其设置为核心转储文件的路径，以便在启动配置中启动调试。注意:MinGw不支持核心转储调试。

  6、远程调试或者本地服务器上调试

  1. miDebuggerServerAddress：调试器服务器(例如gdbserver)的网络地址，以便连接到远程调试(例如:localhost:1234)。
  2. debugServerPath：调试服务器启动的完整路径。
  3. debugServerArgs：调试服务器的参数。
  4. serverStarted：要在调试服务器输出中查找的服务器启动模式。
  5. serverLaunchTimeout：调试器等待debugServer启动的时间(以毫秒为单位)。默认是10000。

  7、其他属性

  1. processId：默认为`${command.pickProcess}`。将显示调试器可以附加到的可用进程列表。建议保留此默认值，但是可以显式地将该属性设置为调试器要附加到的特定进程ID。
  2. request：指示配置节是打算启动程序还是附加到已运行的实例。
  3. targetArchitecture：由于自动检测到目标体系结构，因此不再需要此选项。
  4. type：指示正在使用的底层调试器。使用Visual Studio Windows调试器时必须是cppvsdbg，使用GDB或LLDB时必须是cppdbg。这将在启动时自动设置为正确的值。创建json文件。
  5. sourceFileMap：这允许将源的编译时路径映射到本地源位置。它是键/值对的对象，将解析第一个字符串匹配的路径。(例如:"sourceFileMap": {"/mnt/c":  "c:\"}将映射调试器返回的以/mnt/c开头的任何路径，并将其转换为c:\。对象中可以有多个映射，但它们将按提供的顺序处理。)

  参考：

  1.官网：https://github.com/Microsoft/vscode-cpptools/blob/master/launch.md

  2.csdn博客：https://blog.csdn.net/wzxlovesy/article/details/76708151

  https://blog.csdn.net/g19zwk/article/details/78414226

### 插件

#### vim

- im-select

  [VSCode Vim 自动切换输入法「只需1分钟」](https://zhuanlan.zhihu.com/p/609120496)

  在 VSCode 中使用Vim 插件时，从 insert 模式切换为 normal，此时输入法还是保持 insert 模式的状态

  [im-select](https://github.com/daipeihust/im-select)

  ```json
  "vim.autoSwitchInputMethod.enable": true,
  "vim.autoSwitchInputMethod.defaultIM": "us", // 这是你的系统英文输入法
  "vim.autoSwitchInputMethod.obtainIMCmd": "D:\\scoop\\shims\\im-select.exe",
  "vim.autoSwitchInputMethod.switchIMCmd": "D:\\scoop\\shims\\im-select.exe {im}", // 注意 {im} 前面有空格
  ```



1. Better Comments

   主要是针对行注释，对不同类型的注释会附加不同的颜色，更加方便区分

   ![IMG_20230213_1811_1](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/IMG_20230213_1811_1.png)

2. Peacock    `v4.2.2`    John Papa    2,072,967    (142)

   更改边框颜色

   > Subtly change the color of your Visual Studio Code workspace.
   >
   > 巧妙地更改Visual Studio代码工作区的颜色。

3. IntelliCode    `v1.2.30`    Microsoft    26,381,838    (85)



   > The [Visual Studio IntelliCode](https://go.microsoft.com/fwlink/?linkid=872679) extension provides AI-assisted development features for Python, TypeScript/JavaScript and Java developers in Visual Studio Code, with insights based on understanding your code context combined with machine learning.
   >
   > Visual Studio IntelliCode扩展为Visual Studio Code中的Python、TypeScript/JavaScript和Java开发人员提供Ai辅助开发功能，这些功能基于对代码上下文的理解并结合机器学习。

   IntelliCode API Usage Examples

   > See relevant code examples from GitHub for over 100K different APIs right in your editor.
   >
   > 查看GitHub中的相关代码示例，了解编辑器中超过10万种不同的API。

4. filesize    `v3.1.0`    Matheus Kautzmann    537,361    (14)

   一款在左下角显示文件大小的插件

   > This package is intended for use with the [Visual Studio Code](https://code.visualstudio.com/) editor and it displays the size of the focused file in the status bar of the editor.
   >
   > 此包旨在与Visual Studio代码编辑器一起使用，它在编辑器的状态栏中显示焦点文件的大小。

5. Local History     `v1.8.1`     xyz     578,558    (52)

   你并不需要下它。

   在 VSCode 中，以前需要通过安装插件来实现（例如 Local History 插件），但在 1.44 版本之后，VSCode 内置了时间线（Timeline）功能。

6. Explorer Exclude    `v1.3.2`    Peter Schmalfeldt    41,095    (6)

   隐藏配置文件比较好用

   > Explorer Exclude lets you easily Hide Files & Folders with Dynamic Filter Options. Add a New 'Hidden Items' Explorer Pane for you to …
   >
   > Explorer Exclude让您轻松隐藏文件和文件夹与动态筛选选项。添加新的"隐藏项目"资源管理器窗格，以便…

7. Polacode    `v0.3.4`    P & P    950,823    (54)

   选中代码即可创建截图，没啥用

   > Polaroid for your code
   >
   > 为你的代码拍照

8. Project Manager    `v12.7.0`    Alessandro Fragnani    3,110,287    (119)

   相对于直接Ctrl+R有了收藏夹

   > Easily switch between projects
   >
   > 在项目之间轻松切换

   ```json
   // 我的设置
   {
     "key": "ctrl+shift+q",
     "command": "workbench.view.extension.project-manager",
     "when": "viewContainer.workbench.view.extension.project-manager.enabled"
   }
   ```

9. **Git**

   + Git History    `v0.6.19`    Don Jayamanne    7,745,860    (147)

     > View git log, file history, compare branches or commits
     >
     > 查看git日志、文件历史记录、比较分支或提交

   + GitLens — Git supercharged    `v13.2.0`    GitKraken    20,597,641    (664)

     > GitLens simply helps you **better understand code**. Quickly glimpse into whom, why, and when a line or code block was changed. Jump back through history to **gain further insights** as to how and why the code evolved. Effortlessly explore the history and evolution of a codebase.
     >
     > GitLens只是帮助你**更好地理解代码**。快速了解更改行或代码块的人员、原因和时间。回顾历史，**深入了解**代码是如何演变的以及为什么演变。轻松探索代码库的历史和演变。

10. **主题**

    + GitHub Theme    `v6.3.3`     GitHub

      > GitHub theme for VS Code

    + Peacock    `v1.1.6`    Marnix Koops    6,396    (2)

      试了试，感觉比github的Dark主题要好

      > A vibrant yet elegant dark VS Code theme
      >
      > 充满活力而优雅的黑暗VS代码主题

11. Markdown

     + Markdown All in One    `v3.5.0`    Yu Zhang    5,739,109    (129)

       markdown使用者必备

       > All you need for Markdown (keyboard shortcuts, table of contents, auto preview and more).
       >
       > ***Note***: VS Code has basic Markdown support out-of-the-box (e.g, **Markdown preview**), please see the [official documentation](https://code.visualstudio.com/docs/languages/markdown) for more information.

     + Markdown Preview Enhanced     `v0.6.7`    Yiyi Wang    3,808,814    (91)

       > Markdown Preview Enhanced is an extension that provides you with many useful functionalities such as automatic scroll sync, [math typesetting](https://shd101wyy.github.io/markdown-preview-enhanced/#/math), [mermaid](https://shd101wyy.github.io/markdown-preview-enhanced/#/diagrams?id=mermaid), [PlantUML](https://shd101wyy.github.io/markdown-preview-enhanced/#/diagrams?id=plantuml), [pandoc](https://shd101wyy.github.io/markdown-preview-enhanced/#/pandoc), PDF export, [code chunk](https://shd101wyy.github.io/markdown-preview-enhanced/#/code-chunk), [presentation writer](https://rawgit.com/shd101wyy/markdown-preview-enhanced/master/docs/presentation-intro.html), etc. A lot of its ideas are inspired by [Markdown Preview Plus](https://github.com/atom-community/markdown-preview-plus) and [RStudio Markdown](http://rmarkdown.rstudio.com/).
       >
       > Markdown Preview  Enhanced是一个扩展，它为您提供了许多有用的功能，如自动滚动同步，数学排版，mermaid，PlantUML，pandoc，PDF导出，代码块，演示文稿编写器等。它的很多想法都受到Markdown Preview Plus和RStudio Markdown的启发。

12. HTML

     + Auto Close Tag

       自动闭合HTML/XML标签

     + Auto Rename Tag

       自动完成另一侧标签的同步修改

13. Python

     Python by Microsoft

     这个微软发布的 VS Code 扩展对 Python 有丰富的支持。

     - 使用 Pylint 或 Flake8 或 black 支持为代码进行 Linting
     - 在 VS Code 编辑器中调试代码
     - 支持 Jupyter 笔记本、Pytest

     Python Snippets

     其是由 Ferhat Yaln  开发的内置代码片段包的扩展。这个扩展对开发者非常友好，尤其是对 Python 初学者。它包含许多内置代码段，比如  string、list、sets、tuple、dictionary、class  等等。使用此插件的另一个优点：它还为每个代码段提供了至少一个示例，这对学习 Python 的人来说非常有帮助。

     Pyright

     Pyright 是一个非常快速的静态类型检查器和代码验证器。

     - 必要时自动插入类型提示
     - 根据 PEP8 规则自动重新排序代码中的导入。

     如果你安装了 Pylance 那就不需要安装这个了。

     autoDocstring

     autoDocstring - Python Docstring Generator

     能够自动生成函数的注释格式，通过tab键快速切换填充块编写相应的注释

     Anaconda Extension Pack

    推荐给用anaconda的同学了，大大增强了代码提示功能。原始的代码提示基本只包含了python标准库，有了这个插件之后各种第三方库基本都能实现代码提示了，并且还会额外显示每个方法的帮助

### 主题

https://code.visualstudio.com/docs/getstarted/themes

## IDEA

+ **添加注释时默认顶格**

  1.打开电脑中下载好的`Intellij IDEA`
  2.点击页面菜单栏中的File, 并且在下拉框中点击Settings
  3.在Settings设置页面中点击Editor
  4.点击Editor中的General通用设置
  5.在General通用设置中勾选`Change font size with Ctrl+Mouse Whee`
  6.点击Apply 再 OK按钮, 保存设置即可

+ **添加注释时默认顶格**

  1. **问题描述**

     在IDEA里面使用 `Ctrl` + `/` 添加注释时，会默认添加在顶格。

  2. **解决方式**

     `Settings` -> `Editor` -> `Code Style` -> `Java`，在 `Code Generation` 里面取消勾选两个选项。

     > 对于**其他格式**的文件，在 **`Code Style`** 里找到需要修改的**文件类型**，按照上面的方法进行修改即可。

  3. 两个选项为

     Line comment at first column
     Block comment at first column

+ **项目右键没有run maven选项**

  idea 项目右键没有 run maven 选项，没有 maven 的 clean 与 install 等选项

  安装插件Maven Helper

+ **包目录分级显示**

  在显示目录结构的地方有个小齿轮，里面的Tree Appearance里的设置

  - Flatten Packages：扁平化包
  - Hide Empty Middle Packages：隐藏空的中间包

+ **mapper.xml中的sql语句不提示**

  首先，alt+enter，出现窗口

  点击inject language or reference

  在表列中选择MySQL

# 浏览器

+ 知乎网页在后面加参数后切换黑白模式
  + `?theme=light`
  + `?theme=dark`

## 火狐

### about:config

在浏览器地址栏输入：`about:config`（不包含引号，下同） 并回车，然后点击“接受风险并尝试”，可以进入高级设置界面。

+ 解决火狐浏览器提示连接不安全或证书错误的问题

  `security.enterprise_roots.enabled`：将`false`切换为`true`

+ 用户自定义css

  `toolkit.legacyUserProfileCustomizations.stylesheets`：设置为true

  找到`userChrome.css`文件，修改即可

+ 滚动条样式

  `widget.non-native-theme.scrollbar.style`

  + 0 ：平台默认 滚动条样式
  + 1 ：macOS 滚动条样式
  + 2 ：GTK 滚动条样式
  + 3 ：Android 滚动条样式
  + 4 ：Windows 10 滚动条样式
  + 5 ：Windows 11 滚动条样式

+ 流畅滚动
  [Yet Another Smooth Scrolling](https://addons.mozilla.org/zh-CN/firefox/addon/yass-we/?utm_content=addons-manager-reviews-link&utm_medium=firefox-browser&utm_source=firefox-browser)

  - general.smoothScroll.currentVelocityWeighting
    默认 0.25
    更改 0
  - general.smoothScroll.mouseWheel.durationMaxMS
    默认 200
    更改 250
  - general.smoothScroll.stopDecelerationWeighting
    默认 0.4
    更改 0.82
  - mousewheel.min_line_scroll_amount
    默认 5
    更改 25
  - general.smoothScroll.msdPhysics.enabled
    默认 false
    更改 true

+ 地址栏不隐藏 `http://`

  `browser.urlbar.trimURLs`：`true`改为`false`

+ 单击鼠标中建粘贴剪切板内容

  `middlemouse.paste`：`false`改为`true`

+ 保存到 pocket

  `extensions.pocket.enabled`：`true`改为`false`

+ 搜索显示高亮

  `findbar.highlightAll`

+ 禁用网页自定义右键功能菜单（浏览器右键菜单在最前端）

  `dom.event.contextmenu.enabled`

  设为 true 后可用 shift + 右键实现

+ 地理位置

  `geo.enabled`

+ 地址栏与工具栏

  + 地址栏网址推荐排序比重

    | 名称                                     | 对应         | 初始值 |
    | :--------------------------------------- | ------------ | ------ |
    | places.frecency.bookmarkVisitBonus       | 书签         | 75     |
    | places.frecency.defaultVisitBonus        | 默认         | 0      |
    | places.frecency.downloadVisitBonus       | 下载         | 0      |
    | places.frecency.embedVisitBonus          | 嵌入         | 0      |
    | places.frecency.framedLinkVisitBonus     | 框架链接     | 0      |
    | places.frecency.linkVisitBonus           | 链接         | 100    |
    | places.frecency.permRedirectVisitBonus   | 重定向       | 50     |
    | places.frecency.redirectSourceVisitBonus | 重定向源     | 25     |
    | places.frecency.reloadVisitBonus         | 重新加载     | 0      |
    | places.frecency.tempRedirectVisitBonus   | 临时重定向   | 40     |
    | places.frecency.typedVisitBonus          |              | 2000   |
    | places.frecency.unvisitedBookmarkBonus   | 未访问的书签 | 140    |
    | places.frecency.unvisitedTypedBonus      | 未访问typed  | 200    |

+ 标签页

  + 关闭最后一个标签页时不关闭 Firefox

    `browser.tabs.closeWindowWithLastTab`：`true`改为`false`

  + 转到上/下一页中保存的标签数

    `browser.sessionhistory.max_total_viewers`：默认 -1（无限）

  + 默认用新标签页打开

    + 地址栏： `browser.urlbar.openintab`：Alt+Enter键也能实现
    + 搜索框： `browser.search.openintab`

+ 视频

  + 关闭进入全屏和退出全屏的动画

    `full-screen-api.transition-duration`：数值修改为`0 0`(注意中间空格，原本默认是`200 200`)。

  + 关闭全屏提示

    `full-screen-api.warning.timeout`：把原本的`3000`改为`0`即可

  + 强制启用硬解：

    `media.hardware-video-decoding.force-enabled`

  + 图层加速

    `layers.acceleration.force-enabled`

  + WebRTC
    `media.peerconnection.enabled`

+ 开发

  + 自定义源代码查看编辑器
    1. 将 `view_source.editor.external` 设为 `true`
    2. 新建 `view_source.editor.path` 为你的编辑器路径

### css

+ `#PersonalToolbar`

  这是 Firefox 书签工具栏容器的 ID。您可以使用此 ID 来访问整个书签工具栏。

+ `.urlbar-input-box`

  这是 Firefox 地址栏输入框的 CSS 类名。通过查找具有此类名的元素，您也可以找到地址栏。

﻿﻿# Window10

- CompatTelRunner进程cpu占用过高
  运行`gpedit.msc` -> `计算机设置` -> `管理模板` -> `Windows组件` -> `数据收集和预览版` -> 右侧`允许遥测`设置为 **已禁用**

- 批处理

  ```shell
  "png转gif.bat
  ren *.png *.gif
  "文件名追加1
  @echo off
  setlocal enabledelayedexpansion

  for %%a in (*.*) do (
  set "filename=%%~na"
  set "extension=%%~xa"
  set "newname=!filename!1!extension!"
  ren "%%a" "!newname!"
  )
  ```

- 右键新建菜单管理

  [右键菜单管理](https://github.com/BluePointLilac/ContextMenuManager/releases)

# 虚拟机

## Vmware

+ Vmware虚拟机随系统自启

  https://www.cnblogs.com/xs-xs/p/17069459.html

  在Vmware Workstation目录下载有vmrun.exe程序可以用来启动vmx文件(虚拟机).

  vmrun.exe 参数 `vmrun -T (ws|fusion|player) start "指定虚拟机vmx文件路径" [gui|nogui]`

  - ws 表示 VMware workstation  windows平台使用
  - fusion 表示 VMware fusion Apple平台使用
  - player 表示 VMware player 通用平台
  - gui 表示 使用gui启动虚拟机
  - nogui 表示 不使用gui无界面后台运行

  新建一个脚本文件(.bat)输入以下信息(模板), 注意请根据您当前的文件路径新建脚本.

  ```cmd
  vmrun -T ws start "C:\FileData\Misc\Virtual Machines\ArchLinux\ArchLinux.vmx" nogui
  ```

# Misc

## WinRAR

- 新版图标是换回经典图标
  1. 首先去[WinRAR国际官网](https://www.rarlab.com/themes.htm)找到Themes
  2. 点开后，滚轮翻到最底部。找到 WinRAR Classic theme by Francesco Indrio 点下面的 version with 48x36 toolbar icons
  3. 双击下载好的这个压缩包
  4. 出现页面后点“是”
  5. 然后随机打开一个压缩包 点“选项” 选择“主题” 点击 WinRAR Classic 48x36 即可更换原版主题
