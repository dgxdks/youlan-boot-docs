## **通过Jar包部署(默认)**

### 部署说明

#### 打包特点

使用`SpringBoot`提供的`Maven`打包插件`spring-boot-maven-plugin`进行构建，所有依赖和资源文件都会打包至同一个jar文件中。此种方式支持构建Docker镜像，是文档中`Docker镜像部署`的前置操作。

#### 部署特点

* **优势：** 部署时只需要替换最新的`jar`文件即可，无需关注资源文件和依赖的变更，传输和部署方便。

* **劣势：** 因为`jar`包含了应用运行所需的所有内容，每次部署都需要重新上传，如遇频繁更新或局部更新时都可能需要对服务进行启停。比如代码没有任何改动，只想修改资源文件中的一丢丢内容，但是就有可能需要重新打包部署。

#### 内部结构

<img src="assets/img/home/deploy-jar-struct.png" alt="">

### 如何打包

#### Maven配置

> **提示：** 默认打包方式，开发者无需额外配置，详情可查看[youlan-admin/pom.xml](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-admin/pom.xml)。

```xml

<build>
    <plugins>
        <!-- *******************************通过Jar包部署[开始]******************************* -->
        <!-- SpringBoot构建Jar插件 -->
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <executions>
                <execution>
                    <goals>
                        <goal>repackage</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        <!-- *******************************通过Jar包部署[结束]******************************* -->
    </plugins>
</build>
```

#### 使用IntelliJ IDEA打包

> **提示：** 开发调试时常用此方式，如果项目需要配置CI/CD时还是需要通过下述`mvn`命令进行打包

<img src="assets/img/home/package-jar.png">

#### 使用mvn命令打包

```shell
mvn clean package -D maven.test.skip=true

```

### 如何部署

#### 创建目录

* 创建部署根目录

![create-home](project-deploy-create-home.md ":include")

* 创建部署目录

```shell
# 进入部署根目录
cd /opt/youlan-boot
# 创建部署目录
mkdir youlan-admin
# 进入部署目录
cd /opt/youlan-boot/youlan-admin

```

#### 上传文件

**上传Jar包**

> **提示：** 以`youlan-admin`为例，打包完成后Jar包会生成在`youlan-admin/target`目录下，以下示例只演示通过`scp`命令在`youlan-admin/target`目录下上传Jar包至服务器部署目录

```shell
scp youlan-admin.jar root@部署服务器IP:/opt/youlan-boot/youlan-admin
```

**上传Shell脚本(可选)**

> **提示：** 以`youlan-admin`为例，脚本存放在[youlan-admin/bin](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-admin/bin)目录下，以下示例只演示通过`scp`命令在`youlan-admin/bin`目录下上传Shell脚本至服务器部署目录。**当需要通过Shell脚本部署时此方式为必须**。

```shell
scp app.sh root@部署服务器IP:/opt/youlan-boot/youlan-admin

```

#### 部署服务

**通过java -jar部署**

```shell
# 进入部署目录
cd /opt/youlan-boot/youlan-admin
# java -jar启动服务
java -jar --spring.profiles.active=prod youlan-admin.jar

```

**通过Shell脚本部署**
> **提示：** 如需通过Shell脚本部署，请阅读上翻**上传Shell脚本**

```shell
# 进入部署目录
cd /opt/youlan-boot/youlan-admin
# 给予脚本可执行权限
chmod +x app.sh
# 启动服务
sh app.sh start
# 停止服务
sh app.sh stop

```

## **通过Zip包部署(可选)**

!> **优先推荐默认的`Jar包部署`，大多数场景还是可以满足的**。此方式并未默认集成在项目中，开发者需在充分理解此种部署方式的适用场景后再决定是否使用。

### 部署说明

#### 打包特点

使用`Maven`插件`maven-jar-plugin`、`maven-dependency-plugin`、`maven-resources-plugin`、`maven-assembly-plugin`进行组合式构建。其中源码包、依赖包、资源文件分别放置在不同目录，并最终压缩为一个Zip包。

* **maven-jar-plugin：** 此插件主要是用来定制化生成jar包中的内容

* **maven-dependency-plugin：** 此插件主要是用来将三方依赖包单独生成至指定目录下

* **maven-resource-plugin：** 此插件主要是用来将资源目录下的文件单独生成至指定目录下

* **maven-assembly-plugin：** 此插件主要是用来将上述插件生成的各个目录最终生成Zip压缩包

#### 部署特点

* **优势：** 应用运行所需的不同类型文件分目录存放，部署时可以按需替换文件，例如只想修改一处资源文件内容则只需要上传对应资源文件即可，例如只是源码有变动则只需要上传源码包即可，无需上传所有内容，传输和部署更轻盈。

