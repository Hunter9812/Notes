啥不会，只能看视频。推荐看英文文档，视频只是辅助。

[【残酷难度】最全Arch Linux安装教程——打造真正属于你的操作系统](https://www.bilibili.com/video/BV11J411a7Tp/)

[【超简单】Windows-Arch Linux双系统双磁盘方案，全程不废话](https://www.bilibili.com/video/BV1XY4y1f77S/)

# 安装

## 简单设置

设置字体
`setfont /usr/share/kbd/consolefonts/LatGrkCyr-12x22.psfu.gz`

设置键盘布局
`loadkeys colemak`

配置vim
`vim keys.conf`

```conf
keycode 1 = Caps_Lock
keycode 58 = Escape
```
`loadkeys keys.conf`
`vim .vimrc`

## 同步时间

`timedatectl set-ntp true`

## 分区

- fdisk

  ````bash
  # 查看硬盘的详细信息
  fdisk -l
  # 对硬盘进行分区
  fdisk /dev/sda
  ```
  n
  回车
  -512M
  ```
  ````

- mkfs

  ```bash
  # 引导分区
  mkfs.fat -F32 /dev/sda1
  # 主分区
  mkfs.ext4 /dev/sda2
  # swap分区（虚拟内存的分区）
  mkswap /dev/sda3
  # 挂载swap
  swapon /dev/sda3
  	# 使用 free 命令复查 Swap 文件挂载情况：
  	free -h # -h 选项会使输出以人类可读的单位显示
  ```

- 挂载

  `mount 主分区位置 /mnt`
  `mkdir /mnt/boot`
  `mount 引导分区位置 /mnt/boot`

## 配置pacman

`vim /etc/pacman.conf`

```
Color
color的下一行可以加上ILoveCandy，进度条会变成吃豆人
gf进入 /etc/pacman.d/mirrorlist
```
`vim /etc/xdg/reflector/reflector.conf`

```conf
--save /etc/pacman.d/mirrorlist
--country China
--latest 10
```

`systemctl start reflector.service`

base有最基础的软件

`pacstrap /mnt base linux linux-firmware`

## 配置系统

- Fstab
  `genfstab -U /mnt >> /mnt/etc/fstab`

- Chroot
  `arch-chroot /mnt`

- 时区

  - 要设置[时区](https://wiki.archlinuxcn.org/wiki/系统时间#时区)：

    `ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`

  - 然后运行 [hwclock(8)](https://man.archlinux.org/man/hwclock.8) 以生成 /etc/adjtime：

    `hwclock --systohc`

- 本地化

  - [区域设置](https://wiki.archlinuxcn.org/wiki/Locale)

    - `vim /mnt/etc/locale.gen` 取消掉 `en_US.UTF-8 UTF-8` 和其他需要的[区域设置](https://wiki.archlinuxcn.org/wiki/Locale)前的注释（#）。

      - `locale-gen`

        生成 locale 信息，进入arch再运行

      - `vim /etc/locale.conf``

        `LANG=en_US.UTF-8`

- Root 密码

  - 设置 Root [密码](https://wiki.archlinuxcn.org/wiki/用户和用户组#用户信息存储)：

    ```bash
    # passwd
    ```

## 安装引导程序

  - `grub-mkconfig -o /boot/grub/grub.cfg`

  - `grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB`

## 常用配置

- 系统更新
  `pacman -Syyu`

- 常用安装
  `pacman -S xxx ` man、base-devel

## 添加用户

`useradd -m -G wheel xxx`
`passwd xxx`

visudo 取消%wheelALL=(ALL)的注释

第一次调用sudo的提示

We trust you have received the usual lecture from the local System Administrator. It usually boils down to these three things:

```
#1) Respect the privacy of others.
#2) Think before you type.
#3) With great power comes great responsibility.
```

# pacman

## 安装升级

- `sudo pacman -Sy`：刷新同步软件包列表
  实际操作上，请使用 `pacman -Syu *软件包名*`, 而**不要**使用 `pacman -Sy *软件包名*`，因为后者可能会导致依赖问题。
  - `sudo pacman -Syy`：强制刷新同步软件包列表
- `sudo pacman -Su`：更新软件
- `sudo pacman -Syu`：同步非本地(local)软件仓库并升级系统的软件包
  - `sudo pacman -Syyu`：强制同步非本地(local)软件仓库并升级系统的软件包

## 查询

*pacman* 使用 `-Q` 参数查询本地软件包数据库， `-S` 查询同步数据库，以及 `-F`查询文件数据库。要了解每个参数的子选项，分别参见 `pacman -Q --help`，`pacman -S --help`和`pacman -F --help`。

- `pacman -Ss string1 string2 ...`：查询位置包含了软件包的名字和描述
  `-s` 内置正则
- `pacman -Sc`：删除目前没有安装的所有缓存的包，和没有被使用的同步数据库
- `pacman -Q | wc -l`：计算已安装的软件包数量
- `pacman -Qe`：获取显式安装的软件包列表
  - `pacman -Qeq`：只显示包名
- `pacman -Qd`：获取设置为依赖的软件包
- `pacman -Qdt`：罗列所有不再作为依赖的软件包(孤立orphans)

## 删除

- `sudo pacman -R package_name`：删除单个软件包，保留其全部已经安装的依赖关系
- `sudo pacman -Rs package_name`：删除指定软件包，及其所有没有被其他已安装软件包使用的依赖关系
- `sudo pacman -Rns package_name`：同时删除全局配置文件
  *pacman* 删除某些程序时会备份重要配置文件，在其后面加上*.pacsave扩展名。-n 选项可以避免备份这些文件
  **注意：** pacman 不会删除软件自己创建的文件（例如主目录中的“点文件”不会被删除。）

## 运用

- `sudo pacman -R $(pacman -Qdtq)`：删除所有不再作为依赖的软件包

# [应用程序列表/工具](https://wiki.archlinuxcn.org/wiki/%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E5%88%97%E8%A1%A8/%E5%B7%A5%E5%85%B7)



- ~~[neofetch](https://archlinux.org/packages/?name=neofetch)：在终端中显示系统Logo和信息，cool😎
  alias s=‘neofetch’，第一次学习.bashrc（记得source ~/.bashrc）~~
- fastfetch：c语言版的neofetch
- [konsole](https://archlinux.org/packages/?name=konsole)：kde的终端
- [xfce4-terminal](https://archlinux.org/packages/?name=xfce4-terminal)：Xfce的终端
- [deepin-terminal](https://archlinux.org/packages/?name=deepin-terminal)：Deepin的自带终端
- [Joshuto](https://github.com/kamiyaa/joshuto)：类ranger的终端文件管理器（Rust编写）。
