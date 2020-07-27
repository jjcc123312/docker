# 	Docker

## 一、docker简介

### 1. Docker是什么？

> Docker 是世界领先的软件容器平台。开发人员利用 Docker 可以消除协作编码时“在我的机器上可正常工作”的问题。运维人员利用 Docker 可以在隔离容器中并行运行和管理应用，获得更好的计算密度。企业利用 Docker 可以构建敏捷的软件交付管道，以更快的速度、更高的安全性和可靠的信誉为 Linux 和 Windows Server 应用发布新功能—–《Docker中文网站》

**Docker就是一个工具，可以快速的创建和模拟各类环境的一个工具。而且性能很好，扩展性也强。相信大家都有用过虚拟机，之前的虚拟机大小动辄以G起跳，对于可怜巴巴的开发机而言，实在是耗不起。而且，启动又慢又卡。**

### 2. 为什么要用Docker

Docker容器的启动可以在秒级实现，这相比传统的虚拟机要快得多。其次，docker对系统资源的利用率很高，一台主机上可以同时运行数千个docker容器。

容器除了运行其中应用外，基本不消耗额外的系统资源，使得应用的性能很高，同时系统的开销尽量小。**传统虚拟机方式运行 10 个不同的应用就要起 10 个虚拟机，而Docker 只需要启动 10 个隔离的应用即可。**

#### 更快速的交付和部署

对开发和运维（devop）人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。

**开发者可以使用一个标准的镜像来构建一套开发容器，开发完成之后，运维人员可以直接使用这个容器来部署代码**。 Docker 可以快速创建容器，快速迭代应用程序，并让整个过程全程可见，使团队中的其他成员更容易理解应用程序是如何创建和工作的。 Docker 容器很轻很快！容器的启动时间是秒级的，大量地节约开发、测试、部署的时间。

#### 更高效的虚拟化

Docker 容器的运行不需要额外的 hypervisor （虚拟机监视器）支持，它是内核级的虚拟化，因此可以实现更高的性能和效率。

#### 更轻松的迁移和扩展

Docker 容器几乎可以在任意的平台上运行，包括物理机、虚拟机、公有云、私有云、个人电脑、服务器等。 这种兼容性可以让用户把一个应用程序从一个平台直接迁移到另外一个。

#### 更简单的管理

使用 Docker，只需要小小的修改，就可以替代以往大量的更新工作。所有的修改都以增量的方式被分发和更新，从而实现自动化并且高效的管理。

#### 对比传统虚拟机总结

| 特性       | 容器               | 虚拟机     |
| ---------- | ------------------ | ---------- |
| 启动       | 秒级               | 分钟级     |
| 硬盘使用   | 一般为 MB          | 一般为 GB  |
| 性能       | 接近原生           | 弱于       |
| 系统支持量 | 单机支持上千个容器 | 一般几十个 |

### 3. Docker基本概念及组成

> 对于Docker而言，**主要使用了容器技术。有了容器，就可以将软件运行所需的资源打包到一个隔离的容器中**。容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的库资源和设置。系统因而变得高效，轻量，自给自足，还能**保证部署在任何环境中的软件都能始终如一的运行（不被其他容器所影响）**

 <img src=".\img\70567628.jpg" style="zoom:150%;" />

**容器和虚拟机的比较**

 <img src=".\img\38728296.jpg" alt="容器和虚拟机比较" style="zoom:150%;" /> 

**Docker容器是在操作系统层面上实现虚拟化，直接复用本地主机的操作系统，而传统虚拟机则是在硬件层面实现虚拟化。与传统的虚拟机相比，Docker优势体现为启动速度快、占用体积小。**

简单来说，Docker主要由以下几个部分组成。  

<img src=".\img\1572533319152.png" alt="1572533319152" style="zoom:150%;" /> 

| 名称                           | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| Docker镜像（Images）           | Docker镜像**用于创建Docker容器的模板**，镜像是基于联合文件的一种层次结构，由一系列指令来构建。 |
| Docker容器（Container）        | **容器是独立运行的一个或一组应用。镜像相当于类，容器相当于类的实例。** |
| Docker客户端（Client）         | Docker通过命令行或者其他工具使用Docker API与Docker的守护进程通信。 |
| Docker主机(Docker Host)        | 一个物理或者虚拟的机器用于执行 Docker 守护进程和容器。       |
| Docker守护进程                 | 是Docker服务器端进程，负责支撑Docker容器的运行以及镜像的管理。 |
| Docker 仓库DockerHub(Registry) | Docker 仓库用来保存镜像，**可以理解为代码控制中的代码仓库**。 Docker Hub提供了庞大的镜像集合供使用。用户也可以将自己本地的镜像推送到Docker仓库供其他人下载。 |

- 客户端和服务端
  -  Docker是一个（C/S）架构的程序。Docker客户端只需向Docker服务器或者守护进程发出请求，服务器或者守护进程将完成所有的工作并返回结果。Docker守护进程有时也称为Docker引擎。 
- 镜像（Images）
  - 镜像就是**程序运行的环境的只读版本**。其**包含了所有程序的依赖软件和配置**。
- 容器（Container）
  - Docker利用容器来运行应用。**容器是从镜像创建的运行实例**。它可以被启动，开始，停止，删除。**每个容器都是相互隔离的，保证安全的平台**。 可以把容器看做是一个简易版的 Linux 环境（包括root用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。 
- 创库（Repository）
  - 仓库用来保存镜像，可以理解为代码控制中的代码仓库。

### 4. 应用场景

- 微服务

> 现在微服务大行其道之下，微服务拆分后，一个项目可能部署包就成倍增加了，而且可能各微服务之间的技术栈是不同的，这时候docker就是最佳选择了。 

- 持续集成和持续部署

>  结合Jenkins,通过 Docker 加速应用管道自动化和应用部署，交付速度了有很大程度的提高。 

- IT基础设施优化

> Docker 和容器有助于优化 IT 基础设施的利用率和成本。优化不仅仅是指削减成本，还能确保在适当的时间有效地使用适当的资源。 

- 容器化传统应用

> 容器不仅能提高现有应用的安全性和可移植性，还能节约成本。



## 二、Docker的安装与启动

### 1. CentOS安装Docker

#### 使用yum安装

```shell
# 1、yum 包更新到最新
sudo yum update

# 2、作用：安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依
#赖的
sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# 3、 设置yum源
# 3.1、方案一：使用ustc的（推荐）
sudo yum-config-manager --add-repo http://mirrors.ustc.edu.cn/docker-ce/linux/centos/docker-ce.repo

# 3.2、方案二：使用阿里云（可能失败）
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

# 4、 安装docker；出现输入的界面都按 y
sudo yum install -y docker-ce

# 5、查看docker版本
docker -v

# 6、查看docker信息
sudo docker info
```

#### 卸载docker

