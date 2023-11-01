## **通过Nginx部署**

### 部署说明

#### 打包特点

使用`Vue`提供的`vue-cli-service`命令行工具进行`WebPack`构建，构建产物最终会生成在指定目录下。

#### 内部结构

<img src="assets/img/home/deploy-nginx-struct.png" alt="" loading="lazy">

### 如何打包

#### vue.config.js配置

> **提示：** 默认不需要修改，这里只截图展示部分配置内容

<img src="assets/img/home/deploy-nginx-vue-config.png" alt="" loading="lazy">

#### .env配置

> **提示：** .env包括`.env.development`、`.env.production`、`.env.staging`等多个文件，
> 其中`development`、`production`、`staging`指向的是不同运行环境下的环境变量配置。

<table>
    <tr>
        <td>
            <img src="assets/img/home/deploy-nginx-env-development.png" alt="" loading="lazy">            
        </td>
        <td>
            <img src="assets/img/home/deploy-nginx-env-production.png" alt="" loading="lazy">
        </td>
        <td>
            <img src="assets/img/home/deploy-nginx-env-staging.png" alt="" loading="lazy">
        </td>
    </tr>
</table>

#### nginx配置(可选)

> **提示：** 前端项目在部署前需要对`Nginx`进行必要的配置，项目中内置了基础的[nginx](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-web/nginx)配置文件供同学们使用，可根据实际部署情况修改，并在`部署阶段`覆盖服务器上默认的`Nginx`配置。

<img src="assets/img/home/nginx-config.png" loading="lazy">

#### ssl配置(可选)

> **提示：** 前端项目有时候需要支持`https`，这时候`Nginx`必须配置`ssl`证书。以`阿里云`用户为例，在完成域名申请后可申请免费证书或者购买不同机构提供的更专业的`ssl`证书。为了能更好的提供示例，本人使用`openssl`生成`自签名证书`内置在前端项目中，有时候不是公网项目，使用`自签名证书`还是能节省一些费用的。

!> **为了安全，同学们自己的真实线上环境请不要直接使用项目中提供的证书，辛苦重新生成一下！**

```shell
# 生成私钥
openssl genrsa -des3 -out youlan.com.key.secret 2048
# 生成csr证书
openssl req -new -key youlan.com.key.secret -out youlan.com.csr
# 生成不含密码的私钥
openssl rsa -in youlan.com.key.secret -out youlan.com.key
# 生成x509证书
openssl x509 -req -days 36500 -in youlan.com.csr -signkey youlan.com.key -out youlan.com.pem

```

<img src="assets/img/home/openssl-generator.png" loading="lazy">

#### 使用npm命令打包

```shell
npm run build:prod

```

<table>
    <tr>
        <td>
            <img src="assets/img/home/package-web.png" alt="" loading="lazy">        
        </td>    
        <td>
            <img src="assets/img/home/package-web-desc.png" alt="" loading="lazy">        
        </td>
    </tr>
</table>

### 如何部署

!> **由于开发者生产环境的服务器、操作系统等各种各样，甚至会选择`Nginx`以外的`Web容器`进行部署，此处暂不提供Nginx的安装教程，开发者需自行查找如何安装Nginx。**

#### 创建目录

> **提示：** 示例中默认前端项目部署根目录为`/web/html`，实际部署中需要开发者根据实际情况自行决定部署根目录。

```shell
# 进入服务器根目录
cd /
# 创建前端项目部署目录
mkdir -p /web/html
# 进入前端项目部署目录
cd /web/html

```

#### 上传文件

**上传部署文件**

> **提示：** 以`youlan-web`为例，打包完成后部署文件会生成在`youlan-web/dist`目录下，以下示例只演示通过`scp`命令在前端构建产物输出目录下上传部署文件至服务器部署目录。

```shell
scp -r * root@部署服务器IP:/web/html
```

**上传Nginx文件(可选)**

> **提示：** 以`youlan-web`为例，`Nginx`文件放置在`youlan-web/nginx`目录下，以下示例只要是通过`scp`命令将`Nginx`配置文件上传至部署服务器的`Nginx`默认配置目录下。

