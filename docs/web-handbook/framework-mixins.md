> **提示：** 混入的主要目的是将项目中公共的代码提取出来单独维护，在需要的时候引入至组件中。混入引用后是支持对混入中预先定义各种Vue属性和方法进行重写的，
> 有点Java中继承的意思。但这种方式其实是一把双刃剑，过度使用会导致代码可读性降低，定义混入前需要想清楚剥离出来的代码是否足够抽象且可以灵活扩展。

## 按钮(button.js)

* **全局混入：** 否
* **适用组件：** el-button
* **使用示例：** [新增按钮(BaseAddButton)](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseAddButton.vue)

## 增删改查([crud.js](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/mixin/crud.js))

> **提示：** 项目中比较核心的一个功能，预先定义了常规增删改查所需的属性和方法，具体的引用页面按需使用或者重写即可。
> 相较于每个页面有关增删改查逻辑即使有太多相似代码也要从头撸到尾的情况，起到了很好的改善效果。

* **全局混入：** 否
* **适用组件：** 常规实现增删改查菜单的页面
* **使用示例：** 项目中已有的增删改查相关页面都引入了此混入

## 数据字典([dict.js](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/mixin/dict.js))

> **提示：** 项目中此混入已实现全局混入，使用者无需额外导入，在公共组件中的数据字典组件无法满足使用时，可通过此方式按照字典类型快速导入字典数据。

* **全局混入：** 是
* **适用组件：** 当前组件需要使用数据字典中的数据
* **使用示例：** 详细使用请阅读 [数据字典](/docs/web-handbook/function-dict.md) 章节

## 选择树(tree.js)

* **全局混入：** 否
* **适用组件：** el-tree
* **使用示例：** [菜单树(MenuTree)](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/components/MenuTree.vue)、[机构树(OrgTree)](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/components/OrgTree.vue)

## 文件上传(upload.js)

> **提示：** 公共组件中[文件上传](/docs/web-handbook/framework-components.md?id=上传组件)组件底层上传逻辑全部引用此混入，
> 如果公共组件无法满足实际需求，可依赖此混入快速实现前后端文件上传逻辑。

* **全局混入：** 否
* **适用组件：** el-upload
* **使用示例：** [文件上传](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/FileUpload.vue)、[图片上传](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/ImageUpload.vue)