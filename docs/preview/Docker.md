---
title: Docker
createTime: 2025/07/25 23:45:10
tags:
  - docker
permalink: /article/3r4onz0r/
---
# Docker

#### docker是什么

【docker是什么？和kubernetes(k8s)是什么关系？-哔哩哔哩】 [https://b23.tv/y5YL7N7](https://b23.tv/y5YL7N7)

程序依赖环境，环境不同，程序可能跑不起来，如果能将程序和环境一起打包，那就可以了，docker就是提供这样的功能。
#### 安装

Windows下docker提供了图形化界面的docker desktop，只需要点一点就能安装， so easy（就是默认安装到C盘了，这边建议有下C盘焦虑的搞虚拟机）

docker desktop 使用十分方便，docker hub 直接pull

如果同时运行两个MySQL，让两个容器端口不一样
#### 基础镜像是什么

之前说环境不同程序运行结果不同，所以首先要统一环境。而环境中最重要的是**操作系统**，让所有程序跑在同一个操作系统上。 操作系统分为**用户空间** 和**内核空间** 因此我们可以阉割操作系统，只是利用用户空间部分，就能构建出应用所需的环境。

#### dockerfile是什么

有了基础镜像，我们通常还需要一些依赖比如yum install gcc,甚至创建一些文件夹，最后才是运行目标程序。在Linux中我们可以把要做的事情以命令行的形式一行行列出来。 像这样一行行的列清楚了从操作系统到应用服务的文件就是dockerfile.

#### 容器镜像是什么

dockerfile只是列出来要做什么，并没有真正开始做。当用命令执行**docker build**的时候，**docker**会根据**dockerfile**的说明，一行行构建环境加应用程序，最终将**环境**和**应用程序**打包成类似压缩包的东西，就是**容器container镜像**。 我们可以在同一个操作系统上同时跑多个容器，且这些容器互相独立、互相隔离。

#### 常见命令

【40分钟的Docker实战攻略，一期视频精通Docker】[https://www.bilibili.com/video/BV1THKyzBER6?vd_source=c49ce4d1601c73b33de5f82f9bb94f97](https://www.bilibili.com/video/BV1THKyzBER6?vd_source=c49ce4d1601c73b33de5f82f9bb94f97)

- docker pull 从仓库下载镜像
    
    - 一个镜像有四部分内容
        
        docker pull docker.io/library/nginx:latest
        
        1. docker.io ：registry:仓库地址（官方仓库可省略）
            
        2. library ： namespace命名空间（作者名）
            
        3. latest ： 版本名
            
    - docker.io/library/nginx:latest 一个镜像库，存放同一个镜像的不同版本
        
    
    （会魔法的可使用魔法）
    
- sudo docker images 列出所有下载过的Docker镜像
    
- sudo docker rmi 删除镜像
    
- docker pull –platform=xxxxx nginx
    
- docker run +镜像名 ：使用镜像**创建**并**运行**容器
    
    - 后面加上 -d,分离模式，表示让容器在后台执行，不会阻塞当前窗口
        
    - -p 端口映射，每个docker容器都运行在一个独立的虚拟环境里面，容器的网络与宿主机是隔离的，默认情况下并不能直接从宿主机访问到docker的内部网络 !
        
        冒号前是宿主机端口，冒号后是容器内端口，顺序是先外后内
        
    - -v 宿主机目录：容器内目录 把宿主机与容器文件目录进行绑定，容器内对文件夹的修改会影响宿主机的文件夹，宿主机对文件夹修改同样会影响容器内文件，宿主机和容器通过这个目录，紧密的联系到了一起，即挂在卷。删除容器的时候保证容器不会删除 !
    - -e 把数据库的账号密码作为环境变量
        
    - 临时调试容器，以下这两个命令通常连在一起用
        
        - -it 让我们的控制台进入容器进行交互
            
        - --rm 当容器停止时就把容器删除
            
    - --restart 用来配置容器在停止时的重启策略
        
        - 常用的有 --restart always，只要容器停止，就会立即重启
            
        - --restart unless-stopped，与上面的区别是手动停止容器不会重启
            
- docker ps 查看正在运行的容器
    
- docker rm(删除容器) -f(强制删除正在运行的容器) + 容器名
    
- docker volume list 列出所有创建过的卷
    
- docker volume rm 删除一个卷
    
- docker volume prune -a 删除所有没有任何容器在使用的卷
    
- docker inspect + 容器名字 容器启动时的参数是什么（直接把打印出来的丢给ai）还可以查看很多容器的信息等等，问ai吧