# linux

***Linux is free, when your time is free.***

# Linux / Unix入门指南

## 桌面发行版

*linux desktop distro*

* Debian
* ArchLinux
* Ubuntu
* CentOs
* OpenEuler
* Ubuntu Kylin
* IDK
  * Manjaro: 是一个基于ArchLinux的开源发行版本。
  * Slackware Linux
  * Gentoo

## 图形化界面

*GUI Linux desktop*

* KDE
* Xface
* iceWM

**这是课上的笔记，主要是一些基础的命令和操作。**

# 登录登出

1. localhost login：登录账户

    ![IMG_20230303_1508_1](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/IMG_20230303_1508_1.png)

2. 中括号的左边是账户名，@后面是

3. root的输入命令前的符号是#，其它权限登录的符号是$

4. last:查看近期用户的登录情况

    ![IMG_20230303_1508_2](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/IMG_20230303_1508_2.png)

5. exit: 登出

6. logout:与exit类似

# 电源管理

## shutdown：关机

无参数默认1分钟

- 参数：
    - **-c**：取消延时命令
    - **-r**：重启，等同于reboot
    - now：立即执行

![IMG_20230303_1508_3](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/IMG_20230303_1508_3.png)

![IMG_20230303_1508_4](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/IMG_20230303_1508_4.png)

## reboot：立即重启

## poweroff：立即关机

（一般用这个）

# 文件管理

## cd：切换工作目录

![IMG_20230303_1508_6](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/IMG_20230303_1508_6.png)

- 命令格式：cd [directory]
- 参数：
    - /：代表根目录
    - .：当前目录
    - ..：上级目录
    - ~：当前用户的默认工作目录

## mkdir：创建文件夹

- 命令格式：`mkdir [-选项] 目录名`

- 参数：
    - -p 递归创建多个目录

- 注意事项：
    - 目录还是文件的名字，除了以“/”以外的任意名称，“/”根目录，路径分隔符
    - 文件或目录的名字长度不能超过255个字符

- 实例：

    ```shell
    # 在所在目录创建zkdata和zkdatalog文件夹
    mkdir zkdata zkdatalog
    ```



## touch：创建文件

touch 命令用于创建新的空白文件

- 命令格式：touch [-选项] 文件名

```bash
#在当前路径创建空文件
[root@localhost ~]# touch hello
[root@localhost ~]# ls

#在当前路径同时创建多个文件
[root@localhost ~]# touch t1 t2 t3 t4
[root@localhost ~]# ls
#在指定路径同时创建多个文件
[root@localhost ~]# touch /opt/test1 /opt/test2 /opt/test3
[root@localhost ~]# ls /opt
rh  student  test1  test2  test3  xx

#如果存在同名目录时，无法创建
[root@localhost ~]# mkdir test
mkdir: 无法创建目录"test": 文件已存在

#如果存在同名文件时，touch命令没有提示，但原有文件不会被覆盖
[root@localhost ~]# touch t1

#对于目录而言，只有单个目录的时候，“/”可有可无
[root@localhost ~]# ls /opt/
rh  student  test1  test2  test3  xx
[root@localhost ~]# ls /opt
rh  student  test1  test2  test3  xx

#对于目录而言，查看目录下的内容时，必须要有“/”
[root@localhost ~]# ls /opt/xx
oo

#对于文件而言，后边绝对不能有“/”
[root@localhost ~]# ls /opt/test1
/opt/test1
[root@localhost ~]# ls /opt/test1/
ls: 无法访问/opt/test1/: 不是目录
```

## cp：复制文件

cp（英文全拼：copy file）用于复制文件或目录，cp命令在复制时也可修改目录或文件名字

- 命令格式：cp [-选项] 源文件或目录 目标目录
- 参数：
    - -p 保留源文件属性不变（如：修改时间、归属关系、权限）
    - -r 复制目录（包含该目录下所有的子目录和文件）
- 使用 `.` 配合cp命令执行复制（`.`永远表示当前路径）

## mv：剪切

mv（英文全拼：move file）用于移动文件或目录到其他位置，也可用于修改目录或文件名

- 命令格式：mv [-选项] 源文件... 目标路径
- 使用 `.` 配合mv命令使用

## rm：删除

rm（英文全拼：remove）命令用于删除文件或者目录。

