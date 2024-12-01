## **通过Docker部署**

### 部署说明

!> 通过`Docker`进行全量部署是指通过`DockerCompose`对全量服务进行服务编排，从而实现全量服务的部署相关操作，项目中内置的`docker/docker-compose.yml`已集成了当前项目的全量服务。

### 如何打包

!> 此步骤可参考前后端部署中关于`通过Docker部署`的教程，需先行完成前端端服务的镜像构建，才可进行`Docker全量部署`。

### 如何部署

#### 创建目录

> **提示：** 示例中默认项目部署根目录为`/opt/youlan-boot/`，实际部署中需要开发者根据实际情况自行决定部署根目录

```shell
# 进入/opt目录
cd /opt
# 创建部署根目录
mkdir /opt/youlan-boot
# 进入部署根目录
cd /opt/youlan-boot
```

#### 上传文件

* **文件位置：** [docker/docker-compose.yml](https://gitee.com/kensenzhao/youlan-boot/tree/master/docker)

<img src="/assets/img/home/docker-deploy-java-file.png" loading="lazy">

* **上传文件：**

> **提示：** 由于文件传输方式以及文件传输工具各式各样，开发者需根据自己实际情况决定如何上传，这里只展示使用的`scp`命令将部署文件上传至部署服务器对应部署根目录。

```shell
# 注意是在docker目录下执行此命令
scp docker-compose.yml root@部署服务器IP:/opt/youlan-boot

```

#### 部署服务

##### 上线服务
```shell
# 进入部署目录
cd /opt/youlan-boot
# docker-compose上线全量服务
docker-compose up -d
# docker-compose下线全量服务
docker-compose down
```
