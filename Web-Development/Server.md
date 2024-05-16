# Java

- [sdkman](https://sdkman.io/install)：SDK管理利器

    - `curl -s "https://get.sdkman.io" | bash`

    - `sdk version`

- 后台运行并设置最大最小内存
    ```
    nohup java -Xms128m -Xmx256m -jar equip.jar >> eq.log &
    ```

- `ps -ef | grep java`

# MySQL

##  [Debian 11 上安装 MySQL](https://acytoo.com/ladder/install-mysql-on-debian11/)

安装 Mysql 时，需要判断你的发行版，因此需要 lsb-release

```shell
sudo apt install lsb-release
```

安装 Mysql 的源。可以从这个网页获取最新版本的链接：

https://dev.mysql.com/downloads/repo/apt/

```shell
wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.22-1_all.deb
rm mysql-apt-config_0.8.22-1_all.deb
```

安装

```shell
sudo apt update
sudo apt-get install mysql-server
```

然后就可以使用了

```shell
mysql --version # 检查版本
mysql --help #查看帮助
```

## [mysql开启远程访问权限](https://blog.csdn.net/mazaiting/article/details/106661158)

- 登录到mysql：

  `mysql -u<username> -p<password>`

- 查看user表

  `select host, user from user;`

- 改表法

  `mysql> update user set host = '%' where user = 'root';`

  `FLUSH PRIVILEGES;`

- 授权法

  `GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;`

  `FLUSH PRIVILEGES;`


# Nginx

[【GeekHour】30分钟Nginx入门教程](https://www.bilibili.com/video/BV1mz4y1n7PQ)

## 安装

- 包管理器
- 编译安装
- docker

## 服务启停

- `nginx`：启动nginx

  - `sudo vim /etc/nginx/nginx.conf`

    Nginx 在构建 types_hash 时遇到了问题。要解决此问题，可以根据错误消息中提供的建议增加 types_hash_max_size 或 types_hash_bucket_size 的值。

    在 Nginx 配置文件 /etc/nginx/nginx.conf 中找到 http 块，然后添加或修改以下行：

    ```conf
    nginx

    http {
        types_hash_max_size 2048;      # 增加 types_hash_max_size 的值
        types_hash_bucket_size 128;    # 增加 types_hash_bucket_size 的值

        # ... 其他配置 ...

    	server {
        	# ... 服务器配置 ...
        }
    }
    ```

    将 types_hash_max_size 和 types_hash_bucket_size 的值分别增加为较大的数字，如示例中的 2048 和 128。保存配置文件后，尝试重新启动 Nginx。

  - 如显示80端口被占用：

    `sudo fuser -k 80/tcp`

    `ps -ef|grep nginx`

    `sudo lsof -i:80`

  - `nginx -s $signal`

    - quit：优雅停止
    - stop：立即停止
    - reload：重载配置文件
    - reopen：重新打开日志文件

# Docker

[Docker 容器技术 笔记](https://www.itbaima.cn/document/zj9uvg0sp3b0sok8)

***A container only does one thing.***

## 安装入门

- [官网文档](https://docs.docker.com/engine/install/)

- 包管理器

- 检测是否安装成功

  `docker version`

  ```
  freeman@hunter> docker version
  Client:
   Version:           24.0.5
   API version:       1.43
   Go version:        go1.20.6
   Git commit:        ced0996600
   Built:             Wed Jul 26 21:44:58 2023
   OS/Arch:           linux/amd64
   Context:           default
  Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
  ```

- 初次尝试

  - `sudo docker run hello-world`

  - `sudo docker run -d -p 80:80 nginx`

    访问nginx默认端口：[wsl2](http://localhost:80/)

## 简单使用

- 使用基础镜像

  ```bash
  % sudo docker run -it centos
  [root@9409f3a87e04 /]# uname -r
  5.15.133.1-microsoft-standard-WSL2
  [root@9409f3a87e04 /]# exit
  exit
  % docker ps -a
  CONTAINER ID   IMAGE     COMMAND       CREATED              STATUS                      PORTS     NAMES
  9409f3a87e04   centos    "/bin/bash"   About a minute ago   Exited (0) 21 seconds ago             festive_lamport
  % docker start -i festive_lamport
  ```

- 手动构建镜像

  ```bash
  C:\Users\Hunter
  % docker run -it ubuntu

  apt update
  apt install vim
  exit

  C:\Users\Hunter
  %  docker commit jolly_yonath ubuntu-vim
  ```

  这种方式虽然自定义度很高，但是Docker官方并不推荐

  我们作为普通用户实际上采用Dockerfile的方式会更好一些。

- 编写Dockerfile

  - Dockerfile

      ```dockerfile
      FROM node:14-alpine
      COPY index.js /index.js
      CMD [ "node", "/index.js" ]
      ```

  - index.js

      ```js
      console.log("hello world！")
      ```

  - 运行

      ```bash
      % docker build -t hello-docker-node .
      % docker images
      % docker run -i hello-docker-node
      hello world！
      ```

- 发布镜像到远程仓库

    ```bash
    % docker tag hello-docker-node:latest hunter9812/hello-docker-node:1.0
    % docker images
    % docker login -u hunter9812
    Password:
    Login Succeeded
    % docker push hunter9812/hello-docker-node:1.0
    % docker search hunter9812/
    NAME                           DESCRIPTION            STARS     OFFICIAL   AUTOMATED
    hunter9812/hello-docker-node   nodejs打印helloworld   0
    % docker rmi hunter9812/hello-docker-node:1.0
    % docker pull hunter9812/hello-docker-node:1.0
    % docker run -i hunter9812/hello-docker-node:1.0
    hello world！
    ```

## 容器网络管理

- 容器网络类型

  - **none网络：**这个网络除了有一个本地环回网络之外，就没有其他的网络了，我们可以在创建容器时指定这个网络。

    只有一个本地环回lo网络设备

    ![image-20231221174112683](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/202312211741799.png)

  - **bridge网络：**容器默认使用的网络类型，这是桥接网络，也是应用最广泛的网络类型：

    ![image-20231221174025200](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/202312211740382.png)

  - **host网络**：当容器连接到此网络后，会共享宿主主机的网络，网络配置也是完全一样的

- 用户自定义网络

  Docker默认提供三种网络驱动：bridge、overlay、macvlan，不同的驱动对应着不同的网络设备驱动，实现的功能也不一样，比如bridge类型的，其实就和我们前面介绍的桥接网络是一样的。

## 容器管理存储

### 容器持久化存储

```bash
C:\FileData\Code\Tyro\HTML\Vue\moz-todo-vue (master)
% docker run -it -v C:\FileData\Code\Tyro\HTML\Vue\moz-todo-vue\dist:/usr/share/nginx/html/ -p 80:80 -d nginx
```

访问http://localhost，可以ctrl + F5刷新缓存

## 命令

CONTAINER 可以是容器名字或ID（id可以不用输全，只要与其他不重）

- `docker pull [OPTIONS] NAME[:TAG|@DIGEST]`
  拉取镜像

  - tag:版本

- ` docker images [OPTIONS] [REPOSITORY[:TAG]]`

  列出镜像
  List images

  - -a, --all

    Show all images (default hides intermediate images)
    展示所有的镜像（默认隐藏中间镜像）

- `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

  - --name string

    Assign a name to the container
    给容器分配一个名字

  - --rm

    Automatically remove the container
    自动移除容器

  -  -i, --interactive

    Keep STDIN open even if not attached
    保持标准的输入接口，即使没有连接

    一般it参数是一起使用的，否则base容器启动后就会自动停止了。

  - -t, --tty

    Allocate a pseudo-TTY
    分配一个伪tty设备

  - --network network

    ```bash
    % docker network ls
    NETWORK ID     NAME      DRIVER    SCOPE
    a2bb7bee18c3   bridge    bridge    local
    d8138c516120   host      host      local
    9415712ca245   none      null      local
    ```

    Connect a container to a network
    通过某个网络类型连接一个容器

  - -v, --volume list

    Bind mount a volume
    挂载一个卷

    例子：`docker run -it -v C:\Users\Hunter\tmp:/root/test ubuntu-vim`

  - --volumes-from list

    Mount volumes from the specified
    从指定的卷挂载卷

- `docker create`

  Create a new container
  创建一个新容器

- `docker ps [OPTIONS]`

  列出容器
  List containers

  如果遇到镜像ID为missing的一般是从Docker Hub中下载的镜像会有这个问题，但是问题不大。

  - -a

    Show all containers (default shows just running)
    列出所有的容器(默认仅展示运行的)

- `docker start [OPTIONS] CONTAINER [CONTAINER...]`

  Start one or more stopped containers
  启动一个或多个已停止的容器

  - `-i, --interactive`（interactive:交互式的）

    Attach container's STDIN
    保留交互界面

- `docker rm [OPTIONS] CONTAINER [CONTAINER...]`

  Remove one or more containers
  删除一个或多个的容器

- `docker rmi [OPTIONS] IMAGE [IMAGE...]`

  Remove one or more images
  删除一个或多个的镜像（当有容器使用当前删除镜像的时候不能删除）

- `docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`

  Create a new image from a container's changes
  通过更改的容器创建一个新的镜像

- `docker history [OPTIONS] IMAGE`

  Show the history of an image
  查看构建历史

- `docker build [OPTIONS] PATH | URL | -`

  - -t, --tag list

    Name and optionally a tag in the "name:tag" format
    构建容器的名字和一个可选的tag

- `docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

  Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  通过引用源镜像创建目标镜像并设置好tag

- docker network COMMAND

  Manage networks
  网络管理

  Commands:
    connect     Connect a container to a network
    create      Create a network
    disconnect  Disconnect a container from a network
    inspect     Display detailed information on one or more networks
    ls          List networks
    prune       Remove all unused networks
    rm          Remove one or more networks

  - docker network inspect [OPTIONS] NETWORK [NETWORK...]

    Display detailed information on one or more networks
    显示一个或多个网络上的详细信息

  - docker network create [OPTIONS] NETWORK

    - -d, --driver string

      Driver to manage the Network (default "bridge")

  - docker network connect [OPTIONS] NETWORK CONTAINER

    Connect a container to a network
    让容器连接一个网络

- `docker attach [OPTIONS] CONTAINER`

  Attach local standard input, output, and error streams to a running container
  将本地标准输入、输出和错误流附加到正在运行的容器

- `docker stop [OPTIONS] CONTAINER [CONTAINER...]`

  Stop one or more running containers

- `docker kill [OPTIONS] CONTAINER [CONTAINER...]`

  Kill one or more running containers

- `docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-`
  `docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH`

  Use '-' as the source to read a tar archive from stdin and extract it to a directory destination in a container.

  使用'-'作为源，从stdin读取tar存档并将其解压缩到容器中的目录目标。
  Use '-' as the destination to stream a tar archive of a container source to stdout.
  使用“-”作为目标，将容器源的tar存档流传输到标准输出。

  ```bash
  % docker cp .\test\hello.txt happy_ellis:/root/abc
  % docker cp happy_ellis:/root/abc/ .\test\
  Successfully copied 2.56kB to C:\Users\Hunter\tmp\test\
  % cd .\test\
  % ls

      Directory: C:\Users\Hunter\tmp\test

  Mode                 LastWriteTime         Length Name
  ----                 -------------         ------ ----
  d----          2023/12/22     1:04                abc
  -a---          2023/12/22     0:11             12 hello.txt
  ```

- docker volume COMMAND

  Manage volumes

  Commands:
    create      Create a volume
    inspect     Display detailed information on one or more volumes
    ls          List volumes
    prune       Remove unused local volumes
    rm          Remove one or more volumes

  - docker volume ls [OPTIONS]

     docker volume ls, docker volume list

  - docker volume inspect [OPTIONS] VOLUME [VOLUME...]

    Display detailed information on one or more volumes

    ```bash
    % docker volume inspect lbwnb
    [
        {
            "CreatedAt": "2023-12-21T17:10:59Z",
            "Driver": "local",
            "Labels": null,
            "Mountpoint": "/var/lib/docker/volumes/lbwnb/_data",
            "Name": "lbwnb",
            "Options": null,
            "Scope": "local"
        }
    ]
    ```

  - docker volume create [OPTIONS] [VOLUME]

    Create a volume

    - -d, --driver string   Specify volume driver name (default "local")

      ​							 指定卷驱动进程名称（默认为“local”）
      ​      --label list      Set metadata for a volume
      ​						   设置一个卷的元数据

    - -o, --opt map         Set driver specific options (default map[])

- docker logs [OPTIONS] CONTAINER

- docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

  Execute a command in a running container
  在正在运行的容器中执行命令(启动一个新的终端或是在容器中执行命令)

  - -i, --interactive          Keep STDIN open even if not attached
  - -t, --tty                  Allocate a pseudo-TTY

  例子：`docker exec -it test bash`

# [Rabbitmq](https://www.rabbitmq.com/)

## 安装

- Archlinux

  https://wiki.archlinux.org/title/RabbitMQ

- docker

  `docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin rabbitmq:3-management`

## 命令

- 查看运行状态

  `sudo rabbitmqctl status`