- 命令格式：rm [-选项…] 目录或文件…
- 参数：
    - -i 删除前逐一询问确认。
    - -f 即使原档案属性设为唯读，亦直接删除，无需逐一确认。
    -  -r 将目录及以下之档案亦逐一删除。
- ps：
    - `*`特殊字符：系统常用符号，用来代表任意所有字符
    - `rm -rf /*`：萌新必知，不知百度

### rmdir：删除文件夹

## tar：创建存档文件和提取文件

```shell
# 解压文件 jdk-8u221-linux-x64.tar.gz到/usr/java里
tar -zxvf /usr/package277/jdk-8u221-linux-x64.tar.gz -C /usr/java
```

+ 参数：
    + -z或--gzip或--ungzip   通过gzip指令处理备份文件。
    + -x或--extract或--get  从备份文件中还原文件。
    + -v或--verbose   显示指令执行过程。
    + -f<备份文件>或--file=<备份文件>   指定备份文件。
    + -C<目的目录>或--directory=<目的目录>   切换到指定的目录。

# 查看显示

## ls：列出目录的内容

```bash
[rootlocalhost~]# ls
anaconda-ks.cfg
```

- 命令格式：`ls [选项]... [文件]...`

- 参数：

    + **-l**：等同于ll。

        显示不被隐藏的所有文件与文件夹的详细信息，并成列表显示

        ![IMG_20230317_1448_1](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/IMG_20230317_1448_1.png)

        \1. 第一位文件类型

        \- 普通文件 ， d 目录文件，I 链接文件，p 管理文件， b 块设备文件， c 字符设备文件， s 套接字文件

        \2.文件属性

        第一部分表示文件创建者/所有者权限，第二部分表示同组其他用户的权限，第三部分表示其他组用户的权限，权限也可以用数字代替

        ```
        二进制
        444 r--r--r--
        600 rw-------
        644 rw-r--r--
        666 rw-rw-rw-
        700 rwx------
        744 rwxr--r--
        755 rwxr-xr-x
        777 rwxrwxrwx
        chomd 777 就是赋予三类用户读，写，执行权限
        ```

        从左至右，1-3位数字代表文件所有者的权限，4-6位数字代表同组用户的权限，7-9数字代表其他用户的权限。
        而具体的权限是由数字来表示的，读取的权限等于4，用r表示；写入的权限等于2，用w表示；执行的权限等于1，用x表示；

        \3.目录、链接数量

        第三列的数字，代表该文件所具有的**一级子目录的个数，实际子目录数值是该数字-2，因为 . 和 .. 分别代表 本级目录 和 上级目录**

        \4. 创建者与所在组

        第4 5列是创建者和所在组的名称

        \5.文件大小

        文件大小，单位为字节

        \6.创建的时间和日期

    + -al：显示的所有文件与文件夹的详细信息，包括所有被隐藏的文件和文件夹，并成列表显示。

### chmod：控制用户对文件的权限

Linux/Unix 的文件调用权限分为三级 : 文件所有者（Owner）、用户组（Group）、其它用户（Other Users）。

只有文件所有者和超级用户可以修改文件或目录的权限。可以使用绝对模式（八进制数字模式），符号模式指定文件的权限。

+ 命令格式：

    ```bash
    chmod [-cfvR] [--help] [--version] mode file...
    ```

+ 参数：

    + mode : 权限设定字串，格式如下 :

        ```bash
        [ugoa...][[+-=][rwxX]...][,...]
        ```

        其中：

        - u 表示该文件的拥有者，g 表示与该文件的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。
        - \+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限。
        - r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。

    + -c : 若该文件权限确实已经更改，才显示其更改动作

    + -f : 若该文件权限无法被更改也不要显示错误讯息

    + -v : 显示权限变更的详细资料

    + -R : 对目前目录下的所有文件与子目录进行相同的权限变更(即以递归的方式逐个变更)

    + --help : 显示辅助说明

    + --version : 显示版本

#### 符号模式

使用符号模式可以设置多个项目：who（用户类型），operator（操作符）和  permission（权限），每个项目的设置可以用逗号隔开。 命令 chmod 将修改 who  指定的用户类型对文件的访问权限，用户类型由一个或者多个字母在 who 的位置来说明，如 who 的符号模式表所示:

