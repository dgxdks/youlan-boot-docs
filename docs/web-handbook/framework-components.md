## 按钮组件

### 新增按钮（[base-add-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseAddButton.vue)）
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/config/index.vue#L36))
```vue
  <base-add-button v-has-perm="['system:config:add']" plain @click="handleAdd" />
```

### 删除按钮（[base-remove-button](https://sadfasdf/sadfasdf/)）
* 基础用法([项目实例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/monitor/online/index.vue#L29))
```vue
<base-remove-button v-has-perm="['monitor:onlineUser:kickout']" type="text" @click="handleKickout(scope.row)">强踢</base-remove-button>
```

### 修改按钮([base-update-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseUpdateButton.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/config/index.vue#L39))
```vue
<base-update-button v-has-perm="['system:config:update']" plain :disabled="!tableSelectOne" @click="handleUpdate" />
```

### 搜索按钮([base-search-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseSearchButton.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/monitor/online/index.vue#L13))
```vue
<base-search-button @click="handleQuery" />
```

### 重置按钮([base-reset-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseResetButton.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/monitor/online/index.vue#L14))
```vue
<base-reset-button @click="handleResetQuery" />
```

### 上传按钮([base-upload-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseUploadButton.vue))
* 基础用法([项目实例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/storage/record/index.vue#L51))
```vue
<base-upload-button type="primary" plain @click="handleFileUpload">文件上传</base-upload-button>
```

### 下载按钮([base-download-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDownloadButton.vue))
* 基础使用([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/config/index.vue#L45))
```vue
<base-download-button v-has-perm="['system:config:export']" plain @click="handleExport">导出</base-download-button>
```

### 关闭按钮([base-close-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseCloseButton.vue))
* 基础使用([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/role/authUser.vue#L36))
```vue
<base-close-button plain @click="handleClose">关闭</base-close-button>
```


### 文本按钮([base-text-button](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseTextButton.vue))
* 基础使用([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/role/index.vue#L67))
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
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/role/index.vue#L58))
```vue
<base-switch v-model="scope.row.status" :disabled="$auth.isAdminRole(scope.row.id)" @change="handleStatusChange(scope.row)" />
```
### 新增按钮([base-add-button](https://sadfasdf/sadfasdf/))

* 基础使用
```vue
<base-add-button @click="handleClick"></base-add-button>
```
## 时间组件

### 日期选择([base-date-range-picker](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDateRangePicker.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/config/index.vue#L26))
```vue
<base-date-range-picker v-model="queryForm.createTimeRange" style="width: 240px" />
```

### 时间选择([base-date-time-range-picker](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDateTimeRangePicker.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/log/login/index.vue#L26))
```vue
<base-date-time-range-picker v-model="queryForm.loginTimeRange" style="width: 340px" />
```

## 图标组件

### 基础图标

### 复制内容图标([base-copy-icon](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseCopyIcon.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/tools/generator/index.vue#L122))
```vue
<base-copy-icon v-model="item.codeContent" show-message style="float:right">复制</base-copy-icon>
```

### 图标选择([base-icon-select](https://))
* 基础用法
```vue
<base-icon-select ref="iconSelect" v-model="editForm.menuIcon" />
```
### 复制按钮

### 下拉选择([base-icon-select](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseIconSelect.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/menu/index.vue#L79))
```vue
<base-icon-select ref="iconSelect" v-model="editForm.menuIcon" />
```

### 数据字典
### 单选框
### 复选框
### 字典标签

## 其他组件

### 基础弹窗([base-dialog](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDialog.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/config/index.vue#L83))
```vue
<base-dialog :title="editTitle" :open.sync="editOpen" width="600px" @confirm="handleEditSubmit" @cancel="handleEditCancel">
</base-dialog>
```

### 抽屉弹窗([base-drawer](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseDrawer.vue))
* 基础用法([项目实例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/storage/record/index.vue#L96)))
```vue
<base-drawer title="存储记录详情" :open.sync="editOpen" size="80%" wrapper-closable>
  <el-form ref="editForm" :model="editForm" label-width="100px" size="mini" label-position="left" style="padding: 10px">
    <base-row-split2>
      <el-form-item label="平台名称：" prop="platform">
        {{ editForm.platform }}
      </el-form-item>
    </base-row-split2>
  </el-form>
</base-drawer>
```

### 表单标签([base-form-label](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseFormLabel.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/system/dict/index.vue#L94))
```vue
<el-form ref="editForm" :model="editForm" :rules="editRules" label-width="100px">
  <el-form-item label="字典类型" prop="typeKey">
    <base-form-label slot="label" content="字典类型必须以字母开头，且只能为（小写字母，数字，下滑线）" label="字典类型" />
    <el-input v-model="editForm.typeKey" placeholder="请输入字典类型" />
  </el-form-item>
</el-form>
```

### 二分之一布局

### 三分之一布局

### 代码高亮([base-high-light-code](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/framework/components/BaseHighLightCode.vue))
* 基础用法([项目示例](https://gitee.com/dgxdks/youlan-boot/blob/master/youlan-web/src/views/tools/generator/index.vue#L123))
```vue
<base-high-light-code v-model="item.codeContent" :language="getVmLanguage(item.vmName)" />
```