* **劣势：** 由于做了“拆包”处理，如遇频繁变更依赖文件和资源文件会略显笨拙，因为每次重新部署，要么全量将Zip上传至服务器重新解压并后盖前，要么在本地先解压Zip文件后上传指定目录至服务器并后盖前。

#### 内部结构

<img src="assets/img/home/deploy-zip-struct.png" alt="">

### 如何打包

#### Maven配置

!> 当使用此部署模式时，无法与`Jar包部署`方式同时存在，所以在`pom.xml`中需要删除或注释掉`spring-boot-maven-plugin`插件配置。

> **提示：** 作为可选的部署方式，此方式并没有直接内置在项目里，以下`pom.xml`配置和`assembly.xml`配置是支持此部署方式的一种常用配置模版，开发者在充分理解一下配置内容后可自行集成至项目中。

```xml

<build>
    <plugins>
        <!-- *******************************通过Zip包部署[开始]******************************* -->
        <!-- Maven构建jar插件 -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-jar-plugin</artifactId>
            <configuration>
                <!-- 不加入jar包的文件类型或者路径 -->
                <excludes>
                    <!-- 秘钥文件目录 -->
                    <exclude>/crypto/</exclude>
                    <!-- 国际化资源文件目录 -->
                    <exclude>/i18n/</exclude>
                    <!-- .yml格式文件 -->
                    <exclude>*.yml</exclude>
                    <!-- .txt格式文件 -->
                    <exclude>*.txt</exclude>
                    <!-- .xdb格式文件 -->
                    <exclude>*.xdb</exclude>
                    <!-- .xml格式文件 -->
                    <exclude>*.xml</exclude>
                </excludes>
                <archive>
                    <manifest>
                        <!-- 程序启动主类 -->
                        <mainClass>com.youlan.AdminApplication</mainClass>
                        <!-- 是否把三方依赖jar添加至MANIFEST.MF文件中的Class-Path类路径配置中 -->
                        <addClasspath>true</addClasspath>
                        <!-- 三方依赖jar文件路径前缀，因为要把jar都放在lib目录下，所以前缀是lib -->
                        <classpathPrefix>lib</classpathPrefix>
                        <!-- 使用jar的唯一版本，不jar的详细时间戳版本 -->
                        <useUniqueVersions>false</useUniqueVersions>
                    </manifest>
                    <manifestEntries>
                        <!-- 因为资源文件都放在conf目录下，所以向Class-Path类路径配置中添加资源配置目录 -->
                        <Class-Path>conf/</Class-Path>
                    </manifestEntries>
                </archive>
                <outputDirectory>${project.build.directory}</outputDirectory>
            </configuration>
        </plugin>
        <!-- Maven复制依赖jar至指定目录插件 -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-dependency-plugin</artifactId>
            <executions>
                <execution>
                    <id>copy-dependencies</id>
                    <phase>package</phase>
                    <goals>
                        <goal>copy-dependencies</goal>
                    </goals>
                    <configuration>
                        <outputDirectory>${project.build.directory}/lib/</outputDirectory>
                    </configuration>
                </execution>
            </executions>
        </plugin>
        <!-- Maven复制资源文件至指定目录插件 -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-resources-plugin</artifactId>
            <executions>
                <execution>
                    <id>copy-resources</id>
                    <phase>package</phase>
                    <goals>
                        <goal>copy-resources</goal>
                    </goals>
                    <configuration>
                        <resources>
                            <resource>
                                <directory>src/main/resources</directory>
                            </resource>
                        </resources>
                        <outputDirectory>${project.build.directory}/conf</outputDirectory>
                    </configuration>
                </execution>
            </executions>
        </plugin>
        <!-- Maven组装多个文件目录为压缩包插件 -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <configuration>
                <!-- 这个插件需要指定一个配置文件 -->
                <descriptors>
                    <descriptor>assembly/assembly.xml</descriptor>
                </descriptors>
            </configuration>
            <executions>
                <execution>
                    <!-- 自定义 -->
                    <id>zip</id>
                    <phase>package</phase>
                    <goals>
                        <!-- 只执行一次 -->
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        <!-- *******************************通过Zip包部署[结束]******************************* -->
    </plugins>
</build>
```

<img src="assets/img/home/copy-zip-deploy.png" alt="">

#### Assembly配置

> **提示：** 最终能生成为Zip部署包依赖于`maven-assembly-plugin`插件以及`assembly.xml`配置，以`youlan-admin`模块为例，则此配置文件放置位置为`youlan-admin/assembly/assembly.xml`。