| who  | 用户类型 | 说明                   |
| ---- | -------- | ---------------------- |
| `u`  | user     | 文件所有者             |
| `g`  | group    | 文件所有者所在组       |
| `o`  | others   | 所有其他用户           |
| `a`  | all      | 所有用户, 相当于 *ugo* |

operator 的符号模式表:

| Operator | 说明                                                   |
| -------- | ------------------------------------------------------ |
| `+`      | 为指定的用户类型增加权限                               |
| `-`      | 去除指定用户类型的权限                                 |
| `=`      | 设置指定用户权限的设置，即将用户类型的所有权限重新设置 |

permission 的符号模式表:

| 模式 | 名字         | 说明                                                         |
| ---- | ------------ | ------------------------------------------------------------ |
| `r`  | 读           | 设置为可读权限                                               |
| `w`  | 写           | 设置为可写权限                                               |
| `x`  | 执行权限     | 设置为可执行权限                                             |
| `X`  | 特殊执行权限 | 只有当文件为目录文件，或者其他类型的用户有可执行权限时，才将文件权限设置可执行 |
| `s`  | setuid/gid   | 当文件被执行时，根据who参数指定的用户类型设置文件的setuid或者setgid权限 |
| `t`  | 粘贴位       | 设置粘贴位，只有超级用户可以设置该位，只有文件所有者u可以使用该位 |

#### 八进制语法

chmod命令可以使用八进制数来指定权限。文件或目录的权限位是由9个权限位来控制，每三位为一组，它们分别是文件所有者（User）的读、写、执行，用户组（Group）的读、写、执行以及其它用户（Other）的读、写、执行。历史上，文件权限被放在一个比特掩码中，掩码中指定的比特位设为1，用来说明一个类具有相应的优先级。

| #    | 权限           | rwx  | 二进制 |
| ---- | -------------- | ---- | ------ |
| 7    | 读 + 写 + 执行 | rwx  | 111    |
| 6    | 读 + 写        | rw-  | 110    |
| 5    | 读 + 执行      | r-x  | 101    |
| 4    | 只读           | r--  | 100    |
| 3    | 写 + 执行      | -wx  | 011    |
| 2    | 只写           | -w-  | 010    |
| 1    | 只执行         | --x  | 001    |
| 0    | 无             | ---  | 000    |

## cat：查看文件内容

- 命令格式：`cat [-AbeEnstTuv] [--help] [--version] fileName`
- 参数：
    + -b：显示的文件时，非空输出行显示行号；
    + -a：列出所有隐藏符号；
    + -e：列出每行结尾的回车符 ；
    + -n：显示全部行号（空行前面也会显示行号）；
    + -t：把 Tab 键 ^I 显示出来；
    + -v：列出特殊字符；
    + -n或-number：有1开始对所有输出的行数编号；
- 其它：
    + `cat > 文件名 << 结束符`：创建文件
    + `cat 文件名 | grep 查找内容`：查找文件中的内容
    + `cat >文件名 <<结束符 或者 cat >>文件名 <<结束符`：写入内容
    + `cat 源文件名 > 要写入的文件名`：把一个文件的内容写入到另一个文件，不保存先前的内容
        `cat 源文件名 >> 要写入的文件名`：把一个文件的内容追加到另一个文件
    + `cat 源文件1名 源文件2名 >> 要写入的文件名`：把两个文件的内容合并到另一个文件

## head：查看文件的开头部分

- 命令格式**：**

    ```bash
    head [参数] [文件]
    ```

- 参数：

    + -q 隐藏文件名
    + -v 显示文件名
    + **-c<数目>** 显示的字节数。
    + **-n<行数>** 显示的行数。

## tail：查看文件的末尾部分

- 命令格式：

    ```bash
    tail [参数] [文件]
    ```

- 参数：

    - -f 循环读取
    - -q 不显示处理信息
    - -v 显示详细的处理信息
    - -c<数目> 显示的字节数
    - -n<行数> 显示文件的尾部 n 行内容
    - --pid=PID 与-f合用,表示在进程ID,PID死掉之后结束
    - -q, --quiet, --silent 从不输出给出文件名的首部
    - -s, --sleep-interval=S 与-f合用,表示在每次反复的间隔休眠S秒


## more：按页来查看文件的内容

