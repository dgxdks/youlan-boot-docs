## **通过Docker部署**

> **提示：** 以下内容默认开发者已正确安装Docker&DockerCompose，不熟悉的同学可阅读[Docker&DockerCompose安装及使用](/docs/home/project-deploy-question.md?id=Docker&DockerCompose安装及使用)。
> 此方式虽然能实现快速一键部署，但是项目自带的`docker-compose.yml`文件中组件的部署配置都是单机版的，分布式集群模式需要开发者自行搭建。

### 创建目录

> **提示：** 示例中默认项目部署根目录为`/opt/youlan-boot/`，实际部署中需要开发者根据实际情况自行决定部署根目录

```shell
# 进入/opt目录
cd /opt
# 创建部署根目录
mkdir /opt/youlan-boot
# 进入部署根目录
cd /opt/youlan-boot
```

### 上传文件

* **文件位置：** [docker/components](https://gitee.com/dgxdks/youlan-boot/tree/master/docker/components)

<img src="assets/img/home/docker-deploy-cmpt-file.png" loading="lazy">

* **上传文件：**

> **提示：** 由于文件传输方式以及文件传输工具各式各样，开发者需根据自己实际情况决定如何上传，这里只展示使用的`scp`命令将部署文件上传至部署服务器对应部署根目录。

```shell
# 注意是在docker目录下执行此命令
scp -r components/ root@部署服务器IP:/opt/youlan-boot

```

<img src="assets/img/home/docker-deploy-cmpt-upload.png" loading="lazy">

### 部署组件

> **提示：** 以下命令都是在`/opt/youlan-boot/components/`下执行的

<img src="assets/img/home/docker-deploy-cmpt-execute.png" loading="lazy">

#### 全量部署

* 上线服务

```shell
docker-compose up -d
```

* 上线服务(指定compose文件名称)

```shell
docker-compose -f docker-compose.yml up -d
```

<img src="assets/img/home/docker-deploy-cmpt-up.png" loading="lazy">

* 下线服务

```shell
docker-compose down
```

<img src="assets/img/home/docker-deploy-cmpt-down.png" loading="lazy">

* 停止服务

```shell
docker-compose stop
```

* 启动服务

```shell
docker-compose start
```

* 重启服务

```shell
docker-compose restart
```

<img src="assets/img/home/docker-deploy-cmpt-start.png" loading="lazy">

#### 部分部署

> **提示：** 项目内置的compose文件会将项目中可能需要部署的所有组件配置进去，但对于实际使用来说并不一定都是需要的，这时候可以指定部分服务名称进行部署，
> **不推荐这种方式，不需要的组件注释或删除即可。**

* 上线服务

```shell
docker-compose up -d redis
```

* 上线服务(指定compose文件名称)

```shell
docker-compose -f docker-compose.yml up -d redis
```

* 下线服务

```shell
# 不支持指定服务下线
docker-compose down
```

* 停止服务

```shell
docker-compose stop redis
```

* 启动服务

```shell
docker-compose start redis
```

* 重启服务

```shell
docker-compose restart redis
```

<img src="assets/img/home/docker-deploy-cmpt-sub-start.png" loading="lazy">