```xml

<assembly xmlns="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.0
                      http://maven.apache.org/xsd/assembly-1.1.0.xsd">
    <id>bin</id>
    <formats>
        <!-- 可以根据自己的需求定义压缩文件的格式 -->
        <format>zip</format>
    </formats>
    <!-- 不包含根目录，如果为true，生成的压缩文件会有一个根目录 -->
    <includeBaseDirectory>true</includeBaseDirectory>
    <!-- 指定需要压缩的文件清单 -->
    <fileSets>
        <fileSet>
            <!-- 指定你需要压缩的文件目录 -->
            <directory>${project.build.directory}/lib/</directory>
            <!-- 指定压缩后的文件目录 -->
            <outputDirectory>lib</outputDirectory>
            <fileMode>755</fileMode>
        </fileSet>
        <fileSet>
            <directory>${project.build.directory}/</directory>
            <includes>
                <include>${project.build.finalName}.jar</include>
            </includes>
            <outputDirectory>./</outputDirectory>
            <fileMode>755</fileMode>
        </fileSet>
        <fileSet>
            <directory>${project.build.directory}/conf/</directory>
            <outputDirectory>conf</outputDirectory>
            <fileMode>755</fileMode>
        </fileSet>
        <fileSet>
            <directory>${project.build.directory}</directory>
            <excludes>
                <exclude>**/*</exclude>
            </excludes>
            <outputDirectory>logs</outputDirectory>
        </fileSet>
    </fileSets>
</assembly>

```

<img src="assets/img/home/copy-assembly-deploy.png" alt="">

#### 使用IntelliJ IDEA打包

> **提示：** 开发调试时常用此方式，如果项目需要配置CI/CD时还是需要通过下述`mvn`命令进行打包

<img src="assets/img/home/package-zip.png">

#### 使用mvn命令打包

```shell
mvn clean package -D maven.test.skip=true

```

### 如何部署

#### 创建目录

![create-home](project-deploy-create-home.md ":include")

#### 上传文件

**上传Zip包**

> **提示：** 以`youlan-admin`为例，打包完成后Zip包会生成在`youlan-admin/target`目录下，以下示例只演示通过`scp`命令在`youlan-admin/target`目录下上传Zip包至服务器部署目录

```shell
scp youlan-admin-bin.zip root@部署服务器IP:/opt/youlan-boot
```

**解压Zip包**

```shell
# 进入部署根目录
cd /opt/youlan-boot
# 解压Zip包
unzip youlan-admin-bin.zip

```

<table>
    <tr>
        <td>
            <img src="assets/img/home/scp-zip.png" alt="">
        </td>
        <td>
            <img src="assets/img/home/unzip-zip.png" alt="">
        </td>
    </tr>
</table>

#### 部署服务

**通过java -jar部署**

```shell
# 进入部署目录
cd /opt/youlan-boot/youlan-admin
# java -jar启动服务
java -jar --spring.profiles.active=prod youlan-admin.jar

```

**通过Shell脚本部署**
> **提示：** Zip包在构建时默认集成了Shell脚本

```shell
# 进入部署目录
cd /opt/youlan-boot/youlan-admin
# 给予脚本可执行权限
chmod +x app.sh
# 启动服务
sh app.sh start
# 停止服务
sh app.sh stop

```

## **通过Docker部署(推荐)**

> **提示：** 条件允许的情况下推荐使用Docker进行项目部署，可显著提升运维效率。

### 部署说明

#### 打包特点

通过`Docker`构建工具，将`Maven`构建的产物打包为`Docker`镜像。`Docker`是基于操作系统的轻量级虚拟化技术，极大程度的降低了运维成本。无论是单体应用还是微服务架构，都可支持高效部署和灵活扩缩容。借助CI/CD工具`Jenkins`、`GitLab-CI`等，容器平台`Kubernetes`、`Rancher`、`阿里云SAE`等， 镜像仓库`Harbor`，`阿里云镜像仓库`等，可快速搭建自己技术团队的`DevOps`开发流程，是本人工作中最常用的技术之一。

#### 部署特点

* **优势：** 天然具备面向服务架构的能力，具备系统资源利用率高、运行环境相互隔离、运维操作灵活高效、易于迁移和部署、快速实现扩缩容等一众特点。

* **劣势：** 除了需要引入额外的技术栈，对部署环境也有一定的要求，例如在一个网络管控严格的部署环境下，无法从公网镜像仓库拉取`Docker`镜像，开发者也无法主动通过`Docker`默认的`2375`端口推送镜像至部署服务器，那更新镜像就是一个比较头疼的问题，还不如`Jar包部署`来的方便。

### 如何构建

#### 使用IntelliJ IDEA构建

> **提示：** 借助强大的`IntelliJ IDEA`集成开发工具，通过界面点击就能完成`Docker`相关操作，但是如果项目一旦需要集成`CI/CD`，项目中镜像的构建还是需要回归于使用`docker`命令或者插件方式。