- 命令格式：

    ```bash
    more [-dlfpcsu ] [-num ] [+/ pattern] [+ linenum] [file ... ]
    ```

- 参数：

    + +n   从笫n行开始显示
    + -n    定义屏幕大小为n行
    + +/pattern 在每个档案显示前搜寻该字串（pattern），然后从该字串前两行之后开始显示
    + -c    从顶部清屏，然后显示
    + -d    提示“Press space to continue，’q’ to quit（按空格键继续，按q键退出）”，禁用响铃功能
    + -l    忽略Ctrl+l（换页）字符
    + -p    通过清除窗口而不是滚屏来对文件进行换页，与-c选项相似
    + -s    把连续的多个空行显示为一行
    + -u    把文件内容中的下画线去掉

- 常用操作命令：

    - Enter  向下n行，需要定义。默认为1行
    - Ctrl+F  向下滚动一屏
    - 空格键 向下滚动一屏
    - Ctrl+B 返回上一屏
    - =    输出当前行的行号
    - ：f   输出文件名和当前行的行号
    - V   调用vi编辑器
    - !命令  调用Shell，并执行命令
    - q    退出more

## less：分页显示的工具

- 命令格式：

    ```bash
    less [参数]  文件
    ```

- 参数：

    + -b <缓冲区大小> 设置缓冲区的大小
    + -e 当文件显示结束后，自动离开
    + -f 强迫打开特殊文件，例如外围设备代号、目录和二进制文件
    + -g 只标志最后搜索的关键词
    + -i 忽略搜索时的大小写
    + -m 显示类似more命令的百分比
    + -N 显示每行的行号
    + -o <文件名> 将less 输出的内容在指定文件中保存起来
    + -Q 不使用警告音
    + -s 显示连续空行为一行
    + -S 行过长时间将超出部分舍弃
    + -x <数字> 将“tab”键显示为规定的数字空格
    + **/字符串**：向下搜索“字符串”的功能
    + **?字符串**：向上搜索“字符串”的功能
    + n：重复前一个搜索（与 / 或 ? 有关）
    + N：反向重复前一个搜索（与 / 或 ? 有关）
    + **b** 向后翻一页
    + d 向后翻半页
    + h 显示帮助界面
    + **Q** 退出less 命令
    + u 向前滚动半页
    + y 向前滚动一行
    + **空格键** 滚动一行
    + **回车键** 滚动一页
    + [pagedown]： 向下翻动一页
    + [pageup]：  向上翻动一页

## clear：清屏

`CTRL + L`：也是同样的效果

## grep：搜索

用于查找文件里符合条件的字符串或正则表达式。

+ 命令格式：

  ```bash
  grep [options] pattern [files]
  ```

+ 参数：

  + `-i`：忽略大小写进行匹配。
  + `-v`：反向查找，只打印不匹配的行。
  + `-n`：显示匹配行的行号。
  + `-r`：递归查找子目录中的文件。
  + `-l`：只打印匹配的文件名。
  + `-c`：只打印匹配的行数。

# 文件查找

## find：查找文件

find 命令用于在指定目录下查找文件和目录。

它可以使用不同的选项来过滤和限制查找的结果。

- 命令格式：

    ```bash
    find [path] [expression]
    ```

- 参数：

    **path** 是要查找的目录路径，可以是一个目录或文件名，也可以是多个路径，多个路径之间用空格分隔，如果未指定路径，则默认为当前目录。

    **expression** 是可选参数，用于指定查找的条件，可以是文件名、文件类型、文件大小等等。

    expression 中可使用的选项有二三十个之多，以下列出最常用的部份：

    - `-name pattern`：按文件名查找，支持使用通配符 `*` 和 `?`。
    - `-type type`：按文件类型查找，可以是 `f`（普通文件）、`d`（目录）、`l`（符号链接）等。
    - `-size [+-]size[cwbkMG]`：按文件大小查找，支持使用 `+` 或 `-` 表示大于或小于指定大小，单位可以是 `c`（字节）、`w`（字数）、`b`（块数）、`k`（KB）、`M`（MB）或 `G`（GB）。
    - `-mtime days`：按修改时间查找，支持使用 `+` 或 `-` 表示在指定天数前或后，days 是一个整数表示天数。
    - `-user username`：按文件所有者查找。
    - `-group groupname`：按文件所属组查找。



