[【GeekHour】一小时Git教程](https://www.bilibili.com/video/BV1HM411377j/)

# 安装与初始化

- https://zhuanlan.zhihu.com/p/607970211
- `git -v`

```bash
# 配置用户名("username"是自己的用户名)
git config --global user.name "Hunter Wang"
# 配置邮箱("username@email.com"是注册账号时所用的邮箱) 没有空格可以不加双引号
git config --global user.email "hunter9812@qq.com"
# 保存用户名和密码
git config --global credential.helper store
# 查看git的配置信息
git config --global --list

# 不加--global是打印
省略(Local):本地配置，只对本地仓库有效
--global: 全局配置，所有仓库生效
--system：系统配置，对所有用户生效
```

## 代理

```bash
# 开代理
git config --global http.proxy http://127.0.0.1:26501
git config --global http.sslVerify false
# 关代理
git config --global --unset http.proxy
git config --global http.sslVerify true
```

# 基本使用

## 新建仓库

+ `git init` 将一个目录初始化为 Git 仓库
  + `git init xxx` 在当前目录创建一个文件并初始化为Git仓库
+ `git clone` 复制一个 Git 仓库，以上下其手

## 工作区域和文件状态

- 工作区(Work Directory): `.git`所在的目录

  git add添加到暂存区

- 暂存区(Staging Area/Index): .git/index

  git commit添加到本地仓库

- 本地仓库(Local Repository): .git/objects

- 未跟踪(Untrack)

  新创建未被git管理的文件

- 未修改(Unmodified)

  文件已被git管理起来但文件内容没有发生变化，还没有修改过

- 已修改(Modified)

  修改了，但还没有添加到暂存区里面的文件

- 已暂存(Staged)

  修改了，并添加到暂存区里面的文件

![image-20231030203114762](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/202310302031906.png)



## 添加和提交文件

- `git status`: 查看仓库的状态
- `git add`: 添加到暂存区
- `git commit`:  提交



## 基本快照

+ `git add` 添加文件到缓存

  + `git add .` 添加所有文件、文件夹和子文件夹，包括.gitignore和以点开头的任何其他内容，但会根据.gitignore做过滤

  + `git add *` 将添加除以点开头的文件、文件夹和子文件夹以外的任何文件、文件夹和子文件夹

    + 如果文件在子目录中，git add *仍然会添加以点开头的文件。

  + `-p` `--patch` 将所有更改拆分成小块，并提示用户确认是否要将每个更改添加到暂存区

    ```shell
    y - 暂存此区块
    n - 不暂存此区块
    q - 退出；不暂存包括此块在内的剩余的区块
    a - 暂存此块与此文件后面所有的区块
    d - 不暂存此块与此文件后面所有的 区块
    g - 选择并跳转至一个区块
    / - 搜索与给定正则表达示匹配的区块
    j - 暂不决定，转至下一个未决定的区块
    J - 暂不决定，转至一个区块
    k - 暂不决定，转至上一个未决定的区块
    K - 暂不决定，转至上一个区块
    s - 将当前的区块分割成多个较小的区块
    e - 手动编辑当前的区块
    ? - 输出帮助
    ```

+ `git status`  查看你的文件在工作目录与缓存的状态

  + `-s` 获得简短的结果输出

+ `git diff` 显示已写入缓存与已修改但尚未写入缓存的改动的区别

  + `git diff` #尚未缓存的改动
    + 通常执行完 `git status` 之后接着跑一下 `git diff` 是个好习惯。
  + `--cached` #查看已缓存的改动
  + `git diff HEAD` #查看已缓存的与未缓存的所有改动
