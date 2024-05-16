# 用户管理

- `sudo adduser test`

  创建一个用户名为test的sudo用户。

- `sudo usermod -aG sudo test`

  创建test用户后，可以使用 -aG 组合选项将其添加到 sudo 组，就可以将其转为 sudo 用户。

  使用 -a 选项是为了确保向组中“追加”。

- `sudo -l -U test`

  验证test用户是否被赋予sudo权限，在命令输出中，末尾你会看到是否可以 sudo 权限运行所有命令：(ALL : ALL) ALL

- `sudo deluser --remove-home test`

  删除test用户同时删除test用户的主目录

# apt

## 镜像源

记得备份一下
`sudo cp /etc/apt/source.list /etc/apt/source.list.bak`

- [阿里云镜像开源镜像站（已经更换地址）](https://opsx.alibaba.com/mirror?lang=zh-CN)
- [阿里云镜像开源社区镜像站（新地址）](https://developer.aliyun.com/mirror/)
- [网易开源镜像站](http://mirrors.163.com/.help/ubuntu.html)
- [清华大学开源镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)
- [中科大开源镜像站](https://mirrors.ustc.edu.cn/)

## 常见命令

- 更新软件包列表：
  `sudo apt update`
- 升级已安装的软件包：
  `sudo apt upgrade`
- 安装软件包：
  `sudo apt install <package_name>`
- 删除软件包:
  `sudo apt remove <package_name>`
- 完全删除软件包：
  `sudo apt purge <package_name>`
- 搜索软件包：
  `apt search <keyword>`
- 显示软件包信息：
  `apt show <package_name>`