## which：查看可执行文件的位置

which指令会在PATH变量指定的路径中，搜索某个系统命令的位置，并且返回第一个搜索结果

- 命令格式：

    ```bash
    which 可执行文件名称
    ```

- 参数：

    + -n 　指定文件名长度，指定的长度必须大于或等于所有文件中最长的文件名。
    + -p 　与-n参数相同，但此处的包括了文件的路径。
    + -w 　指定输出时栏位的宽度。
    + -V 　显示版本信息

# 用户管理

## id：查看用户信息

id命令用于显示用户的ID，以及所属群组的ID。
id 会显示用户以及所属群组的实际与有效 ID，若两个 ID 相同，则仅显示实际 ID，若仅指定用户名称，则显示目前用户的 ID。该命令会显示用户的 UID（User ID）、GID（Group ID）以及附属于用户的所有组 ID。

+ 命令格式：

    ```bash
    id [-gGnru][--help][--version][用户名称]
    ```

+ 参数：

    + -g 或 --group 　显示用户所属群组的ID。
    + -G 或 --groups 　显示用户所属附加群组的ID。
    + -n 或 --name 　显示用户，所属群组或附加群组的名称。
    + -r 或 --real 　显示实际ID。
    + **-u 或 --user 　显示用户ID。**
    + -help 　显示帮助。
    + -version 　显示版本信息。

## useradd：添加新用户

useradd 命令用于建立用户帐号。

useradd 可用来建立用户帐号。帐号建好之后，再用 passwd 设定帐号的密码。而可用 userdel 删除帐号。使用 useradd 指令所建立的帐号，实际上是保存在 /etc/passwd 文本文件中。

- 命令格式：

    ```bash
    useradd [-mMnr][-c <备注>][-d <登入目录>][-e <有效期限>][-f <缓冲天数>][-g <群组>][-G <群组>][-s <shell>][-u <uid>][用户帐号]

    or

    useradd -D [-b][-e <有效期限>][-f <缓冲天数>][-g <群组>][-G <群组>][-s <shell>]
    ```

- 参数：

    + -c comment 指定一段注释性描述。
    + -d 目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。
    + -g 用户组 指定用户所属的用户组。
    + -G 用户组，用户组 指定用户所属的附加组。
    + -s Shell文件 指定用户的登录Shell。
    + -u 用户号 指定用户的用户号，如果同时有-o选项，则可以重复使用其他用户的标识号。

## passwd：更改密码

密码相关信息保存在 /etc/shadow 文件中

- 命令格式：

    ```bash
    passwd [-k] [-l] [-u [-f]] [-d] [-S] [username]
    ```

- 参数：

    + -d 删除密码
    + -f 强迫用户下次登录时必须修改口令
    + -w 口令要到期提前警告的天数
    + -k 更新只能发送在过期之后
    + -l 停止账号使用
    + -S 显示密码信息
    + -u 启用已被停止的账户
    + -x 指定口令最长存活期
    + -g 修改群组密码
    + 指定口令最短存活期
    + -i 口令过期后多少天停用账户

## usermod：修改用户

- 命令格式：

    ```bash
    usermod [-LU][-c <备注>][-d <登入目录>][-e <有效期限>][-f <缓冲天数>][-g <群组>][-G <群组>][-l <帐号名称>][-s <shell>][-u <uid>][用户帐号]
    ```

- 参数：

    + -c<备注> 　修改用户帐号的备注文字。
    + -d<登入目录> 　修改用户登入时的目录。
    + -e<有效期限> 　修改帐号的有效期限。
    + -f<缓冲天数> 　修改在密码过期后多少天即关闭该帐号。
    + -g<群组> 　修改用户所属的群组。
    + -G<群组> 　修改用户所属的附加群组。
    + **-l<帐号名称> 　修改用户帐号名称。**
    + -L 　锁定用户密码，使密码无效。
    + -s<shell> 　修改用户登入后所使用的shell。
    + **-u<uid> 　修改用户ID。**
    + -U 　解除密码锁定。

## userdel：删除用户

userdel命令用于删除用户帐号。

userdel可删除用户帐号与相关的文件。若不加参数，则仅删除用户帐号，而不删除相关文件。

- 命令格式：

    ```bash
    userdel [-r][用户帐号]
    ```

