[快速入门 : PowerShell 3.0 【720P】【MVA】【中文字幕】](https://www.bilibili.com/video/BV1sx411p7xt)

# PowerShell

常用功能：选中代码，右键一下复制，再次右键粘贴
命名规则：动词-名词

## 基本命令

1. 跳转 cd -> set-location

2. 获取目录列表 dir,ls -> get-childitem

3. 清屏 cls,clear -> clear-host

4. 创建目录 md -> mkdir

5. 查询别名 gal -> get-alias

6. 获取帮助 man -> help

7. type,cat -> get-content

8. copy,cp -> copy-item

9. update-help -erroraction silentlycontinue

10.  ps -> Get-Process

    这是一行系统监控信息，表示了当前运行中的进程的一些状态信息，具体含义如下：

    - NPM(K): 正在运行的进程数
    - PM(M): 进程使用的物理内存大小（单位为MB）
    - WS(M): 进程使用的工作集（工作集是进程占用的物理内存的子集，包括主动使用和缓存的数据，单位为MB）
    - CPU(s): 进程占用的CPU时间（单位为秒）
    - Id: 进程ID
    - SI: 进程启动时的会话ID
    - ProcessName：进程名称。

## window原生命令

- ping一台计算机 `ping 主机名`
- 返回路径的根目录 `cd\`
- 运行应用
  - notepad 记事本
  - calc 计算器
  - mspaint 绘画
  - mmc 控制台
- ipconfig /all

## 命令
- help get-service -full
- Get-Service | Export-Csv -Path c:\service.csv
- Get-Service | Stop-Service -whatif 查看powershell会做什么
- Get-Service -DisplayName `*bi*` | Stop-Service -Confirm 询问你是否要执行该操作
- -PassThru 显示运行结果
- Get-Module -ListAvailable 显示现在可用的Module列表

## nuke
- 停止所有服务 Get-Service | Stop-Service

# cmd

- 创建软链接

  在PowerShell中，要创建一个指向文件夹的软连接，你可以使用以下命令：

  ```
  powershell
  New-Item -ItemType SymbolicLink -Path <link_name> -Target <target_folder> -Force
  ```

  其中，`<link_name>`是软连接的名称，`<target_folder>`是软连接指向的目标文件夹的完整路径。

  例如，要在当前目录下创建一个名为`myfolderlink`的软连接，指向`C:\Path\to\TargetFolder`文件夹，可以使用以下命令：

  ```
  powershell
  New-Item -ItemType SymbolicLink -Path .\myfolderlink -Target "C:\Path\to\TargetFolder" -Force
  ```

  这里的`-Force`参数用于强制创建软连接，即使已经存在同名的文件或文件夹。

  运行上述命令后，软链接就会被创建到指定的目标文件夹。

  你可以使用以下命令验证软链接是否创建成功：

  ```
  powershell
  Get-Item .\myfolderlink
  ```

  输出应该类似于：

  ```
  Mode                LastWriteTime         Length Name
  ----                -------------         ------ ----
  d-----        2023/11/04     11:22                myfolderlink
  ```

  其中，“d”表示它是一个软链接（SymbolicLink），而不是一个普通的文件或目录。

  请注意，创建符号链接和硬链接需要管理员权限。
