# 常用命令

## config

- aria2

  - scoop config aria2-enabled false

  - scoop config aria2-warning-enabled false

  - ```
    与 Aria2 有关的设置选项：

        aria2-enabled: 开启 Aria2 下载，默认
        truearia2-retry-wait: 重试等待秒数，默认
        2aria2-split: 单任务最大连接数，默认5
        aria2-max-connection-per-server: 单服务器最大连接数，默认5 ，最大
        16aria2-min-split-size: 最小文件分片大小，默认5M

    优化Aria2 设置，单任务最大连接数设置为 32，单服务器最大连接数设置为 16，最小文件分片大小设置为 1M

    # aria2 在 Scoop 中默认开启
    scoop config aria2-enabled true
    # 关于以下参数的作用，详见aria2的相关资料
    scoop config aria2-retry-wait 4
    scoop config aria2-split 16
    scoop config aria2-max-connection-per-server 16
    scoop config aria2-min-split-size 4M
    ```

- proxy

  - 设置代理：

    scoop config proxy 127.0.0.1:9812

  - 恢复使用系统代理

    scoop config rm proxy

- scoop_repo

    - 指定scoop更新库的地址
        scoop config scoop_repo https://github.com/ScoopInstaller/Scoop


# bucket

## 添加bucket

- 先删除

  ```bash
  scoop bucket rm main && scoop bucket rm extras && scoop bucket rm versions && scoop bucket rm java && scoop bucket rm nirsoft && scoop bucket rm nerd-fonts
  ```

- 官方源

  ```bash
  scoop bucket add main
  scoop bucket add extras
  scoop bucket add versions
  scoop bucket add java
  scoop bucket add nirsoft
  scoop bucket add nerd-fonts
  ```


## 官方维护的 bucket

- [main](https://github.com/ScoopInstaller/Main) - Default bucket for the most common (mostly CLI) apps

- [extras](https://github.com/ScoopInstaller/Extras) - Apps that don't fit the main bucket's [criteria](https://github.com/ScoopInstaller/Scoop/wiki/Criteria-for-including-apps-in-the-main-bucket)

- [games](https://github.com/Calinou/scoop-games) - Open source/freeware games and game-related tools

- [nerd-fonts](https://github.com/matthewjberger/scoop-nerd-fonts) - Nerd Fonts

- [nirsoft](https://github.com/kodybrown/scoop-nirsoft) - Almost all of the [250+](https://rasa.github.io/scoop-directory/by-apps#kodybrown_scoop-nirsoft) apps from [Nirsoft](https://nirsoft.net/)

- [java](https://github.com/ScoopInstaller/Java) - A collection of Java development kits (JDKs), Java runtime engines  (JREs), Java's virtual machine debugging tools and Java based runtime  engines.

- [nonportable](https://github.com/TheRandomLabs/scoop-nonportable) - Non-portable apps (may require UAC)

- [php](https://github.com/ScoopInstaller/PHP) - Installers for most versions of PHP

- [versions](https://github.com/ScoopInstaller/Versions) - Alternative versions of apps found in other buckets