- 参数：

    + -r 　删除用户登入目录以及目录中所有文件。

# 用户组管理

## groupadd：添加用户组

groupadd 命令用于创建一个新的工作组，新工作组的信息将被添加到系统文件中。

相关文件:

+ /etc/group 组账户信息。
+ /etc/gshadow 安全组账户信息。
+ /etc/login.defs Shadow密码套件配置。

- 命令格式：

    ```bash
    groupadd [-g gid [-o]] [-r] [-f] group
    ```

- 参数：

    + -g：指定新建工作组的 **id**；
    + -r：创建系统工作组，系统工作组的组 ID 小于 500；
    + -K：覆盖配置文件 **/etc/login.defs**；
    + -o：允许添加组 ID 号不唯一的工作组。
    + -f,--force: 如果指定的组已经存在，此选项将失明了仅以成功状态退出。当与 -g 一起使用，并且指定的 GID_MIN 已经存在时，选择另一个唯一的 GID（即 -g 关闭）。

## 	groupmod：更改用户组

- 命令格式：

    ```bash
    groupmod [-g <群组识别码> <-o>][-n <新群组名称>][群组名称]
    ```

- 参数：

    + **-g <群组识别码> 　设置欲使用的群组识别码。**
    + -o 　重复使用群组识别码。
    + **-n <新群组名称> 　设置欲使用的群组名称。**

## gpasswd：组管理

gpasswd 是 Linux 下工作组文件 /etc/group 和 /etc/gshadow 管理工具，用于将一个用户添加到组或者从组中删除。

- 命令格式：

    ```bash
    gpasswd [可选项] 组名
    ```

- 参数：

    + **-a：添加用户到组；**
    + **-d：从组删除用户；**
    + -A：指定管理员；
    + -M：指定组成员和-A的用途差不多；
    + -r：删除密码；
    + -R：限制用户登入组，只有组中的成员才可以用newgrp加入该组。

**注意**：添加用户到某一个组 可以使用 `usermod -G group_name user_name` 这个命令可以添加一个用户到指定的组，但是以前添加的组就会清空掉。

## groupdel：删除群组

groupdel命令用于删除群组。

需要从系统上删除群组时，可用groupdel(group delete)指令来完成这项工作。倘若该群组中仍包括某些用户，则必须先删除这些用户后，方能删除群组。

- 命令格式：

    ```bash
    groupdel [群组名称]
    ```

注意：group下没有用户才能删除。

# 包管理器

## rpm

RPM:red-hat package manager(红帽包管理器)管理应用程序的安装、卸载和维护

rpm软件包命名格式：软件名称-版本号-发行版本号-处理器架构.rpm

​         版本号：x.y.x     x:主版本号   y:次版本号 z:修正版本号

使用RPM命令管理软件（安装、刷新、查询、升级、卸载）

​     RPM命令-安装Install

​     rpm –i example.rpm    安装一个包

​     rpm –iv example.rpm   安装一个包，安装过程显示安装的文件信息

​     rpm –ivh example.rpm  安装一个包，显示安装的文件信息和进度

​     2 RPM命令-卸载

​     rpm –e example.rpm

​     rpm –e –nodeps example.rpm    卸载不考虑依赖关系，强制卸载（不建议）

​     rpm –e –allmatches example.rpm 若存在多个版本，使用allmatches参数批量卸载

​     3 RPM命令-升级      v显示文件信息， h进度条

​     rpm –U example.rpm        存在旧包时，欲删除旧包安装新包时使用

​     rpm –Uvh example.rpm

​     rpm –F example.rpm        存在旧包时，在旧包的基础上升级

​     rpm –Fvh example.rpm

​     4 RPM命令-查询

​     rpm –q example.rpm        查询特定的example.rpm软件包是否安装

​     rpm –qa                   查询所有已经安装的软件包

​     rpm –qf                    查询所有已经安装过的软件包

​     rpm –qp                   查询未安装的软件包

rpm –ql                    查询已安装的软件包中的文件列表和完成目录

## yum


## dnf

DNF是一种基于RPM包管理器的软件包管理器，用于在Fedora、CentOS和Red Hat Enterprise Linux等Linux发行版上安装、更新和删除软件包。以下是一些常见的DNF命令及其参数：

