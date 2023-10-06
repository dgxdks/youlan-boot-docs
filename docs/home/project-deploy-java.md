> 本人根据自己对过往的项目经历的总结，为当前项目配置了几个区别较为明显的主流部署方式，每一种方式都有自己适合的应用场景，同学们可根据自己的需求灵活配置和使用。
**以下文档中所涉及后端代码示例来源于[youlan-admin](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-admin)
> ，前端示例来源于[youlan-web](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-web)，在扩展新的部署模块时可参考示例模块配置，内容基本大同小异。
**

* 部署方式比较

| 部署方式     | 打包特点                                                      | 应用场景 | Docker支持 |
|----------|-----------------------------------------------------------|------|----------|
| Jar包部署   | 使用SpringBoot提供的打包插件进行构建，所有依赖和资源文件都会集中在一个jar文件中            |      |          |
| Zip包部署   | 使用多种Maven插件组合进行构建，相同根目录下源码包、依赖包、资源文件归置在不同目录下并最终压缩为一个zip文件 |      |          |
| Docker部署 |                                                           |      |          |

## 通过Jar包部署(默认)

### 打包配置

```xml

<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <version>${springboot.version}</version>
    <executions>
        <execution>
            <goals>
                <goal>repackage</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

> **spring-boot-maven-plugin**
> 是SpringBoot提供的Maven打包插件，打包完成后会生成一个可执行jar文件，文件中包含了当前应用所需的所有依赖和资源文件，可通过jar -jar命令直接启动

## 通过Zip包部署

## 通过Docker镜像部署

### 打包方式

#### 使用IntelliJ IDEA构建

#### 使用Maven插件构建