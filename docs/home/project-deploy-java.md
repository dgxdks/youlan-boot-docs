## 通过Jar包部署(默认)

### 部署特点

#### 打包方式

使用`SpringBoot`提供的`Maven`打包插件`spring-boot-maven-plugin`进行构建，所有依赖和资源文件都会打包至同一个jar文件中。

#### 启动方式

`java -jar`

#### 部署优势

部署时只需要替换最新的jar文件即可，无需关注资源文件和依赖的变更，传输和部署方便。

#### 不足之处

因为jar包含了应用运行所需的所有内容，每次部署都需要重新上传，如遇频繁更新或局部更新时会略显笨重。比如只想替换资源文件的内容，可能就需要重新打包部署。

#### Docker支持

此种方式支持构建Docker镜像

#### 内部结构

<img src="assets/img/java-handbook/deploy-jar-struct.png" alt="">

### 如何打包

#### Maven插件配置

> **提示：** 默认打包方式，开发者无需额外配置，详情可查看[youlan-admin/pom.xml](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-admin/pom.xml)。

```xml

<build>
    <finalName>${project.artifactId}</finalName>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <filtering>false</filtering>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
            <filtering>true</filtering>
            <includes>
                <include>banner.txt</include>
            </includes>
        </resource>
    </resources>
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

<img src="assets/img/java-handbook/package-jar.png">

#### 使用mvn命令打包

```shell
mvn clean package -D maven.test.skip=true -P Zip

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

> **提示：** 以`youlan-admin`为例，脚本存放在[youlan-admin/bin](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-admin/bin)目录下，以下示例只演示通过`scp`命令在`youlan-admin/bin`目录下上传Shell脚本至服务器部署目录。**当需要通过Shell脚本部署时此方式为必须**

```shell
scp * root@部署服务器IP:/opt/youlan-boot/youlan-admin

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
chmod +x start.sh stop.sh
# 启动服务
./start.sh
# 停止服务
./stop.sh

```

## 通过Zip包部署(可选)

### 部署特点

### 如何打包

#### Maven配置

> **提示：** 作为可选的部署方式，此方式并没有直接内置在项目里，以下`pom.xml`配置和`assembly.xml`配置是支持此部署方式的一种常用配置模版，开发者在充分理解一下配置内容后可自行集成至项目中。

!> **注意：** 当使用此部署模式时，无法与[通过Jar包部署]模式同时存在，所以在`pom.xml`中需要删除或注释掉`spring-boot-maven-plugin`插件配置。

##### pom.xml配置

```xml

<build>
    <finalName>${project.artifactId}</finalName>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <filtering>false</filtering>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
            <filtering>true</filtering>
            <includes>
                <include>banner.txt</include>
            </includes>
        </resource>
    </resources>
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

##### assembly.xml配置

> **提示：** 最终能生成为Zip部署包全部仰仗`maven-assembly-plugin`插件以及`assembly.xml`配置，以`youlan-admin`模块为例，此配置文件建议放置位置为`youlan-admin/assembly/assembly.xml`。

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

##### 图片示例

<table>
    <tr>
        <td>
            <img src="assets/img/java-handbook/hidden-jar-deploy.png" alt="" width="100%" height="100%">        
        </td>        
        <td>
            <img src="assets/img/java-handbook/copy-zip-deploy.png" alt="">        
        </td>        
        <td>
            <img src="assets/img/java-handbook/copy-assembly-deploy.png" alt="">        
        </td>
    </tr>
</table>

## 通过Docker部署

### 打包方式

#### 使用IntelliJ IDEA构建

#### 使用Maven插件构建