- **dnf install [package_name]**：安装指定的软件包。
- **dnf update**：更新系统上所有已安装软件包的版本。
- **dnf upgrade**：升级系统上所有已安装软件包的版本，并删除不再需要的软件包。
- **dnf remove [package_name]**：删除指定的软件包。
- **dnf search [keywords]**：搜索与关键字匹配的软件包。
- **dnf info [package_name]**：显示有关指定软件包的详细信息，如版本、大小、依赖项等。
- **dnf list installed**：列出系统上已安装的所有软件包。

## apt

## pacman

## pkg



# 进程管理

## ps

显示当前正在运行的进程信息。它提供了一种查看系统中活动进程的简单方法，包括进程ID（PID）、父进程ID（PPID）、CPU使用率、内存使用量等。

- 语法

  `ps [options] [--help]`

- 常用命令

  - `ps -ef`：显示所有正在运行的进程，包括系统进程和用户进程。每个进程都会有一个唯一的PID来标识自己。
  - `ps -ef | grep process_name`：查找特定进程。
  - `kill PID`：结束指定进程
  - `ps aux`：查看系统中所有的进程，使用 BS 操作系统格式
  - `ps -le`：查看系统中所有的进程，使用 Linux 标准命令格式

- 参数

  - a:显示所有与终端相关的进程
  - u:显示进程的用户及内存等信息
  - x:显示没有控制终端的进程
  - -l：长格式显示更加详细的信息；比如优先级、父进程的PPID等
  - -e：显示所有进程；



# 任务计划

## at：在指定时间执行命令

+ 语法：

    ```linux
    at [-V] [-q queue] [-f file] [-mldbv] timespec
    at [选项] [日期时间]
    ```

+ 参数：

    - `-V`: Displays the version of the `at` command. (显示`at`命令的版本。)
    - `-q`: Specifies the job queue to use. The default is "a". (指定要使用的作业队列。默认值为“a”。)
    - `-f`: Specifies the file that contains the commands to be executed. (指定包含要执行的命令的文件。)
    - `-m`: Sends an email to the user when the job has completed. (在作业完成时向用户发送电子邮件。)
    - `-l`: Displays a list of pending jobs. (显示挂起作业的列表。)
    - `-d`: Deletes a pending job. (删除挂起的作业。)
    - `-b`: Executes the job immediately if possible, otherwise schedules it for later. (如果可能，立即执行作业，否则将其安排在以后执行。)
    - `-v`: Displays verbose output. (显示详细输出。)

+ 用法：

    ```bash
    # 在大多数 Linux 系统上，你可以使用 systemctl 命令启用 atd 服务并将它们设置为从现在开始自动启动：
    sudo systemctl enable --now atd
    # 启动at服务
    systemctl start atd
    # 退出at交互界面
    ctrl + D
    ```

## corntab：

## atq：查看计划任务

会显示TaskID Time user

# 网络

- nslookup

  - 语法

    ```bash
    nslookup –option1 –option2 host-to-find dns-server
    ```

  - e.g.

    ```bash
    nslookup baidu.com
    ```

# 资讯

- 重读 The C Programming Language https://zhuanlan.zhihu.com/p/379408556
- Kernighan《UNIX 传奇：历史与回忆》杂感 https://www.cnblogs.com/Solstice/p/unix_bwk.html
- Unix版权史 https://www.ruanyifeng.com/blog/2010/03/unix_copyright_history.html
- Unix 操作系统演进简史 https://www.sohu.com/a/332185684_632967
- The Unix Tree https://www.tuhs.org/cgi-bin/utree.pl
- Dennis Unix v6 https://minnie.tuhs.org/Archive/Distributions/Research/Dennis_v6/
- Computer Simulation and History http://simh.trailing-edge.com/
- The Evolution of the Unix Time-sharing System https://www.bell-labs.com/usr/dmr/www/hist.html
- MIT 6.828: Operating System Engineering https://pdos.csail.mit.edu/6.828/2018/schedule.html
- COS 333: Advanced Programming Techniques https://www.cs.princeton.edu/courses/archive/spring19/cos333/
- CS 144: Introduction to Computer Networking https://cs144.github.io/
- Life With Unix: A Guide for Everyone https://www.tuhs.org/Archive/Documentation/Books/Life_with_Unix_v2.pdf