```shell
scp -r * root@部署服务器IP:/etc/nginx
```

## **通过Docker部署(推荐)**

### 如何构建

!> 以`youlan-web`为例，镜像构建时默认使用了`youlan-web/nginx`目录下的配置做为镜像中内置`Nginx`的配置，开发者可根据实际情况对`Dockerfile`进行修改。

#### 使用WebStorm构建

##### 1.修改运行配置

<table>
    <tr>
        <td>
            <img src="assets/img/home/open-dockerfile-config-web.png" alt="" loading="lazy">        
        </td>
        <td>
            <img src="assets/img/home/modify-dockerfile-config-web.png" alt="" loading="lazy">
        </td>        
        <td>
            <img src="assets/img/home/desc-dockerfile-config-web.png" alt="" loading="lazy">
        </td>
    </tr>
</table>

##### 2.添加Docker连接

<table>
    <tr>
        <td>
            <img src="assets/img/home/open-docker-connect-web.png" alt="" loading="lazy">        
        </td>
        <td>
            <img src="assets/img/home/modify-docker-connect-web.png" alt="" loading="lazy">
        </td>        
        <td>
            <img src="assets/img/home/desc-docker-connect-web.png" alt="" loading="lazy">
        </td>
    </tr>
</table>

##### 3.添加Docker服务

<table>
    <tr>
        <td>
            <img src="assets/img/home/open-docker-service-web.png" alt="" loading="lazy">        
        </td>
        <td>
            <img src="assets/img/home/add-docker-service-web.png" alt="" loading="lazy">
        </td>        
        <td>
            <img src="assets/img/home/desc-docker-service-web.png" alt="" loading="lazy">
        </td>
    </tr>
</table>

##### 4.执行Docker构建

<table>
    <tr>
        <td>
            <img src="assets/img/home/run-docker-build-web.png" alt="" loading="lazy">        
        </td>
        <td>
            <img src="assets/img/home/finish-docker-build-web.png" alt="" loading="lazy">
        </td>
    </tr>
</table>

##### 4.查看Docker镜像

<img src="assets/img/home/desc-docker-image-web.png" alt="" loading="lazy">

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

* **文件位置：** [docker/docker-compose.yml](https://gitee.com/dgxdks/youlan-boot/tree/master/docker)

<img src="assets/img/home/docker-deploy-java-file.png" loading="lazy">

* **上传文件：**

> **提示：** 由于文件传输方式以及文件传输工具各式各样，开发者需根据自己实际情况决定如何上传，这里只展示使用的`scp`命令将部署文件上传至部署服务器对应部署根目录。

```shell
# 注意是在docker目录下执行此命令
scp docker-compose.yml root@部署服务器IP:/opt/youlan-boot

```

#### 部署服务

##### 通过DockerCompose部署

!> **为了简化文档示例描述的复杂度，内置的`docker-compose.yml`文件包含了所有可能需要部署的前后端服务，所以此处只演示上线`docker-compose.yml`文件中配置的部分服务。实际使用时如需前后端分离部署可自行拆分此文件。**

```shell
# 进入部署目录
cd /opt/youlan-boot
# docker-compose指定部分服务上线
docker-compose up -d youlan-web

```

<img src="assets/img/home/docker-deploy-java-web.png" loading="lazy">


#####  通过Docker命令部署

```shell
# 进入项目根目录
cd /opt/youlan-boot
# 创建部署根目录
mkdir youlan-web
# 进入部署根目录
cd /opt/youaln-boot/youlan-web
# 创建logs目录
mkdir logs
# 使用docker命令部署（默认后端反向代理地址youlan-admin）
docker run -it -d --name youlan-web -p 80:80 -p 443:443 -v /opt/youlan-boot/youlan-web/logs/:/var/log/nginx youlan-web:latest
# 使用docker命令部署（指定后端反向代理地址youlan-admin对应的ip地址）
docker run -it -d --name youlan-web --add-host=youlan-admin:后端服务地址 -p 80:80 -p 443:443 -v /opt/youlan-boot/youlan-web/logs/:/var/log/nginx youlan-web:latest

```

<img src="assets/img/home/docker-deploy-web-cmd.png" loading="lazy">