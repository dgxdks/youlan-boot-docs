## 按钮组件

### 新增按钮（[base-add-button](https://sadfasdf/sadfasdf/)）
* 基础使用
```vue
  <base-add-button v-has-perm="['system:config:add']" plain @click="handleAdd" />
```

### 删除按钮（[base-remove-button](https://sadfasdf/sadfasdf/)）
* 基础用法
```vue
<base-remove-button v-has-perm="['system:config:remove']" type="text" @click="handleDelete(scope.row)" />
```

### 修改按钮([base-update-button]())
* 基础用法
```vue
<base-update-button v-has-perm="['system:config:update']" plain :disabled="!tableSelectOne" @click="handleUpdate" />
```

### 搜索按钮([base-search-button]())
* 基础用法
```vue
<base-search-button @click="handleQuery" />
```

### 重置按钮([base-reset-butto]())
* 基础用法
```vue
<base-reset-button @click="handleResetQuery" />
```

### 上传按钮([base-upload-button]())
* 基础用法
```vue
<base-upload-button type="primary" plain @click="handleFileUpload">文件上传</base-upload-button>
```

### 下载按钮([base-download-button](https://))
* 基础使用
```vue
<base-download-button v-has-perm="['system:dict:export']" plain @click="handleExport">导出</base-download-button>
```

### 关闭按钮([base-close-button](https://))
* 基础使用
```vue
<base-close-button plain @click="handleClose" />
```


### 文本按钮([base-text-button]())
* 基础使用
```vue
<base-text-button
    v-has-perm="['system:role:remove']"
    icon="el-icon-delete"
    color="#606266"
    @click="handleClick"
>
    文本
</base-text-button>
```

### 开关按钮([base-switch](https://))
* 基础用法
```vue
<base-switch v-model="scope.row.isDefault" @change="handleIsDefaultChange(scope.row)" />
```
=======
### 新增按钮([base-add-button](https://sadfasdf/sadfasdf/))

* 基础使用
```vue
<base-add-button @click="handleClick"></base-add-button>
```

### 删除按钮

### 修改按钮

### 搜索按钮

### 重置按钮

### 上传按钮

### 下载按钮

### 关闭按钮

### 文本按钮
>>>>>>> ebe8b27112d4aa5092d43d87a3673f7beeb80e74

### 菜单按钮

## 时间组件

### 日期选择([base-date-range-picker](https://))
* 基础用法
```vue
<base-date-range-picker v-model="queryForm.createTimeRange" style="width: 240px" />
```

### 时间选择([base-date-time-range-picker](https://))
* 基础用法
```vue
<base-date-time-range-picker v-model="queryForm.loginTimeRange" style="width: 340px" />
```

## 图标组件

### 基础图标

<<<<<<< HEAD
### 复制内容图标([base-copy-icon](https://))
* 基础用法
```vue
<base-copy-icon v-model="item.codeContent" show-message style="float:right">复制</base-copy-icon>
```

### 图标选择([base-icon-select](https://))
* 基础用法
```vue
<base-icon-select ref="iconSelect" v-model="editForm.menuIcon" />
```
=======
### 复制按钮

### 下拉选择
>>>>>>> ebe8b27112d4aa5092d43d87a3673f7beeb80e74

## 数据字典
### 单选框
### 复选框
### 下拉选择
### 字典标签

## 其他组件

<<<<<<< HEAD
### 基础弹窗([base-dialog](https://))
* 基础用法
```vue
<base-dialog :title="title" :open.sync="open" width="600px" @confirm="handleConfirm" @cancel="handleCancel">
  基础弹框
</base-dialog>
```

### 抽屉弹窗([base-drawer](https://))
* 基础用法
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

### 表单标签([base-form-label](https://))
* 基础用法
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

### 代码高亮
