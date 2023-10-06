* 项目结构树
~~~
youlan-web
├─ docker                                 // Docker镜像  
├─ nginx                                  // Nginx部署  
├─ src  
│  └─ api                                 // 接口
│  └─ assets                              // 资源文件
│  └─ components                          // 前端框架组件
│  └─ framework                           // 业务开发框架
│     └─ components                       // 内置组件  
│     └─ directive                        // 内置指令  
│     └─ icons                            // 内置图标  
│     └─ mixin                            // 内置混入  
│     └─ index.js                         // 业务开发框架入口js文件  
│  └─ layout                              // 前端页面布局
│  └─ router                              // 前端路由
│  └─ store                               // Vuex状态管理
│  └─ utils                               // 工具
│  └─ views                               // 功能模块页面
│     └─ components                       // 功能模块公共组件
~~~

## 关于framework目录

> [framework](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-web/src/framework) 目录是具体业务开发的核心，为了能更好的与前端整体框架进行解耦，故将业务开发相关的核心代码集中化管理，
> 这个目录汇聚了业务开发相关的组件、指令、图标、混入、工具。前端项目的开发会与此目录下的内容紧密配合。这个目录下的大部分内容，从当前项目中单独剥离出去放在陌生项目里，稍作修改同样是可以使用的，详情可见[开发框架](/docs/web-handbook/framework-methods.md)。

## 关于components目录

> 项目中有多个components组件目录，分别为：**前端框架级**[src/components](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-web/src/components)、**业务开发级**[src/framework/components](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-web/src/framework/components)、**功能模块级**[src/views/components](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-web/src/views/components)，
> 这么定义的目的是为了更好的划分不同级别组件之间的责任，递进式依赖可以避免将所有组件都归置在一起，提高代码可读性，降低维护成本。 