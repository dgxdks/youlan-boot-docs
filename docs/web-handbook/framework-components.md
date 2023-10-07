## 按钮组件

### 新增按钮([base-add-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseAddButton.vue))

* 基础用法

```vue

<base-add-button v-has-perm="['system:config:add']" plain @click="handleAdd"/>
```

### 删除按钮([base-remove-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseRemoveButton.vue))

* 基础用法

```vue

<base-remove-button v-has-perm="['monitor:onlineUser:kickout']" type="text" @click="handleKickout(scope.row)">强踢</base-remove-button>
```

### 修改按钮([base-update-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseUpdateButton.vue))

* 基础用法

```vue

<base-update-button v-has-perm="['system:config:update']" plain :disabled="!tableSelectOne" @click="handleUpdate"/>
```

### 搜索按钮([base-search-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseSearchButton.vue))

* 基础用法

```vue

<base-search-button @click="handleQuery"/>
```

### 重置按钮([base-reset-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseResetButton.vue))

* 基础用法

```vue

<base-reset-button @click="handleResetQuery"/>
```

### 上传按钮([base-upload-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseUploadButton.vue))

* 基础用法

```vue

<base-upload-button type="primary" plain @click="handleFileUpload">文件上传</base-upload-button>
```

### 下载按钮([base-download-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDownloadButton.vue))

* 基础使用

```vue

<base-download-button v-has-perm="['system:config:export']" plain @click="handleExport">导出</base-download-button>
```

### 关闭按钮([base-close-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseCloseButton.vue))

* 基础使用

```vue

<base-close-button plain @click="handleClose">关闭</base-close-button>
```

### 文本按钮([base-text-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseTextButton.vue))

* 基础使用

```vue

<base-text-button
    v-has-perm="['system:role:update']"
    icon="el-icon-circle-check"
    color="#606266"
    @click="handleDataScope(scope.row)"
>
  数据权限
</base-text-button>
```

### 开关按钮([base-switch](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseSwitch.vue))

* 基础用法

```vue

<base-switch v-model="scope.row.status" :disabled="$auth.isAdminRole(scope.row.id)" @change="handleStatusChange(scope.row)"/>
```

### 菜单按钮([base-menu-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseMenuButton.vue))

* 基础用法

```vue

<base-menu-button>
  <base-text-button
      v-has-perm="['system:user:updatePasswd']"
      icon="el-icon-key"
      color="#606266"
      @click="handleResetPwd(scope.row)"
  >重置密码
  </base-text-button>
  <base-text-button
      v-has-perm="['system:user:update']"
      icon="el-icon-circle-check"
      color="#606266"
      @click="handleAuthRole(scope.row)"
  >分配角色
  </base-text-button>
</base-menu-button>
```

### 示例图片

<img src="assets/img/web-handbook/button-demo.png" alt="">

## 上传组件

### 文件上传([file-upload](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/FileUpload.vue))

> **提示：** 虽然功能不同，但是底层上传逻辑基本是一致的，所以在实现这几个组件的时候使用了代码混入，使用细节请阅读[文件上传(upload.js)](/docs/web-handbook/framework-mixins.md?id=文件上传uploadjs)混入

* 普通上传([file-upload](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/FileUpload.vue))

```vue

<file-upload
    ref="upload"
    :action="upload.action"
    :accept="upload.accept"
    :form-data="{cover: upload.cover}"
    @onError="handleImportError"
    @onSuccess="handleImportSuccess"
>
  <template slot="tip">
    <el-checkbox v-model="upload.cover"/>
    是否更新已经存在的用户数据
  </template>
  <span>仅允许导入xls、xlsx格式文件。</span>
  <el-link
      :underline="false"
      style="font-size:12px;vertical-align: baseline;"
      type="primary"
      @click="handleDownloadTemplate"
  >下载模板
  </el-link>
</file-upload>
```

* 拖拽上传([file-upload-drag](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/FileUploadDrag.vue))

```vue

<file-upload-drag
    ref="upload"
    :action="upload.action"
    :accept="upload.accept"
    :form-data="{cover: upload.cover}"
    @onError="handleImportError"
    @onSuccess="handleImportSuccess"
>
  <template slot="tip">
    <el-checkbox v-model="upload.cover"/>
    是否更新已经存在的用户数据
  </template>
  <span>仅允许导入xls、xlsx格式文件。</span>
  <el-link
      :underline="false"
      style="font-size:12px;vertical-align: baseline;"
      type="primary"
      @click="handleDownloadTemplate"
  >下载模板
  </el-link>
</file-upload-drag>
```

### 图片上传([image-upload](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/ImageUpload.vue))

* 基础用法

```vue

<image-upload
    ref="imageUpload"
    :limit="3"
    :file-size="5"
    @onSuccess="handleImageUploadSuccess"
    @onError="handleImageUploadError"
/>
```

