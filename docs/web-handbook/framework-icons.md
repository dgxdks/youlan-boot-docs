> **提示：** 内置了一些常用的Icon，基本都是从[RuoYi](https://gitee.com/y_project/RuoYi-Vue/tree/master/ruoyi-ui/src/assets/icons/svg)继承过来的，
> 同学们可以根据自己实际情况进行新增修改

## 如何定义Icon

> **提示：** 当前已完成了自定义Icon配置，以下内容只是为了说明是如何配置自定义Icon的

### 1.安装svg依赖

```shell
npm install svg-sprite-loader --save-dev

```

### 2.创建icons目录

当前项目的icons目录创建在 **src/framework/icons/** 下

### 3.修改vue.config.js

```javascript
config.module
    .rule('svg')
    // 先排除svg-loader对自定义icons目录的扫描
    .exclude.add(resolve('src/framework/icons'))
    .end()
config.module
    // 指定规则名称
    .rule('icons')
    // 指定匹配规则
    .test(/\.svg$/)
    // 指定扫描目录
    .include.add(resolve('src/framework/icons'))
    .end()
    // 指定laoder名称
    .use('svg-sprite-loader')
    // 指定loader
    .loader('svg-sprite-loader')
    // 配置参数
    .options({
        symbolId: 'icon-[name]'
    })
    .end()
```

### 4.创建index.js导入所有icon

```javascript
const req = require.context('./svg', false, /\.svg$/)
const requireAll = requireContext => requireContext.keys().map(item => {
    requireContext(item)
    return item.match(/\.\/(.*)\.svg/)[1]
})
const icons = requireAll(req)
export default icons
```

## 如何添加Icon

> **提示：** 仅以 [阿里巴巴矢量图标库](https://www.iconfont.cn/)为例进行说明

###  1.搜索Icon
<table>
    <tr>
        <td>
            <img src="assets/img/web-handbook/icon-search-demo.png">        
        </td>
        <td>
            <img src="assets/img/web-handbook/icon-show-demo.png">        
        </td>
    </tr>
</table>

###  2.添加Icon
<table>
    <tr>
        <td>
            <img src="assets/img/web-handbook/icon-download-demo.png">        
        </td>
        <td>
            <img src="assets/img/web-handbook/icon-add-demo.png">        
        </td>
    </tr>
</table>

## 如何使用Icon

> **提示：** 自定义Icon的具体使用请查看[Icon组件](/docs/web-handbook/framework-components.md?id=icon组件)章节

