!> 版本不断迭代，文档内容可能会与项目最新代码有出入，文档仅做参考，请以最新项目为准！

## 默认配置

> 在youlan-tools模块resources目录下的tools.yml,可以自己根据实际情况调整默认配置。

```yaml
youlan:
  tools:
    generator:
      # 包路径
      package-name: com.youlan.system
      # 默认是否生成DTO
      need-entity-dto: true
      # 默认是否生成PageDTO
      need-entity-page-dto: true
      # 默认是否生成VO
      need-entity-vo: true
      # 表描述转功能名称替换正则
      table-feature-regex: "(表)"
      # 是否去除表前缀
      table-remove-prefix: true
      # 表前缀匹配项
      table-match-prefix:
        - t_
      # 排除参与代码生成的数据库表
      table-exclude:
        - t_tools_generator_column
        - t_tools_generator_table
      #编辑时要排除的列字段
      editColumnExclude:
        - sts
        - create_time
        - create_by
      #查询时要排除的列字段
      queryColumnExclude:
        - id
        - sts
      #显示时要排除的列字段
      viewColumnExclude:
        - sts
```

## 单表结构

* 新建数据库表结构（单表）

```sql
drop table if exists sys_student;
create table sys_student
(
    student_id       int(11) auto_increment comment '编号',
    student_name     varchar(30) default '' comment '学生名称',
    student_age      int(3) default null comment '年龄',
    student_hobby    varchar(30) default '' comment '爱好（0代码 1音乐 2电影）',
    student_sex      char(1)     default '0' comment '性别（0男 1女 2未知）',
    student_status   char(1)     default '0' comment '状态（0正常 1停用）',
    student_birthday datetime comment '生日',
    primary key (student_id)
) engine=innodb auto_increment=1 comment = '学生信息表';
```

## 树表结构

* 新建数据库表结构（树表）

```sql
drop table if exists sys_product;
create table sys_product
(
    product_id   bigint(20) not null auto_increment comment '产品id',
    parent_id    bigint(20) default 0 comment '父产品id',
    product_name varchar(30) default '' comment '产品名称',
    order_num    int(4) default 0 comment '显示顺序',
    status       char(1)     default '0' comment '产品状态（0正常 1停用）',
    primary key (product_id)
) engine=innodb auto_increment=1 comment = '产品表';
```

## 主子表结构

* 新建数据库表结构（主子表）

```sql
-- ----------------------------
-- 客户表
-- ----------------------------
drop table if exists sys_customer;
create table sys_customer
(
    customer_id   bigint(20) not null auto_increment comment '客户id',
    customer_name varchar(30)  default '' comment '客户姓名',
    phonenumber   varchar(11)  default '' comment '手机号码',
    sex           varchar(20)  default null comment '客户性别',
    birthday      datetime comment '客户生日',
    remark        varchar(500) default null comment '客户描述',
    primary key (customer_id)
) engine=innodb auto_increment=1 comment = '客户表';


-- ----------------------------
-- 商品表
-- ----------------------------
drop table if exists sys_goods;
create table sys_goods
(
    goods_id    bigint(20) not null auto_increment comment '商品id',
    customer_id bigint(20) not null comment '客户id',
    name        varchar(30)   default '' comment '商品名称',
    weight      int(5) default null comment '商品重量',
    price       decimal(6, 2) default null comment '商品价格',
    date        datetime comment '商品时间',
    type        char(1)       default null comment '商品种类',
    primary key (goods_id)
) engine=innodb auto_increment=1 comment = '商品表';
```

## 代码生成使用

> 1、登录系统依次点击菜单（系统工具 -> 代码生成) 

<img src="assets/img/java-handbook/function-generator-menu.png" alt="">

> 2、点击代码生成页面导入按钮,选择导入记录,勾选完成后点击确定按钮

<img src="assets/img/java-handbook/function-generator-button.png" alt="">
<img src="assets/img/java-handbook/function-generator-button-choose.png" alt="">
<img src="assets/img/java-handbook/function-generator-finish.png" alt="">

> 3、点击编辑按钮,修改代码生成信息,修改完成后点击提交按钮

<img src="assets/img/java-handbook/function-generator-edit-button.png" alt="">
<img src="assets/img/java-handbook/function-generator-basic-info.png" alt="">
<img src="assets/img/java-handbook/function-generator-fields-info.png" alt="">
<img src="assets/img/java-handbook/function-generator-info.png" alt="">

> 4、点击预览按钮,确认代码生成信息

<img src="assets/img/java-handbook/function-generator-preview.png" alt="">

> 5、点击生成按钮,生成代码

<img src="assets/img/java-handbook/function-generator-download.png" alt="">