### 示例图片

<table>
    <tbody>
        <tr>
            <td>
                <img src="assets/img/web-handbook/file-upload-demo.png" alt="">
            </td>
            <td>
                <img src="assets/img/web-handbook/file-upload-drag-demo.png" alt="">
            </td>
            <td>
                <img src="assets/img/web-handbook/image-upload-demo.png" alt="">
            </td>
        </tr>        
    </tbody>
</table>

* 基础使用

## 时间组件

### 日期选择([base-date-range-picker](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDateRangePicker.vue))

* 日期选择

```vue

<base-date-range-picker v-model="queryForm.createTime" type="date" style="width: 240px"/>
```

* 日期范围选择

```vue

<base-date-range-picker v-model="queryForm.createTimeRange" style="width: 240px"/>
```

### 时间选择([base-date-time-range-picker](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDateTimeRangePicker.vue))

* 时间选择

```vue

<base-date-time-range-picker v-model="queryForm.loginTime" type="datetime" style="width: 240px"/>
```

* 时间范围选择

```vue

<base-date-time-range-picker v-model="queryForm.loginTimeRange" style="width: 340px"/>
```

### 示例图片

<table>
    <tbody>
        <tr>
            <td>
                <img src="assets/img/web-handbook/date-range-picker-demo.png" alt="">
            </td>
            <td>
                <img src="assets/img/web-handbook/date-time-range-picker-demo.png" alt="">
            </td>
        </tr>        
        <tr>
            <td>
                <img src="assets/img/web-handbook/date-picker-demo.png" alt="">
            </td>
            <td>
                <img src="assets/img/web-handbook/date-time-picker-demo.png" alt="">
            </td>
        </tr>
    </tbody>
</table>

## Icon组件

### 基础Icon([base-svg-icon](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseSvgIcon.vue))