```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

#### 设置镜像

**yum源是阿里云**

> 控制台首页(产品与服务)–>容器镜像服务—>镜像加速器 

 ![img](.\img\55090666.jpg) 

 文件`/etc/docker/daemon.json`(不存在，手动创建下`daemon.json`文件)，内容为： 

```json
{
  "registry-mirrors": ["https://镜像地址.mirror.aliyuncs.com"]
}
```

**yum源是ustc**

文件`/etc/docker/daemon.json`(不存在，手动创建下`daemon.json`文件)，内容为： 

```json
{
"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
```

### 2. Docker启动，停止等命令

```shell
#1、启动docker
systemctl start docker
#2、停止docker
systemctl stop docker
#3、重启docker
systemctl restart docker
#4、查看docker状态
systemctl status docker
#5、设置开启自启动
systemctl enable docker
#6、关闭开机自启动
systemctl disable docker
#7、查看docker信息
docker info
```



## 三、Docker常用命令

### 1. 镜像相关命令

> **Docker镜像是由文件系统叠加而成（是一种文件的存储形式）**；是docker中的核心概念，**可以认为镜像就是对某些运行环境或者软件打的包**，用户可以从docker仓库下载基础镜像到本地，比如开发人员可以从docker仓库拉取（下载）一个只包含centos7系统的基础镜像，然后在这个镜像中安装jdk、mysql、Tomcat和自己开发的应用，最后将这些环境打成一个新的镜像。开发人员将这个新的镜像提交给测试人员进行测试，测试人员只需要在测试环境下运行这个镜像就可以了，这样就可以保证开发人员的环境和测试人员的环境完全一致。

![1572596399899](.\img\1572596399899.png)

**Docker关于镜像的相关操作有：**

- 查看镜像
- 搜索镜像
- 拉取镜像
- 删除镜像
- 拷贝镜像

#### 1.1. 查看镜像

```shell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        10 months ago       1.84kB
```

- REPOSITORY：镜像名称
- TAG：镜像标签
- IMAGE ID：镜像ID（唯一）
- CREATED：创建时间
- SIZE：内存大小

#### 1.2. 搜索镜像

```shell
docker search 镜像名称
```

<img src=".\img\1572599534548.png" alt="1572599534548" style="zoom:150%;" />

- name：镜像名称
- DESCRIPTION：镜像描述
- STARS：用户评价，反应一个镜像的受欢迎程度
- OFFICIAL：是否官方
- AUTOMATED：自动构建，表示该镜像由Docker Hub自动构建流程创建的

#### 1.3 拉取镜像

```shell
# 拉取镜像就是从Docker仓库下载镜像到本地，镜像名称格式为 名称:版本号，如果版本号不指定则是最新的版本 
# 命令如下：
docker pull 镜像名称:版本号
```

<img src=".\img\1572599458847.png" alt="1572599458847" style="zoom:150%;" />

#### 1.4 删除镜像

```shell
# 按照镜像id删除镜像
docker rmi 镜像Id 或者 repository

# 删除所有镜像
docker rmi `docker images -q`
```

<img src=".\img\1572599688082.png" alt="1572599688082" style="zoom:150%;" />

#### 1.5 拷贝镜像

```shell
# 比如，想创建拷贝一个镜像`hello-wrold`，同时命名为`lqdev.cn/hello-world:1`
docker tag REPOSITORY:TAG NEW_REPOSITORY:TAG
```

![1572775210048](.\img\1572775210048.png)

### 2. 容器相关命令

容器是Docker中的核心概念，容器是由镜像运行产生的运行实例。镜像和容器的关系，就如同java语言中的类和对象的关系。

Docker提供的关于容器的操作有：

- 查看容器
- 创建容器
- 启动容器
- 停止容器
- 文件拷贝
- 目录挂载
- 查看容器IP地址
- 产出容器

#### 2.1 查看容器

```shell
#查看正在运行的容器
docker ps

#查看所有的容器
docker ps -a

#查看最后创建的容器数量：docker ps -n 1
docker ps -n ?

#只查看容器的id
docker ps -q

#查看所有容器的容器id
docker ps -aq
```

<img src=".\img\1572775994057.png" alt="1572775994057" style="zoom:150%;" />

#### 2.2 创建容器

可以基于已有的镜像来创建和启动容器，创建与启动容器使用命令：`docker run`

**参数说明**

| 参数        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| -i          | 以**交互模式**运行容器，通常与 -t 同时使用；                 |
| -t          | 表示容器运行后会进入其命令行。加入这两个参数后，容器创建就能登录进去。即分配一个伪终端。 |
| --name      | 为创建的容器命名                                             |
| -v          | 表示目录映射关系（前者是宿主机目录，后者是映射到宿主机上的目录）。格式为：/.../.../...`:`/.../.../... |
| -d          | 在run后面加上-d参数,则会**创建一个守护式容器在后台运行**（这样创建容器后不会自动登录容器，如果只加`-i` `-t`两个参数，创建后就会自动进去容器）。 |
| -p          | 表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个-p做多个端口映射。格式为：主机(宿主)端口:容器端口(常用)、ip:主机端口:容器端口。 |
| -P          | 大写p，随机指定端口                                          |
| -m          | 设置容器使用内存最大值                                       |
| --link=[]   | 添加链接到另一个容器；                                       |
| --expose=[] | 开放一个端口或一组端口                                       |
| -e          | username="ritchie": 设置环境变量；                           |
| --env-file  | --env-file=[]: 从指定文件读入环境变量；                      |

##### docker run 流程图：

![img](.\img\1595401351885-30be0b17-b9be-4178-9757-7bc990e323eb.png)

##### 1）交互式容器

以**交互式方式**创建并启动容器，启动完成后，直接进入当前容器。使用`exit`命令退出容器，需要注意的是以此种方式启动容器，**如果退出容器，则容器会进入停止状态**。

```shell
# 创建并启动名称为 mycentos7 的交互式容器；下面指令中的镜像名称 centos:7 也可以使用镜像id
# docker run -i -t --name=容器名称 镜像名称:TAG 指定的command
docker run -i -t --name=mycentos7 centos:7 /bin/bash
```

<img src=".\img\1572783575113.png" alt="1572783575113" style="zoom:150%;" />

###### 从容器退回到主机

```powershell
# 容器直接突出
exit

# 容器不停止退出
ctrl + P + Q
```

##### 	2）守护式容器

创建一个**守护式容器**；如果对于一个需要长期运行的容器来说，我们可以创建一个守护式容器。命令如下（容器名称不能重复）

```shell
# 创建并启动守护式容器
docker run -i -d --name=mycentos2 centos:7 /bin/bash

# 登录进入容器命令为：docker exec -it container_name (或者 container_id) /bin/bash（exit退出时，容器不会停止）
docker exec -it mycentos2 /bin/bash
```

![1572789073852](.\img\1572789073852.png)

#### 2.3 退出容器和进入容器

##### 从容器退回到主机

```powershell
# 容器直接退出。对于交互式容器，会终止停止该容器
exit

# 容器不停止退出
ctrl + P + Q
```

##### 从主机进入容器

```powershell
# 启动容器后，自动进入容器内
docker start -i mycentos2

# 启动容器后，手动进入容器内。该命令只适用于交互式容器
docker attach mycentos2

# 启动容器后，手动进入容器内。适用于守护式容器
docker exec -it 容器ID /bin/bash 
```

**区别：**

*#docker exec #进入当前容器后开启一个新的终端，可以在里面操作。（常用）*

*#docker attach # 进入容器正在执行的终端*

#### 2.4 停止与启动容器

```shell
# 启动已有的容器：docker start 容器名称或者ID
docker start mycentos2

# 停止容器
docker stop mycentos2

# 重启容器
docker restart mycentos2

# 强制停止当前容器
docker kill mycentos2
```

![1572789198247](.\img\1572789198247.png)

#### 2.5 文件拷贝

- 将linux宿主机中的文件或文件夹拷贝到容器内可以使用命令：

```shell
# 创建一个文件
touch a.txt

# docker cp 需要拷贝的文件或文件夹 容器名称:/路径
docker cp a.txt mycemtos2:/
```

![1572794434627](.\img\1572794434627.png)

- 将文件或文件夹从容器中拷贝到linux宿主机使用命令：

```shell
# 登录容器，创建文件,然后退出
docker exec -i -t mycentos2 /bin/bash
touch b.txt
exit

# docker cp 容器名称:容器中文件的路径 linux宿主机中的位置
docker cp mycentos2:/b.txt /root
```

![1572794693715](.\img\1572794693715.png)

> 注意：容器在停止状态下也可以进行拷贝。
>
> 拷贝操作都是在linux宿主机中完成。

#### 2.6 目录挂载

可以在创建容器的时候，将宿主机的目录与容器内的目录进行映射，这样我们就可以通过修改宿主机某个目录的文件从而去影响容器。

创建容器时添加-v参数，后边为宿主机目录:容器目录，例如： `docker run -i -d -v /usr/local/test:/usr/local/test --name=mycentos3 centos:7`

```shell
# 创建linux宿主机要挂载的目录
mkdir /usr/local/test

# 创建并启动mycentos3，并挂载linux中的/usr/local/test目录到容器中的/user/local/test;也就是在linux中的/usr/local/test中操作相当于对容器相应目录操作
docker run -id -v /user/local/test:/user/local/test --name=mycentos3 centos:7

# 在linux下创建文件
touch /usr/local/test/def.txt

# 进入容器
docker exec -it mycentos3 /bin/bash

# 在容器中查看目录中是否有对应文件def.txt
ll /usr/local/test
```

![1572796767640](.\img\1572796767640.png)

> 注意：如果你共享的是多级的目录，可能会出现权限不足的提示。 这是因为CentOS7中的安全模块selinux把
> 权限禁掉了，需要添加参数 **--privileged=true** 来解决挂载的目录没有权限的问题。

#### 2.7 查看容器网络信息

```shell
# docker inspect 容器名
docker inspect mycentos1
```

![1572797303267](.\img\1572797303267.png)

> 容器之间在一个局域网内，linux宿主机器可以与容器相互通信；但是外部的物理机笔记本是不能与容器直接通信的，如果需要则需要通过宿主机器端口的代理。

#### 2.8 删除容器

```shell
# docker rm 容器名称或者容器Id
docker rm 容器名称/容器Id

# 删除所有容器
docker rm 'docker ps -a -q'
```

![1572832323489](.\img\1572832323489.png)

> 如果容器是运行状态则删除失败，需要停止容器才能删除

####  2.9 查看容器日志

```powershell
docker logs --help
Options:
      --details        Show extra details provided to logs 
*  -f, --follow         Follow log output
      --since string   Show logs since timestamp (e.g. 2013-01-02T13:23:37) or relative (e.g. 42m for 42 minutes)
*      --tail string    Number of lines to show from the end of the logs (default "all")
*  -t, --timestamps     Show timestamps
      --until string   Show logs before a timestamp (e.g. 2013-01-02T13:23:37) or relative (e.g. 42m for 42 minutes)
➜  ~ docker run -d centos /bin/sh -c "while true;do echo 6666;sleep 1;done" #模拟日志      
#显示日志
-tf		#显示日志信息（一直更新）
--tail number #需要显示日志条数
docker logs -t --tail n 容器id #查看n行日志
docker logs -ft 容器id #跟着日志
```

#### 3.0 Docker命令帮助文档（重要）

```powershell
  attach      Attach local standard input, output, and error streams to a running container
  #当前shell下 attach连接指定运行的镜像
  build       Build an image from a Dockerfile # 通过Dockerfile定制镜像
  commit      Create a new image from a container's changes #提交当前容器为新的镜像
  cp          Copy files/folders between a container and the local filesystem #拷贝文件
  create      Create a new container #创建一个新的容器
  diff        Inspect changes to files or directories on a container's filesystem #查看docker容器的变化
  events      Get real time events from the server # 从服务获取容器实时时间
  exec        Run a command in a running container # 在运行中的容器上运行命令
  export      Export a container's filesystem as a tar archive #导出容器文件系统作为一个tar归档文件[对应import]
  history     Show the history of an image # 展示一个镜像形成历史
  images      List images #列出系统当前的镜像
  import      Import the contents from a tarball to create a filesystem image #从tar包中导入内容创建一个文件系统镜像
  info        Display system-wide information # 显示全系统信息
  inspect     Return low-level information on Docker objects #查看容器详细信息
  kill        Kill one or more running containers # kill指定docker容器
  load        Load an image from a tar archive or STDIN #从一个tar包或标准输入中加载一个镜像[对应save]
  login       Log in to a Docker registry #
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

```

## 四、Docker应用部署

### 1. Mysql部署

#### 1.1 拉取镜像

```shell
# 拉取MySQL 5.7镜像
docker pull centos/mysql-57-centos7
```

![1572838491986](.\img\1572838491986.png)

#### 1.2 创建容器

`docker run -di --name=mysql5.7 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql`
`-p` 代表端口映射，格式为 宿主机映射端口:容器运行端口
`-e` 代表添加环境变量 `MYSQL_ROOT_PASSWORD` 是`root`用户的远程登陆密码（如果是在容器中使用root登录的话，那么其密码为空)

```shell
#  创建mysql5.7容器
docker run -i -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=zsl19970202. --name=mysql5.7 centos/mysql-57-centos7
```

![1572838717528](.\img\1572838717528.png)

#### 1.3 操作容器Mysql

```sh
# 进入mysql容器
docker exec -it mysql5.7 /bin/bash

# 登录容器里面的mysql
mysql -u root -p
```

![1572873819510](.\img\1572873819510.png)

#### 1.4 远程登录Mysql

```shell
# 查看ip；如果以后要内部连接该mysql，如其他容器中要连接mysql容器的mysql的时候，可以使用如下命令查看Ip
docker inspect mysql5.7
```

![1572873876353](.\img\1572873876353.png)

#### 1.5 配置Mysql主从

**1.  拉取MySQL镜像 **

```sh
docker pull mysql:5.7.13
```

**2. 创建Mysql的容器**

定义一个主的mysql容器，多个从的mysql容器

```sh
docker run -id --name=mysql-master -p 3306:3306 -e MYSQL_ROOT_PASSWORD=zsl19970202. \
mysql:5.7.13

docker run -id --name=mysql-slave1 -p 3307:3306 -e MYSQL_ROOT_PASSWORD=zsl19970202. \
mysql:5.7.13

docker run -id --name=mysql-slave2 -p 3308:3306 -e MYSQL_ROOT_PASSWORD=zsl19970202. \
mysql:5.7.13
```

**3. 创建主容器的复制账号**

进入mysql-master容器登录mysql，运行命令; Master数据库创建数据同步用户，授予用户 slave REPLICATION SLAVE权限，用于在主从库之间同步数据。 

```mysql
CREATE USER 'user_name'@'%' IDENTIFIED BY '123456';
grant replication slave on *.* to 'user_name'@'%';
或
grant replication slave on *.* to 'jjcc'@'%' IDENTIFIED by 'zsl19970202.';
# 查看账号是否创建
show grants for 'jjcc'@'%';
```

如果出现`[Err] 1055 - Expression #1 of ORDER BY clause is not in GROUP BY clause and contains nonaggregated column 'information_schema.PROFILING.SEQ' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by`，请修改`sql_mode`的值，原因出在sql的模式。

```mysql
set sql_mode = '';
set sql_mode = 'NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES';
```

**4. 修改Mysql环境配置**

 创建配置文件目录 （也可以在容器中 安装 vim 来编辑配置文件 ；命令： `apt-get update`  `apt-get install vim` ）

 目录结构如下 ：

`/usr/local/mysql/master`

`/usr/local/mysql/slave1`

`/usr/local/mysql/slave2`

 **拷贝一份MySQL配置文件** 

mysql容器中my.cnf文件存在于目录`/ect/mysql`

```sh
docker cp mysql-master:/ect/mysql/my.cnf /usr/local/master/my.cnf
```

修改my.cnf，在 [mysqld] 节点最后加上后保存 

```cnf
[mysqld]
log-bin=mysql-bin
server-id=1
```

log-bin=mysql-bin 使用binary logging，mysql-bin是log文件名的前缀

server-id=1 唯一服务器ID，非0整数，不能和其他服务器的server-id重复

**将修改后的文件覆盖Docker中MySQL中的配置文件**

```sh
docker cp /usr/local/mysql/my.cnf mysql-master:/ect/mysql/my.cnf
```

**重启容器mysql-master**

**6.  配置从Slave **

与主容器相似，拷贝配置文件至slave1目录修改后覆盖回Docker中。

修改my.cnf，在 [mysqld] 节点最后加上后保存 

```cnf
[mysqld]
## 设置server_id,注意要唯一
server-id=2  
## 开启二进制日志功能，以备Slave作为其它Slave的Master时使用
log-bin=mysql-slave-bin   
## relay_log配置中继日志
relay_log=edu-mysql-relay-bin  
```

**重启从Slave容器**

**7. 配置主从复制**

 进入Master mysql ,执行如下命令：

```mysql
show master status	
```

![1573811458619](.\img\1573811458619.png)

 进入`slave`数据库

执行如下命令：

```mysql
set sql_mode = '';
set sql_mode = 'NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES';

change master to 
master_host='172.17.0.2', 
master_user='jjcc', 
master_password='zsl19970202.', 
master_port=3306, 
master_log_file='mysql-bin.000001',
master_log_pos= 154, master_connect_retry=30;

start slave;

# Slave_IO_Running与Slave_SQL_Running如果有一个不是YES，一半是重启从容器后，事务回滚引起的，那么给出解决方法如下：
stop slave;
set GLOBAL SQL_SLAVE_SKIP_COUNTER=1;
start slave;
```

`master_port`：Master的端口号，指的是容器的端口号

`master_user`：用于数据同步的用户

`master_password`：用于同步的用户的密码

`master_log_file`：指定 Slave 从哪个日志文件开始复制数据，即**上文中提到的 File 字段的值**

`master_log_pos`：从哪个 Position 开始读，即**上文中提到的 Position 字段的值**

`master_connect_retry`：如果连接失败，重试的时间间隔，单位是秒，默认是60秒

在Slave 中的mysql终端执行`show slave status`;用于查看主从同步状态。
**使用`start slave`开启主从复制过程。**

正常情况下使用`show slave status` 命令结果：

 <img src=".\img\1573811803626.png" alt="1573811803626" style="zoom:150%;" /> 

#### 1.6 使用挂载

数据？如果数据都在容器中，那么我们容器删除，数据就会丢失！需求：数据可以持久化

MySQL，容器删除了，删库跑路！需求：MySQL数据可以存储在本地！

容器之间可以有一个数据共享的技术！Docker容器中产生的数据，同步到本地！

![在这里插入图片描述](.\img\watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODIyMzQ1,size_16,color_FFFFFF,t_70)

**总结一句话：容器的持久化和同步操作！容器间也是可以数据共享的！**

```powershell
# 获取mysql镜像
➜  ~ docker pull mysql:5.7
# 运行容器,需要做数据挂载 #安装启动mysql，需要配置密码的，这是要注意点！
# 参考官网hub 
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

#启动我们得
-d 后台运行
-p 端口映射
-v 卷挂载
-e 环境配置
-- name 容器名字
➜  ~ docker run -d -p 3306:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7

# 启动成功之后，我们在本地使用sqlyog来测试一下
# sqlyog-连接到服务器的3306--和容器内的3306映射 

# 在本地测试创建一个数据库，查看一下我们映射的路径是否ok！

```

### 2. Tomcat部署

#### 2.1 拉取镜像

```shell
# 拉取tomcat镜像
docker pull tomcat
```

![1572879212134](.\img\1572879212134.png)

#### 2.2 创建容器

```sh
# 创建tomcat容器;并挂载了webapps目录
docker run -di --name=mytomcat -p 9000:8080 -v /usr/local/tomcat/webapps:/usr/local/tomcat/webapps tomcat

# 如果出现 WARNING: IPv4 forwarding is disabled. Networking will not work.
#执行如下操作
# 1、编辑 sysctl.conf
vi /etc/sysctl.conf

# 2、在上述打开的文件中后面添加
net.ipv4.ip_forward=1

# 3、重启network
systemctl restart network
```

![1572879294234](.\img\1572879294234.png)

测试访问宿主机的端口号为9000的 tomcat。地址：http://宿主机ip:9000，也可往`/user/local/tomcat/webapps`下部署应用，然后再访问。

> 注意：**进入容器后，无法使用vim编辑文件，只能通过在宿主机中编辑好文件，通过拷贝的方式进行修改配置文件**。

### 3. Nginx部署

#### 3.1 拉取镜像

```shell
# 拉取nginx镜像
docker pull nginx
```

#### 3.2 创建容器

```shell
# 创建nginx容器
docker run -di --name=mynginx -p 80:80 nginx
```

启动后再宿主机上访问：http://宿主机IP/

### 4. Redis部署

#### 3.1 拉取镜像

```sh
# 拉取Redis镜像
docker pull redis
```

#### 3.2 创建容器

#####  创建宿主机 redis 容器的数据和配置文件目录

**用于与容器中的配置文件等进行挂载** 

```sh
# 这里我们在 /home/docker 下创建
mkdir /home/docker/redis/{conf,data} -p
cd /home/docker/redis
```

 **注意：后面所有的操作命令都要在这个目录`/home/docker/redis`下进行** 

 **获取 redis 的默认配置模版** 

```sh
# 获取 redis 的默认配置模版
# 这里主要是想设置下 redis 的 log / password / appendonly
# redis 的 docker 运行参数提供了 --appendonly yes 但没 password
wget https://raw.githubusercontent.com/antirez/redis/4.0/redis.conf -O conf/redis.conf

# 直接替换编辑
sed -i 's/logfile ""/logfile "access.log"/' conf/redis.conf;
sed -i 's/# requirepass foobared/requirepass 123456/' conf/redis.conf;
sed -i 's/appendonly no/appendonly yes/' conf/redis.conf;
sed -i 's/bind 127.0.0.1/bind 0.0.0.0/' conf/redis.conf;
```

> protected-mode 是在没有显式定义 bind 地址（即监听全网段），又没有设置密码 requirepass时，protected-mode 只允许本地回环 127.0.0.1 访问。改为bind 0.0.0.0 
>

##### 创建并运行一个名为 myredis 的容器,放到start-redis.sh脚本里面

```sh
# 创建并运行一个名为 myredis 的容器
docker run \
-p 6379:6379 \
-v $PWD/data:/data \
-v $PWD/conf/redis.conf:/etc/redis/redis.conf \
--privileged=true \
--name myredis \
-d redis:5.0.5 redis-server /etc/redis/redis.conf

# 命令分解
docker run \
-p 6379:6379 \ # 端口映射 宿主机:容器
-v $PWD/data:/data:rw \ # 映射数据目录 rw 为读写
-v $PWD/conf/redis.conf:/etc/redis/redis.conf:ro \ # 挂载配置文件 ro 为readonly
--privileged=true \ # 给与一些权限
--name myredis \ # 给容器起个名字
-d redis redis-server /etc/redis/redis.conf # deamon 运行容器 并使用配置文件启动容器内的 redis-server 
```

#### 3.3 查看活跃的容器

```sh
# 查看活跃的容器
docker ps
# 如果没有 myredis 说明启动失败 查看错误日志
docker logs myredis
# 查看 myredis 的 ip 挂载 端口映射等信息
docker inspect myredis
# 查看 myredis 的端口映射
docker port myredis
```

#### 3.4 操作redis容器

```sh
docker exec -it myredis bash
redis-cli -a 123456
```



## 五、Dockerfile文件

### 1. 什么是Dockerfile文件

Dockerfile其实就是一个文本文件，由一系列命令和参数构成，Docker可以读取Dockerfile文件并根据Dockerfile文件的描述来构建镜像。

Dockerfile文件内容一般分为4部分：

- 基础镜像信息
- 维护者信息
- 镜像操作指令
- 容器启动时执行的指令

### 2. Dockerfile常用命令

| 命令                                 | 作用                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| `FROM` image_name:tag                | 定义了使用哪个基础镜像启动构建流程                           |
| `MAINTAINER` user_name               | 声明镜像的创建者，姓名+邮箱                                  |
| `ENV` key value                      | 设置环境变量（可以写多条）                                   |
| `RUN` command                        | 是Dockerfile的核心部分（可以写多条），镜像构建的时候需要运行的命令 |
| `ADD` source_dir/file dest_dir/file  | 将宿主机的文件复制到容器内，如果是一个压缩文件，将会在复制后自动解压 |
| `COPY` source_dir/file dest_dir/file | 和ADD相似，但是如果有压缩文件并不能解压                      |
| `WORKDIR` path_dir                   | 设置镜像的工作目录                                           |
| `VOLUME`                             | 创建一个可以从本地主机或其他容器挂载的挂载点，一般用来存放数据库和需要保持的数据等。 |
| `USER`                               | 用于指定运行镜像所使用的用户                                 |
| `ARG`                                | 设置构建参数                                                 |
| EXPOSE                               | 保留端口配置                                                 |
| CMD                                  | 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代。 |
| ONBUILD                              | 当构建一个被继承 DockerFile 这个时候就会运行ONBUILD的指令，触发指令。 |

#### FROM指定基础镜像

第一条指令必须为`FROM`指令。并且，如果在同一个Dockerfile中创建多个镜像时，可以使用多个`FROM`指令（每个镜像一次）。

```dockerfile
FROM <image>
FROM <image>:<tag>
```

#### MAINTAINER（已弃用）

声明镜像的创建者

```dockerfile
MAINTAINER <name>
```

#### LABEL镜像元数据

指定维护者信息

```dockerfile
# 格式：LABEL <key>=<value> LABEL <key>=<value> ...
LABEL author="作者：Jjcc"
LABEL version="版本：0.1"
LABEL desc="说明：修改nginx首页提示"
```

 利用`docker inspect`命令进行查看。 

```
"Labels": {
                "author": "作者：Jjcc",
                "desc": "说明：修改nginx首页提示",
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>",
                "version": "版本：v0.1"
            },
```

#### RUN执行命令

 **在镜像的构建过程中执行特定的命令**，并生成一个中间镜像。 

```dockerfile
RUN <command>
或者
RUN ["executable", "param1", "param2"]
```

 第一种后边直接跟shell命令 

- 在linux操作系统上默认 `/bin/sh -c`
- 在windows操作系统上默认 `cmd /S /C`

第二种是类似于函数调用。

可将`executable`理解成为可执行文件，后面就是两个参数。

两种写法比对：

```dockerfile
RUN /bin/bash -c 'source $HOME/.bashrc; echo $HOME
RUN ["/bin/bash", "-c", "echo hello"]
```

**注意：多行命令不要写多个`RUN`，原因是Dockerfile中每个指令都会建立一层镜像。多少个RUN就构建了多少层镜像，会造成镜像的臃肿、多层，不仅仅增加了构建部件的时间，还容易出错。**

 `RUN`书写时的换行符是`\` ;

`RUN`书写时的串行符是`&&`

![img](.\img\80952556.jpg) 

#### CMD启动时命令

指定启动容器时执行的命令，每个 Dockerfile 只能有一条 `CMD` 命令。如果指定了多条命令，只有最后一条会被执行。

如果用户启动容器时候指定了运行的命令，则会覆盖掉 `CMD` 指定的命令。

```dockerfile
# 使用 exec 执行，推荐方式；
CMD ["executable","param1","param2"]

# 提供给 ENTRYPOINT 的默认参数；
CMD ["param1","param2"]

# 在 /bin/sh 中执行，提供给需要交互的应用；
CMD command param1 param2
```

 第三种比较好理解了，就是`shell`这种执行方式和写法,第一种和第二种其实都是可执行文件加上参数的形式: 

 举例说明两种写法： 

```dockerfile
CMD [ "sh", "-c", "echo $HOME" ]
CMD [ "echo", "$HOME" ]
```

 **补充细节：这里边包括参数的一定要用双引号，就是双引号`"`,不能是单引号。千万不能写成`单引号`。原因是参数传递后，`docker`解析的是一个`JSON array`。** 

#### EXPOSE设置监听端口

告诉 `Docker` 服务端容器暴露的端口号，供互联系统使用。在启动容器时需要通过 `-P`，Docker 主机会自动分配一个端口转发到指定的端口。 

为镜像设置监听端口，容器运行时会监听该端口，格式为：

```dockerfile
EXPOSE <port> [<port>/<protocol>...]
```

 如，`nginx`镜像，监听了80端口 

```dockerfile
EXPOSE 80
```

 同时，也能指定协议名，如： 

```dockerfile
EXPOSE 80/udp
```

#### ENV设置环境变量

主要就是设置环境变量，之后的命令都可以用此变量进行赋值，并在容器运行时保持，格式如下：

```dockerfile
ENV <key> <value>
ENV <key>=<value> ...
```

 例如 

```dockerfile
ENV PG_MAJOR 9.3
ENV PG_VERSION 9.3.4
RUN curl -SL http://example.com/postgres-$PG_VERSION.tar.xz | tar -xJC /usr/src/postgress && …
ENV PATH /usr/local/postgres-$PG_MAJOR/bin:$PATH
```

#### COPY复制文件

主要就是构建镜像时，进行拷贝文件到镜像的指定路径下，格式为：

```dockerfile
COPY <源路径>... <目标路径>
COPY ["<源路径1>",... "<目标路径>"]
```

复制本地主机的<src>（为dockerfile所在目录的相对路径）到容器中的 <dest> 

 当使用本地目录为源目录时，推荐使用 `COPY`。 

#### ADD更高级的复制文件

 `ADD` 指令和 `COPY` 的格式和性质基本一致。但是在 `COPY` 基础上增加了一些功能。比如`<源路径>`可以是一个 `URL`，这种情况下，`Docker` 引擎会试图去下载这个链接的文件放到`<目标路径>`去。  还可以是一个 `tar` 文件（自动解压为目录）。 

#### ENTRYPOINT启动默认命令

 `ENTRYPOINT` 用于给容器配置一个可执行程序。也就是说，每次使用镜像创建容器时，通过 `ENTRYPOINT` 指定的程序都会被设置为默认程序。`ENTRYPOINT` 有以下两种形式： 

```dockerfile
ENTRYPOINT ["executable", "param1", "param2"]
ENTRYPOINT command param1 param2
```

`ENTRYPOINT` 与 `CMD` 非常类似，不同的是通过`docker run`执行的命令不会覆盖 `ENTRYPOINT`，而`docker run`命令中指定的任何参数，都会被当做参数再次传递给`ENTRYPOINT`。

`Dockerfile` 中**只允许**有一个 `ENTRYPOINT` 命令，多指定时会覆盖前面的设置，而只执行最后的`ENTRYPOINT` 指令。

`docker run`运行容器时指定的参数都会被传递给`ENTRYPOINT`，且会覆盖 CMD 命令指定的参数。如，执行`docker run  -d`时，`-d` 参数将被传递给入口点。也可以通过`docker run --entrypoint`重写 `ENTRYPOINT` 入口点。如：可以像下面这样指定一个容器执行程序： 

```dockerfile
ENTRYPOINT ["/usr/bin/nginx"]
```

#### VOLUME定义匿名卷

VOLUME用于创建挂载点，即向基于所构建镜像创始的容器添加卷：

```dockerfile
VOLUME ["/data"]
```

**创建一个可以从本地主机或其他容器挂载的挂载点，一般用来存放数据库和需要保持的数据等。**

 一个卷可以存在于一个或多个容器的指定目录，该目录可以绕过联合文件系统，并具有以下功能： 

- 卷可以容器间共享和重用
- 容器并不一定要和其它容器共享卷
- 修改卷后会立即生效
- 对卷的修改不会对镜像产生影响
- 卷会一直存在，直到没有任何容器在使用它

 `VOLUME` 让我们可以将源代码、数据或其它内容添加到镜像中，而又不并提交到镜像中，并使我们可以多个容器间共享这些内容。 

#### USER指定当前用户

用于指定运行镜像所使用的用户:

```dockerfile
USER Jjcc
```

使用`USER`指定用户后，`Dockerfile` 中其后的命令`RUN`、`CMD`、`ENTRYPOINT`都将使用该用户。镜像构建完成后，通过`docker run`运行容器时，可以通过`-u`参数来覆盖所指定的用户。 

 当服务不需要管理员权限时，可以通过该命令指定运行用户。并且可以在之前创建所需要的用户，例如：`RUN groupadd -r postgres && useradd -r -g postgres postgres`。要临时获取管理员权限可以使用 `gosu`，而不推荐 `sudo`。 

#### WORKDIR指定工作目录

 用于在容器内设置一个工作目录： 

```dockerfile
WORKDIR /opt/docker/workdir
```

 通过`WORKDIR`设置工作目录后，`Dockerfile` 中其后的命令`RUN`、`CMD`、`ENTRYPOINT`、`ADD`、`COPY`等命令都会在该目录下执行。 

 可以使用多个 `WORKDIR` 指令，后续命令如果参数是相对路径，则会基于之前命令指定的路径。例如 

```dockerfile
WORKDIR /a
WORKDIR b
WORKDIR c
RUN pwd
```

 则最终路径为 `/a/b/c`。 

#### ARG设置构建参数

 该命令用于设置构建参数，该参数在容器运行时是获取不到的，只有在构建时才能获取。这也是其和`ENV`的区别。 

```dockerfile
ARG <name>[=<default value>]
```

 使用举例： 

```dockerfile
arg author=Jjcc
# 构建时，也可以替换了
# docker build --build-arg <varname>=<value>
docker build --build-arg author=Jjcc123321
```

#### 示例

```dockerfile
 # 注意：第一行 必须以FROM 开头。
 # FROM 指定基础镜像，即以此镜像作为基础
 FROM nginx
 # 设置元数据，利用 docker inspect [镜像名称|镜像ID],即可查看。
 LABEL author="作者：oKong"
 LABEL version="版本：v0.1"
 LABEL desc="说明：修改nginx首页提示"
 
 # 操作执行，这里直接修改了nginx的html的首页内容，/usr/share/nginx/html
# 原本想输出中文，乱码了，设置了 ENV LANG C.UTF-8 或者 ENV LANG zh_CN.UTF-8 都不行 放弃了，有知道大神望告知！
 RUN echo 'hello,oKong' > /usr/share/nginx/html/index.html
 
 # 启动命令 不写时 会直接使用基础镜像的启动命令
 # CMD ["nginx", "-g", "daemon off;"]
 # 这里利用 ENTRYPOINT 改写
 ENTRYPOINT ["nginx"]
```

 使用`docker build`构建镜像，并将镜像指定为`lqdev.cn/mynginx:v2`： 

```dockerfile
docker build -t lqdev.cn/mynginx:v2 .
```

 构建完成后，使用`lqdev.cn/mynginx:v2`启动一个容器： 

```dockerfile
docker run -p 80:80 -d lqdev.cn/mynginx:v2 -g "daemon off;"
```

 在运行容器时，我们使用了`-g "daemon off;"`，这个参数将会被传递给 `ENTRYPOINT`，最终在容器中执行的命令为 `nginx -g "daemon off;"`。此时，可利用`docker ps -a`查看下,最后效果是一样的。 <img src=".\img\9267994.jpg" alt="ps -a" style="zoom:150%;" /> 

### 3. 构建自定义镜像

1. 准备jdk、tomcat安装包，放至宿主机目录`/usr/local/dockerDivImages`
2. 进入目录`/usr/local/dockerDivImages`
3. 编写dockerfile

```dockerfile
# 基础镜像
FROM centos

# 维护者信息
LABEL author="Jjcc"
LABEL version="1.0"
LABEL desc="tomcat+jdk"

# 镜像构建时执行的指令
RUN mkdir -p /usr/local

# 将jdk压缩文件添加到镜像centos的/usr/local目录中
ADD jdk-8u231-linux-x64.tar.gz /usr/local/java/

# 将tomcat压缩文件添加到镜像centos的/usr/local目录中
ADD apache-tomcat-8.5.47.tar.gz /usr/local/tomcat/

# 添加环境变量
ENV JAVA_HOME /usr/local/java/jdk1.8.0_231
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH

ENV CATALINA_HOME /usr/local/tomcat/apache-tomcat-8.5.47
ENV CATALINA_BASE $CATALINA_HOME
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin

# 容器启动时执行的指令，这里容器启动时运行tomcat
ENTRYPOINT /usr/local/tomcat/apache-tomcat-8.5.47/bin/catalina.sh run
```

4.  利用`build`命令，构建镜像： 

```sh
docker build -t mydivimages .
```

 **注意：后面有个`.`的。表示当前所在路径** 

```sh
[root@iZbp15rmf8lyj1p9xi0shyZ dockerDivImages]# ls
apache-tomcat-8.5.47.tar.gz  dockerfile  jdk-8u231-linux-x64.tar.gz
[root@iZbp15rmf8lyj1p9xi0shyZ dockerDivImages]# docker build -t mydivimages .
Sending build context to Docker daemon  204.4MB
Step 1/14 : FROM centos
latest: Pulling from library/centos
729ec3a6ada3: Pull complete 
Digest: sha256:f94c1d992c193b3dc09e297ffd54d8a4f1dc946c37cbeceb26d35ce1647f88d9
Status: Downloaded newer image for centos:latest
 ---> 0f3e07c0138f
Step 2/14 : LABEL author="Jjcc"
 ---> Running in 04b55f6a9149
Removing intermediate container 04b55f6a9149
 ---> 040bb7e91aa5
Step 3/14 : LABEL version="1.0"
 ---> Running in 08c44d96fe0c
Removing intermediate container 08c44d96fe0c
 ---> 43be6b2c8162
Step 4/14 : LABEL desc="tomcat+jdk"
 ---> Running in 22b32d9cbbca
Removing intermediate container 22b32d9cbbca
 ---> 41d4b1ac469c
Step 5/14 : RUN mkdir -p /usr/local
 ---> Running in 3af102264fd5
Removing intermediate container 3af102264fd5
 ---> d412f6a5cc0c
Step 6/14 : ADD jdk-8u231-linux-x64.tar.gz /usr/local/java/
 ---> 583b2cc3a8c0
Step 7/14 : ADD apache-tomcat-8.5.47.tar.gz /usr/local/tomcat/
 ---> f209b34d987e
Step 8/14 : ENV JAVA_HOME /usr/local/java/jdk1.8.0_231
 ---> Running in 1fef2b36ffdb
Removing intermediate container 1fef2b36ffdb
 ---> 65ef2e3e8555
Step 9/14 : ENV JRE_HOME $JAVA_HOME/jre
 ---> Running in 95cb11061827
Removing intermediate container 95cb11061827
 ---> b9704f7f82b6
Step 10/14 : ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
 ---> Running in d217ecc8b4a8
Removing intermediate container d217ecc8b4a8
 ---> e61ff7306f92
Step 11/14 : ENV CATALINA_HOME /usr/local/tomcat/apache-tomcat-8.5.47
 ---> Running in ed9e6f175938
Removing intermediate container ed9e6f175938
 ---> 7d154e5a75de
Step 12/14 : ENV CATALINA_BASE $CATALINA_HOME
 ---> Running in 50d7f94cb48c
Removing intermediate container 50d7f94cb48c
 ---> 283ca26bbe8f
Step 13/14 : ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin
 ---> Running in c06c5c2a133b
Removing intermediate container c06c5c2a133b
 ---> 898b3ecbbc2e
Step 14/14 : ENTRYPOINT /usr/local/tomcat/apache-tomcat-8.5.47/bin/catalina.sh run
 ---> Running in 089fcf366ef5
Removing intermediate container 089fcf366ef5
 ---> 744d79d0cc95
Successfully built 744d79d0cc95
Successfully tagged mydivimages:latest
```

5. 查看镜像

![1573095333415](.\img\1573095333415.png)

6. 运行容器

```sh
docker run -d --name=mydivcontiner -p 8080:8080 mydivimages
```

7. 查看容器与登录容器

<img src=".\img\1573095401680.png" alt="1573095401680" style="zoom:150%;" />





## 六、DockerCompose

### 1. Compose简介

#### 1.1 概念

Compose项目是Docker官方的开源项目，负责实现对Docker容器集群的快速编排。他**是一个定义和运行多容器的docker应用工具**。使用compose，你能通过YMAL文件配置你的服务，然后通过一个命令，你能使用配置文件创建和运行所有的服务。

#### 1.2 组成

Docker-compose将所管理的容器分为三层，分别是工程**（Project），服务（Service）,容器（Container）**。**Docker-Compose运行目录下的所有文件**（Docker-Compose.yml，extends文件或环境变量文件等）组成一个工程，若无特殊指定工程名即为当前目录名。一个工程中可以包含多个服务，每个服务中定义了容器运行的镜像，参数，依赖。一个服务当中可以包括多个容器实例。

- **服务（service）**：**一个应用的容器，实际上可以包括若干运行相同镜像的容器实例**。每个服务都有自己的名字、使用的镜像、挂载的数据卷、所属的网络、依赖哪些其他服务等等，即以容器为粒度，用户需要Compose所完成的任务。
- **项目（project）**：**由一组关联的应用容器组成的一个完成业务单元**，在docker-compose.yml中定义。即是Compose的一个配置文件可以解析为一个项目，Compose通过分析指定配置文件，得出配置文件所需完成的所有容器管理与部署操作。

> Docker-Compose的工程配置文件默认为docker-compose.yml，可**通过环境变量COMPOSE_FILE或-f参数自定义配置文件**，其定义了多个有依赖关系的服务及每个服务运行的容器。
>
> 使用一个Dockerfile模板文件，可以让用户很方便的定义一个单独的应用容器。在工作中，经常会碰到需要多个容器相互配合来完成某项任务的情况。例如：要部署一个Web项目，除了Web服务容器，往往还需要再加上后端的数据库服务容器，甚至还包括负载均衡容器等。

### 2. 安装与卸载

#### 2.1 安装

```sh
curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 设置文件可执行权限
chmod +x /usr/local/bin/docker-compose

# 查看版本信息
docker-compose -version
```

<img src=".\img\1573008756022.png" alt="1573008756022" style="zoom:150%;" />

#### 2.2. 卸载

```sh
# 二进制包方式安装的，删除二进制文件即可
rm /usr/local/bin/docker-compose
```

#### 2.3 DockerCompose常用命令

使用Compose前，可以通过执行`docker-compose  --help|-h`来查看Compose基本命令用法。

也可以通过执行 `docker-compose [COMMAND] --help` 或者 `docker-compose --help [COMMAND]` 来查看某个具体的使用格式。

Compose命令的基本的使用格式为：

`docker-compose [-f 参数...] [options] [COMMAND] [ARGS...]`

命令选项如下：

```sh
-f，–file FILE指定使用的Compose模板文件，默认为docker-compose.yml，可以多次指定。
-p，–project-name NAME指定项目名称，默认将使用所在目录名称作为项目名。
-x-network-driver 使用Docker的可拔插网络后端特性（需要Docker 1.9 及以后版本）
-x-network-driver DRIVER指定网络后端的驱动，默认为bridge（需要Docker 1.9 及以后版本）
-verbose 输出更多调试信息
-v，–version打印版本并退出
```

**Docker Compose常用命令列表如下：**

| 命令    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| build   | 构建项目中的服务容器                                         |
| help    | 获得一个命令的帮助                                           |
| kill    | 通过发送SIGKILL信号来强制停止服务容器                        |
| config  | 验证和查看compose文件配置                                    |
| create  | 为服务创建容器。只是单纯的create，还需要使用start启动compose |
| down    | 停止并删除容器，网络，镜像和数据卷                           |
| exec    | 在运行的容器中执行一个命令                                   |
| logs    | 查看服务容器的输出                                           |
| pause   | 暂停一个服务容器                                             |
| port    | 打印某个容器端口所映射的公共端口                             |
| ps      | 列出项目中目前的所有容器                                     |
| pull    | 拉取服务依赖的镜像                                           |
| push    | 推出服务镜像                                                 |
| restart | 重启项目中的服务                                             |
| rm      | 删除**所有（停止状态的）**服务容器                           |
| run     | 在指定服务上执行一个命令                                     |
| scale   | 设置指定服务运行的容器个数                                   |
| stop    | 停止已经处于运行状态的容器，但不删除它                       |
| top     | 显示运行的进程                                               |
| unpause | 恢复处于暂停状态中的服务                                     |
| up      | 自动完成包括构建镜像、创建服务、启动服务并关闭关联服务相关容器的一些列操作 |
| version | 打印版本信息                                                 |





## 七、迁移与备份

<img src=".\img\1573110194873.png" alt="1573110194873" style="zoom:150%;" />

其中涉及到的命令有：

- `docker commit`：将容器保存为镜像
- `docker save`：将镜像备份为tar文件
- `docker load`：根据tar文件回复为镜像

### 1. 将Docker容器保存为镜像

使用`docker commit`命令可以将容器保存为镜像。

命令形式：`docker commit 容器名称|容器ID 镜像名称`

```shell
docker commit mydivcontiner mydivcontiner1
```

此镜像的内容就是当前容器的内容，接下来你可以用此镜像再次运行新的容器

### 2. 镜像备份

使用`docker save`命令可以将已有镜像保存为tar文件。

命令形式：`docker save -o tar文件名 镜像名`

```sh
# 保存镜像为文件
docker save -o mynginx.tar mynginx
```

![1573112915957](.\img\1573112915957.png)

### 3. 镜像恢复与迁移

使用`docker load`命令可以根据tar文件恢复为docker镜像。

命令形式：`docker load -i tar文件名`

```sh
# 停止mynginx容器
docker stop mynginx

# 删除mynginx容器
docker rm mynginx

# 删除mynginx镜像
docker rmi mynginx

# 加载恢复mynginx镜像
docker load -i mynginx.tar

# 在镜像恢复之后，基于该镜像再次创建启动容器
docker run -di --name=mynginx -p 80:80 mynginx
```

![1573113125541](.\img\1573113125541.png)

![1573113137014](.\img\1573113137014.png)

> **注意**：在执行docker load命令恢复镜像时，需要先删除原镜像。

### 4. 导出和导入Docker容器

##### 导出容器

 如果要导出本地某个容器，可以使用 `docker export` 命令。 

```sh
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                    PORTS               NAMES
7691a814370e        ubuntu:14.04        "/bin/bash"         36 hours ago        Exited (0) 21 hours ago                       test
$ sudo docker export 7691a814370e > ubuntu.tar
```

 这样将导出容器快照到本地文件。 

##### 导入容器快照

 可以使用 `docker import` 从容器快照文件中再导入为镜像，例如 

```sh
cat ubuntu.tar | sudo docker import - test/ubuntu:v1.0
sudo docker images
REPOSITORY          TAG                 IMAGE ID            CREATED              VIRTUAL SIZE
test/ubuntu         v1.0                9d37a6082e97        About a minute ago   171.3 MB
```

 此外，也可以通过指定 URL 或者某个目录来导入，例如 

```sh
docker import http://example.com/exampleimage.tgz example/imagerepo
```

 *注：用户既可以使用 `docker load` 来导入镜像存储文件到本地镜像库，也可以使用 `docker import` 来导入一个容器快照到本地镜像库。这两者的区别在于容器快照文件将丢弃所有的历史记录和元数据信息（即仅保存容器当时的快照状态），而镜像存储文件将保存完整记录，体积也要大。此外，从容器快照文件导入时可以重新指定标签等元数据信息。 

## 八、发布镜像

### 1. 推送至阿里云镜像

阿里云镜像仓库地址：https://cr.console.aliyun.com/repository/

#### 1.1 登录阿里云Docker Registry

```
$ sudo docker login --username=jjcc123321 registry.cn-hangzhou.aliyuncs.com
```

用于登录的用户名为阿里云账号全名，密码为开通服务时设置的密码。

您可以在访问凭证页面修改凭证密码。

#### 1.2. 从Registry中拉取镜像

```
$ sudo docker pull registry.cn-hangzhou.aliyuncs.com/1sd2/test:[镜像版本号]
```

#### 1.3. 将镜像推送到Registry

```
$ sudo docker login --username=jjcc123321 registry.cn-hangzhou.aliyuncs.com$ sudo docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/1sd2/test:[镜像版本号]$ sudo docker push registry.cn-hangzhou.aliyuncs.com/1sd2/test:[镜像版本号]
```

请根据实际镜像信息替换示例中的[ImageId]和[镜像版本号]参数。

#### 1.4. 选择合适的镜像仓库地址

从ECS推送镜像时，可以选择使用镜像仓库内网地址。推送速度将得到提升并且将不会损耗您的公网流量。

如果您使用的机器位于VPC网络，请使用 registry-vpc.cn-hangzhou.aliyuncs.com 作为Registry的域名登录，并作为镜像命名空间前缀。

### 2. 示例

使用"docker tag"命令重命名镜像，并将它通过专有网络地址推送至Registry。

```powershell
PS C:\Users\Jjcc> docker images                                                                                                                                                                                    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mysql               latest              5ac22cccc3ae        2 days ago          544MB
tomcat              latest              df72227b40e1        6 days ago          647MB
PS C:\Users\Jjcc> docker tag df72227b40e1 registry.cn-hangzhou.aliyuncs.com/1sd2/test:1                                                                                                                            PS C:\Users\Jjcc> docker images                                                                                                                                                                                    REPOSITORY                                    TAG                 IMAGE ID            CREATED             SIZE
mysql                                         latest              5ac22cccc3ae        2 days ago          544MB
tomcat                                        latest              df72227b40e1        6 days ago          647MB
registry.cn-hangzhou.aliyuncs.com/1sd2/test   1                   df72227b40e1        6 days ago          647MB

```

使用"docker images"命令找到镜像，将该镜像名称中的域名部分变更为Registry专有网络地址。

```powershell
PS C:\Users\Jjcc> docker push registry.cn-hangzhou.aliyuncs.com/1sd2/test                                                                                                                                          The push refers to repository [registry.cn-hangzhou.aliyuncs.com/1sd2/test]
aca03caac7b1: Pushed                                                                                                                                                                                               4b1785e8102b: Pushed                                                                                                                                                                                               31d7eb4c72a9: Pushed                                                                                                                                                                                               afa12e842ed4: Pushed                                                                                                                                                                                               f73b2345c404: Pushed                                                                                                                                                                                               f5181c7ef902: Pushed                                                                                                                                                                                               2e5b4ca91984: Pushed                                                                                                                                                                                               527ade4639e0: Pushed                                                                                                                                                                                               c2c789d2d3c5: Pushed                                                                                                                                                                                               8803ef42039d: Pushed                                                                                                                                                                                               1: digest: sha256:600999dceed25b0aa50f7c234a0f67ba0490516e9893db3c5aaca863a739af32 size: 2421
```

## 九、Docker网络

https://blog.csdn.net/qq_41822345/article/details/107123141#Docker__478

