##### 1.完成Maven构建

> **提示：** 此步骤与`Jar包部署`中的打包方式一致，此处不再重复展示。

##### 2.修改运行配置

<table>
    <tr>
        <td>
            <img src="assets/img/home/open-dockerfile-config.png" alt="">        
        </td>
        <td>
            <img src="assets/img/home/modify-dockerfile-config.png" alt="">
        </td>        
        <td>
            <img src="assets/img/home/desc-dockerfile-config.png" alt="">
        </td>
    </tr>
</table>

##### 3.添加Docker连接

<table>
    <tr>
        <td>
            <img src="assets/img/home/open-docker-connect.png" alt="">        
        </td>
        <td>
            <img src="assets/img/home/modify-docker-connect.png" alt="">
        </td>        
        <td>
            <img src="assets/img/home/desc-docker-connect.png" alt="">
        </td>
    </tr>
</table>

##### 4.添加Docker服务

<table>
    <tr>
        <td>
            <img src="assets/img/home/open-docker-service.png" alt="">        
        </td>
        <td>
            <img src="assets/img/home/add-docker-service.png" alt="">
        </td>        
        <td>
            <img src="assets/img/home/desc-docker-service.png" alt="">
        </td>
    </tr>
</table>

##### 4.执行Docker构建

<table>
    <tr>
        <td>
            <img src="assets/img/home/run-docker-build.png" alt="">        
        </td>
        <td>
            <img src="assets/img/home/finish-docker-build.png" alt="">
        </td>
    </tr>
</table>

##### 4.查看Docker镜像

<img src="assets/img/home/desc-docker-image.png" alt="">

#### 使用Maven插件构建

!> **只提供了简单的插件配置，镜像仓库的用户名/密码都直接配置在了`pom.xml`中，所以存在一定安全隐患，可开启`<useMavenSettingsForAuth>true</useMavenSettingsForAuth>`进行安全加固，开发者需自行查找配置细节。**

> **提示：** 借助`Maven`插件`dockerfile-maven-plugin`的能力，支持项目在`Maven`构建完成后根据指定的`Dockerfile`完成`Docker`镜像构建。此种方式支持`CI/CD`，但是侵入性强，强依赖于`Maven`。

##### 1.指定DOCKER_HOST

> **提示：** 通过环境变量指定`Docker`连接地址，需提前开启`Docker`的`2375`端口，示例中使用的是本地`Docker`服务。

```shell
# 设置环境变量DOCKER_HOST
export DOCKER_HOST=tcp://127.0.0.1:2375
# 查看环境变量DOCKER_HOST
echo $DOCKER_HOST

```

<img src="assets/img/home/set-docker-host.png" alt="">

##### 2.修改Maven配置

<img src="assets/img/home/modify-docker-plugin-config.png" alt="">

##### 3.执行Docker构建

<img src="assets/img/home/run-docker-plugin-build.png" alt="">

### 如何部署

#### 创建目录

![create-home](project-deploy-create-home.md ":include")

#### 上传文件

* **文件位置：** [docker/docker-compose.yml](https://gitee.com/dgxdks/youlan-boot/tree/master/docker)

<img src="assets/img/home/docker-deploy-java-file.png">

* **上传文件：**

> **提示：** 由于文件传输方式以及文件传输工具各式各样，开发者需根据自己实际情况决定如何上传，这里只展示使用的`scp`命令将部署文件上传至部署服务器对应部署根目录。

```shell
# 注意是在docker目录下执行此命令
scp docker-compose.yml root@部署服务器IP:/opt/youlan-boot

```

#### 部署服务

**通过DockerCompose部署**

!> **为了简化文档示例描述的复杂度，内置的`docker-compose.yml`文件包含了所有可能需要部署的前后端服务，所以此处只演示上线`docker-compose.yml`文件中配置的部分后端服务。实际使用时如需前后端分离部署可自行拆分此文件。**

```shell
# 进入部署目录
cd /opt/youlan-boot
# docker-compose指定部分服务上线
docker-compose up -d youlan-admin

```

<img src="assets/img/home/docker-deploy-java.png">


**通过Docker命令部署**

```shell
# 进入项目根目录
cd /opt/youlan-boot
# 创建部署根目录
mkdir youlan-admin
# 进入部署根目录
cd /opt/youaln-boot/youlan-admin
# 创建logs目录
mkdir logs
# 使用docker命令部署
docker run -it -d --name youlan-admin -p 4085:4085 -v /opt/youlan-boot/youlan-admin/logs/:/application/logs/ youlan-admin:latest

```

<img src="assets/img/home/docker-deploy-java-cmd.png">