> **提示：** 内置Icon都存放在项目[svg](https://gitee.com/dgxdks/youlan-boot/tree/master/youlan-web/src/framework/icons/svg)目录下，不带后缀的icon文件名称就是icon-class属性值。
> 例如icon文件名称为404.svg，如果需要使用则需要指定icon-class=“404”，不需要.svg后缀。而class-name="search-icon"的作用是为了自定义icon样式，其属性值"search-icon"指定的是css中的class类名。

* 基础用法

```vue
<!-- 两个组件名称都指向的是同一个组件-->
<svg-icon class-name="search-icon" icon-class="search" @click.stop="click"/>
<base-svg-icon class-name="search-icon" icon-class="search" @click.stop="click"/>
```

### 内容复制Icon([base-copy-icon](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseCopyIcon.vue))

> **提示：** 有时候当需要复制页面中的文本内容时会插入一个可点击的图标表示内容可复制，这个组件实现了此基础功能

* 基础用法

```vue

<base-copy-icon v-model="item.codeContent" show-message style="float:right">复制</base-copy-icon>
```

### 下拉选择Icon([base-icon-select](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseIconSelect.vue))

> **提示：** 将项目内置的所有icon以下拉选择框的形式进行展示，支持选择和搜索

* 基础用法

```vue

<base-icon-select ref="iconSelect" v-model="editForm.menuIcon"/>
```

### 示例图片

<table>
    <tbody>
        <tr>
            <td>
                <img src="assets/img/web-handbook/copy-icon-demo.png" alt="">
            </td>
            <td>
                <img src="assets/img/web-handbook/icon-select-demo.png" alt="">
            </td>
        </tr>
    </tbody>
</table>

## 数据字典组件

> **提示：** 数据字典组件v-model绑定的值，数据类型都会被转为String类型，在向后端传值以及后端返回数据前端回显的时候需要注意数据类型

### 单选框([dict-radio](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/DictRadio.vue))

```vue

<dict-radio v-model="editForm.isDefault" dict-type="db_yes_no"/>
```

### 复选框([dict-checkbox](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/DictCheckbox.vue))

```vue

<dict-checkbox v-model="editForm.orgTypeList" dict-type="sys_org_type"/>
```

### 标签([dict-tag](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/DictTag.vue))

```vue

<dict-tag v-model="scope.row.orgType" dict-type="sys_org_type"/>
```

### 下拉选择([dict-select](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/DictSelect.vue))

```vue

<dict-select v-model="editForm.sex" dict-type="sys_user_sex" placeholder="请选择性别"/>
```

### 示例图片

<table>
    <tbody>
        <tr>
            <td>
                <img src="assets/img/web-handbook/dict-select-radio-demo.png" alt="">
            </td>
            <td>
                <img src="assets/img/web-handbook/dict-tag-demo.png" alt="">
            </td>
        </tr>
    </tbody>
</table>

## 其他组件

### 基础弹窗([base-dialog](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDialog.vue))

* 基础用法

```vue
<!-- 字典类型对话框 -->
<base-dialog :title="editTitle" :open.sync="editOpen" width="500px" @confirm="handleEditSubmit" @cancel="handleEditCancel">
  <el-form ref="editForm" :model="editForm" :rules="editRules" label-width="100px">
  </el-form>
</base-dialog>
```

### 抽屉弹窗([base-drawer](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDrawer.vue))

* 基础用法

```vue

<!-- 存储记录详细 -->
<base-drawer title="存储记录详情" :open.sync="editOpen" size="80%" wrapper-closable>
  <el-form ref="editForm" :model="editForm" label-width="100px" size="mini" label-position="left" style="padding: 10px">
  </el-form>
</base-drawer>
```

### 图片预览([image-preview](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/ImagePreview.vue))

* 基础用法

```vue

<image-preview :src="editForm.fullUrl" :width="150" :height="150"/>
```

### 表格工具栏([table-toolbar](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/TableToolbar.vue))

* 基础用法

```vue

<template>
  <table-toolbar :columns.sync="columns" :query-show.sync="queryShow" @refresh="getList"/>
</template>
<script>
  export default {
    data() {
      return {
        // 动态控制表格中的列是否显示
        columns: {
          id: {label: '用户编号', show: true},
          userName: {label: '用户名称', show: true},
          nickName: {label: '用户昵称', show: true},
          orgName: {label: '组织机构', show: true},
          userMobile: {label: '手机号码', show: true},
          status: {label: '状态', show: true},
          createTime: {label: '创建时间', show: true}
        }
      }
    }
  }
</script>
```

### 表单标签([base-form-label](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseFormLabel.vue))

* 基础用法

> **提示：**  如果需要覆盖el-form-item表单元素中默认的label标签内容时，可通过插槽进行替换

```vue

<el-form ref="editForm" :model="editForm" :rules="editRules" label-width="100px">
  <el-form-item label="字典类型" prop="typeKey">
    <!-- 插槽替换 -->
    <base-form-label slot="label" content="字典类型必须以字母开头，且只能为（小写字母，数字，下滑线）" label="字典类型"/>
    <el-input v-model="editForm.typeKey" placeholder="请输入字典类型"/>
  </el-form-item>
</el-form>
```

### 分割布局([base-row-split](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseRowSplit.vue))

> **提示：**  等分布局对栅格布局el-row和el-col组合的封装，实现了将一行空间均分为N的布局方式。子组件会按照一行N个的方式依次排列下去，同时支持v-if，当子组件中出现
> v-if="false" 时，后续元素会依次递进上来

* 自定义分割([base-row-split](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseRowSplit.vue))

```vue

<base-row-split :span="1.5" :gutter="10">
  <el-form-item label="平台名称：" prop="platform">
    {{ editForm.platform }}
  </el-form-item>
  <el-form-item label="文件名称：" prop="fileName">
    {{ editForm.fileName }}
  </el-form-item>
</base-row-split>
```

* 二分之一分割([base-row-split2](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseRowSplit2.vue))

```vue

<base-row-split2>
  <el-form-item label="平台名称：" prop="platform">
    {{ editForm.platform }}
  </el-form-item>
  <el-form-item label="文件名称：" prop="fileName">
    {{ editForm.fileName }}
  </el-form-item>
</base-row-split2>
```

* 三分之一分割([base-row-split3](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseRowSplit3.vue))

```vue

<base-row-split3>
  <el-form-item label="日志名称：">{{ editForm.logName }}</el-form-item>
  <el-form-item label="日志类型：">
    <dict-tag v-model="editForm.logType" dict-type="sys_operation_log_type"/>
  </el-form-item>
  <el-form-item label="操作人员：">
    {{ editForm.logBy }}
  </el-form-item>
</base-row-split3>
```

### 代码高亮([base-high-light-code](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseHighLightCode.vue))

* 基础用法

```vue

<base-high-light-code v-model="item.codeContent" :language="getVmLanguage(item.vmName)"/>
```

### 图片示例

<table>
    <tbody>
        <tr>
            <td>
                <img src="assets/img/web-handbook/base-dialog-demo.png" alt="">
            </td>
            <td>
                <img src="assets/img/web-handbook/base-draw-demo.png" alt="">
            </td>            
            <td>
                <img src="assets/img/web-handbook/base-row-split3-demo.png" alt="">
            </td>
        </tr>
        <tr>
            <td>
                <img src="assets/img/web-handbook/image-preview-demo.png" alt="">
            </td>            
            <td>
                <img src="assets/img/web-handbook/table-toolbar-demo.png" alt="">
            </td>
        </tr>
    </tbody>
</table>