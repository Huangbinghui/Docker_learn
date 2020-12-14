# DOCKER

## DockerFile常用指令

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