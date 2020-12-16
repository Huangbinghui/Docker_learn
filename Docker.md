# Docker

## 一、Docker简介

---

### 1、什么是Docker

> [Docker](https://www.docker.com/)是一个开源的应用容器引擎，基于GO，遵从Apache2.0协议开源。

[Docker]()可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的Linux机器上，也可以实现虚拟化。

容器是完全的沙箱机制，互相之间不会有任何接口，性能开销极低。

---

### 2、Docker架构原理

![image-20201130165613062](https://github.com/Huangbinghui/Docker_learn/blob/main/image-20201130165613062.png)



> Docker三要素：[**镜像**](#1)、[**容器**](#2)、[**仓库**](#3)。

#### 	1、镜像

​	镜像（Image）是一个只读的模板，它可以是一个可运行软件（tomcat,Mysql），也可以是一个系统（CentOS）。镜像可以用来创建容器，一个镜像可以创建很多容器。

#### 	2、容器

​	Docker利用容器（Container），可以独立运行一个或一组应用。容器是用镜像创建的运行实例。它可以被启动、开始停止删除。每个容器都是互相隔离的、保证安全的平台。

#### 	3、仓库

​	仓库是集中存放镜像文件的场所。

---

### 3、Docker用处

#### 	1 、简化环境搭建

#### 	2、 简化运维工作量

#### 	3、 微服务利器

---

### 4、 Docker与虚拟机的区别

> Docker是一个轻量级的虚拟化技术，比传统的虚拟机性能更好。

虚拟机体系结构：

![image-20201130193517659](https://github.com/Huangbinghui/Docker_learn/blob/main/image-20201130193517659.png)

* Server：真实的电脑。
* Host OS：真实电脑操作系统。
* Hypervisor：虚拟平台。
* Guest OS:虚拟平台上的系统。
* APP：虚拟平台操作系统中的应用。



Docker体系结构：

![image-20201130193724552](https://github.com/Huangbinghui/Docker_learn/blob/main/image-20201130193726562.png)

* Server：真实的电脑。
* Host OS：真实电脑操作系统。
* Docker Engine：Docker虚拟化技术。
* APP：所有的应用程序现在都作为Docker容器运行。

`这种体系结构的明显优势是，不需要为虚拟机操作系统提供硬件模拟。所有应用程序都作为Docker容器工作，性能更好。`

|            |       Docker容器        |        虚拟机（VM）         |
| :--------: | :---------------------: | :-------------------------: |
|  操作系统  |     与宿主机共享OS      |   宿主机OS上运行宿主机OS    |
|  存储大小  | 镜像小，便于存储与传输  |     镜像庞大（vmdk等）      |
|  运行性能  |   几乎无额外性能损失    | 操作系统额外的cpu、内存消耗 |
|   移植性   | 轻便、灵活、适用于Linux | 笨重、与虚拟化技术耦合度高  |
| 硬件亲和性 |     面向软件开发者      |       面向硬件运维者        |

## 二、 Docker 安装

> [官方安装教程](https://docs.docker.com/engine/install/centos/)CentOS7。

> [更换阿里云镜像](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors?accounttraceid=1c3181cb2f9e484eb6342b48a243a6ffrljg)

## 三、Docker基本命令

1、启动：`systemctl start docker`

2、重启：`systemctl restart docker`

3、停止：`systemctl stop docker`

4、开机启动：`systemctl enable docker`

5、查看概要信息：`docker info`

6、查看帮助文档：`docker --help`

7、查看版本信息：`docker version`

## 四、Docker镜像

### 1、`docker images` 列出Docker本地所有镜像。

| REPOSITORY | 镜像的仓库源       |
| ---------- | ------------------ |
| TAG        | 镜像的标签（版本） |
| IMAGE ID   | 镜像的ID           |
| CREATE     | 创建日期           |
| SIZE       | 镜像大小           |

**OPTIONS：可选参数**：

| -a             | 显示所有镜像（包括中间层） |
| -------------- | -------------------------- |
| **-q**         | **只显示镜像ID**           |
| **-qa**        | **可以组合**               |
| **--digests**  | **显示镜像的摘要信息**     |
| **--no-trunc** | **显示完整的镜像信息**     |

### 2、`docker search`搜索镜像

**OPTIONS：可选参数**：

| --no-trunc      | 显示完整的镜像描述                     |
| --------------- | -------------------------------------- |
| **-s**          | **列出收藏数不小于指定值的镜像**       |
| **--automated** | **只列出Docker Hub自动构建类型的镜像** |

### 3、`docker pull`[:TAG]下载镜像

不加TAG默认下载latest。

### 4、`docker rmi`删除镜像

不加TAG默认删除latest。

有镜像生成的容器在运行时候会报错，删除失败。

**删除多个：docker rmi** **-f 镜像名称1:[TAG] 镜像名称2:[TAG]**

**删除全部：docker rmi -f $(docker images -qa)**

## 五、Docker容器

### 1、创建并启动

> `dcoker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

| `--name "IMAGE NAME"` | 为容器指定一个名称                                 |
| --------------------- | -------------------------------------------------- |
| `-i`                  | **以交互模式运行容器，通常与-t或者-d同时使用**     |
| `-t`                  | **为容器重新分配一个伪输入终端，通常与-i同时使用** |
| `-d`                  | **后台运行容器，并返回容器ID**                     |
| `-P`                  | **随机端口映射，容器内部端口随机映射到主机的端口** |
| `-p`                  | **指定端口映射，格式为：主机(宿主)端口:容器端口**  |

* **常用命令：**
  * 启动普通容器：`docker run --name 别名 镜像ID`
  * 启动交互式容器：`docker run -it --name 别名  镜像ID`
  *  守护式方式创建并启动容器：`docker run -di --name 别名 镜像ID `
  * 启动容器，并执行/bin/bash命令：` docker run -it --name 别名 镜像ID /bin/bash命令`
  * 端口映射：`docker run -it -p 8888:8080 tomcat`或`docker run -it -P tomcat`

### 2、列出容器

> `docker ps [OPTIONS]`

| `-a`         | 列出所有容器           |
| ------------ | ---------------------- |
| `-f`         | 根据条件筛选内容       |
| `--format`   | 指定返回值的模板文件   |
| `-l`         | 显示最近创建的容器     |
| `-n`         | 显示最近创建的n个容器  |
| `--no-trunc` | 不截断输出             |
| `-q`         | 静默模式，只显示镜像ID |
| `-s`         | 显示总的文件大小       |

* **常用命令：**
  * `docker ps` 查看正在运行的容器
  * `docker ps -a` 查看所有容器
  * `docker ps -n 2` 显示最近创建的2个容器
  * `docker ps -f status=exited` 查看停止的容器

### 3、退出容器

* `exit`退出容器并停止
* `CTRL + P + Q`容器不停止退出

### 4、进入容器

* `docker attach 容器ID或容器名`

### 5、启动容器

* `docker start 容器ID或容器名`

### 6、重启容器

* `docker restart 容器ID或容器名`

### 7、停止容器

* `docker stop 容器ID或容器名`

* 暴力删除：`docker kill 容器ID或容器名 `(不推荐)

### 8、删除容器

* `docker rm -f 容器ID`强制删除
* `docker rm -f 容器ID1 容器ID2 `删除多个容器，中间空格隔开
* `docker rm -f $(docker ps -qa)`删除所有容器

### 9、宿主机和容器之间的文件拷贝

#### 			1、宿主机文件拷贝到容器

* `docker cp 需要拷贝的文件或者目录  容器名称：容器目录`

  #### 2、容器文件拷贝到宿主机

* `docker cp 容器名称：容器目录  宿主机目录`

### 10、查看容器日志

日志文件记录在`var\lib\docker\containers\容器ID\XX.log`

### 11、查看容器进程

`docker top 容器ID`

### 12、进入容器执行命令

`docker exec -it [容器名称 或者 容器ID] 执行命令`

### 13、提交运行时容器成为镜像

`docker commit -a='作者' -m='备注' 运行时容器ID 新镜像名称`

### 14、推送镜像到Hub服务器

### 15、推送镜像到阿里云

### 16、查看容器元信息

## 六、容器目录挂载

### 1、简介

我们可以在创建容器的时候，将宿主机的目录与容器内的目录进行映射，这样我们就可以实现宿主机和容器目录的双向数据自动同步；

### 2、实现

* 单目录挂载

  `docker run -it -v /宿主机目录:/容器目录 镜像名`

* 多目录挂载

  `docker run -it -v /宿主机目录:/容器目录 -v /宿主机目录2:/容器目录2 镜像名`

* 挂载目录为只读

  `docker run -it -v /宿主机目录:/容器目录:ro 镜像名`

## 七、Docker常用软件安装

### 	1、Docker上安装Tomcat及配置

* 第一步：先运行一个容器
* 第二步：宿主机里home目录下新建tomcat目录，复制容器里conf,webapps到宿主机

```shell
docker cp 容器id:/usr/local/tomcat/conf  /home/tomcat/
docker cp 容器id:/usr/local/tomcat/webapps  /home/tomcat/
```

* 第三步：把容器里的tomcat里的webapp，logs，conf挂载到宿主机tomcat目录下，方便上传代码，同步持久化日志，以及方便配置tomcat；

```shell
 docker run -d --name 容器名称 -p 80:8080 -v /home/tomcat/conf/:/usr/local/tomcat/conf/  -v /home/tomcat/webapps/:/usr/local/tomcat/webapps/ -v /home/tomcat/logs/:/usr/local/tomcat/logs/  镜像ID
```

* 第四步：配置tomcat server.xml 以及 同步上传war包

```xml
<Context path="" docBase="/usr/local/tomcat/webapps/WebTest" debug="0" reloadable="true" />   
```

### 	2、Docker上安装mysql5.7以及配置

* 第一步：运行容器

  

* 第二步：宿主机里home目录下新建mysql目录，复制容器里conf,webapps到宿主机

   ``` shell
  docker cp 容器id:/etc/mysql/conf.d /home/mysql/
  
  docker cp 容器id::/var/log /home/mysql/
  
  docker cp 容器id::/var/lib/mysql /home/mysql/ 
  ```

   

* 第三步：把容器里的tomcat里的webapp，logs，conf挂载到宿主机tomcat目录下，方便上传代码，同步持久化日志，以及方便配置tomcat；关掉容器，启动容器；

  ```shell
  docker run -p 3306:3306 -d -v /etc/mysql/conf.d/:/home/mysql/conf/ -v /var/log:/home/mysql/log/ -v /var/lib/mysql/:/home/mysql/mysql/ -e MYSQL_ROOT_PASSWORD=123456 镜像ID
  ```

  

* 第四步：导入sql脚本 

## 八、Docker迁移与备份

> 我们开发的时候，经常自定义镜像，然后commit提交成镜像到本地仓库，但是我们发布到客户服务器的时候，可以用前面讲得搞到hub官方，或者阿里云，但是有些机密性的项目，是禁止公网存储的，所以我们只能通过docker镜像备份和迁移实现；

### 	1、备份镜像

```shell
docker save -o 备份镜像的名称  源镜像名称:tag版本

docker save -o mytomcat7.1.tar java1234/tomcat7:7.1
```

### 	2、恢复镜像

```shell
docker load -i 镜像文件

docker load -i mytomcat7.1.tar
```

## 九、DockerFile

### 	1、DockerFile简介

> Dockerfile是由一系列命令和参数构成的脚本，这些命令应用于操作系统(centos或者Ubuntu)基础镜像并最终创建的一个新镜像；
>
>  
>
> 我们前面讲过的用手工的方式，修改配置文件，或者添加，删除文件目录的方式，来构建一种新镜像；这种手工方式麻烦，容易出错，而且不能复用；
>
> 我们这里讲Dockerfile，用脚本方式来构建自动化，可复用的，高效率的创建镜像方式，是企业级开发的首选方式；
>
>  
>
> 再软件系统开发生命周期中，采用Dockerfile来构建镜像；
>
> 1、对于开发人员:可以为开发团队提供一个完全一致的开发环境;
>
> 2、对于测试人员:可以直接拿开发时所构建的镜像或者通过Dockerfile文件构建一个新的镜像开始工作；
>
> 3、对于运维人员:在部署时，可以实现应用的无缝移植。

### 	2、DockerFile常用命令

* `FROM image_name:tag` ：定义了使用哪个基础镜像启动构建流程
* `MAINTAINER user_info` ：声明镜像维护者信息
* `LABEL key value`：镜像描述元信息（可以写多条）
* `ENV key value`：设置环境变量（可以写多条）
* `RUN command` : 构建镜像时需要运行的命令（可以写多条）
* `WORKDIR path_dir` ：设置终端默认登录进来的工作目录
* `EXPOSE port` ：当前容器对外暴露的端口
* `ADD source_dir/file dest_dir/file` ：讲宿主机文件复制到容器内，如果是压缩文件，将在复制后自动解压。
* `COPY source_dir/file dest_dir/file` ：和ADD类似，但如果有压缩文件不会自动解压。
* `VOLUME` ：创建一个可以从本地主机或者其他容器挂载的挂载点，一般存放数据库和需要保持的数据等。
* `CMD `：指定启动容器时要运行的命令，假如有多个，最后一个生效
* `EntryPOINT` ：指定容器启动时要运行的命令
* `ONBUILD` ：当一个被继承的DockerFile时运行的命令，父镜像在被子镜像继承后父镜像的ONBUILD触发。可以把ONBUILD理解为一个触发器。

## 十、DockerFile构建自定义CentOS

### 1、编写DockerFile

```dockerfile
FROM centos

MAINTAINER caofeng<caofeng2012@126.com>



LABEL name="Java1234 CentOS Image" \

    build-date="20191112"

    

ENV WORKPATH /home/

WORKDIR $WORKPATH



RUN yum -y install net-tools

RUN yum -y install vim



EXPOSE 80

CMD /bin/bash
```

### 2、构建

`docker build -f MycentOSDockerFile -t hbh/CentOS:1.1 .` ：**注意后面要有个句号**

### 3、运行

`docker run -it 镜像ID`

### 4、查看历史镜像

`docker history镜像ID `

## 十一、Docker私有仓库

### 1、搭建

* 第一步：拉取私有仓库镜像 （私有仓库程序本身就是一个镜像）

* 第二步：启动私有仓库容器

  `docker run -di --name=myRegistry -p 5000:5000 registry`

* 第三步：测试

  http://192.168.1.112:5000/v2/_catalog

* 第四步：etc/docker 修改daemon.json，让docker信任私有仓库地址

  `"insecure-registries": ["192.168.1.112:5000"]`

* 第五步：修改配置后重启docker；

  ` systemctl restart docker`

### 2、测试

* 第一步：标记此镜像为私有仓库的镜像

  `docker tag tomcat:7 192.168.1.112:5000/mytomcat7`

* 第二步：上传镜像到私有仓库

  `docker push 192.168.1.112:5000/mytomcat7`

* 第三步：删除192.168.1.112:5000/mytomcat7本地仓库镜像

  `docker rmi -f 192.168.1.112:5000/mytomcat7`

* 第四步：从私有仓库拉取192.168.1.112:5000/mytomcat7镜像，并运行；

  `docker run -it -p 8080:8080 192.168.1.112:5000/mytomcat7`

* 第五步：浏览器运行 http://192.168.1.112:8080测试

