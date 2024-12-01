## 接口模块([youlan-common-api](https://gitee.com/kensenzhao/youlan-boot/tree/master/youlan-common/youlan-common-api))

> 接口模块主要为了解耦模块间的直接引用关系，接口模块只负责定义接口，具体实现交给其他模块。

## 验证码模块([youlan-common-captcha](https://gitee.com/kensenzhao/youlan-boot/tree/master/youlan-common/youlan-common-captcha))

### 图形验证码

- [参考图形验证码生成样例](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-admin/src/main/java/com/youlan/controller/system/CaptchaController.java#L39)

### 短信验证码

- [参考验证码生成样例](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-admin/src/main/java/com/youlan/controller/system/CaptchaController.java#L50)

### 工具类

- [CaptchaHelper（验证码工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-captcha/src/main/java/com/youlan/common/captcha/helper/CaptchaHelper.java)

## 核心模块(youlan-common-core)

### 配置注入

- [AsyncConfig（异步配置）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/config/AsyncConfig.java)
- [ScheduleConfig(调度配置）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/config/ScheduleConfig.java)

### 数据脱敏

[参考数据脱敏功能](/docs/java-handbook/function-sensitive.md "数据脱敏")

### 工具类

- [AspectHelper（Aop切面工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/AspectHelper.java)
- [EnumHelper（枚举工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/EnumHelper.java)
- [EnvironmentHelper（Spring环境参数工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/EnvironmentHelper.java)
- [FileHelper（文件工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/FileHelper.java)
- [ListHelper（列表集合工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/ListHelper.java)
- [MapStructHelper（MapStruct工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/MapStructHelper.java)
- [MessageHelper（国际化工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/MessageHelper.java)
- [SpElHelper（SpEl表达式工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/helper/SpElHelper.java)
- [JacksonHelper（Jackson工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/jackson/helper/JacksonHelper.java)
- [SensitiveHelper（数据脱敏工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/sensitive/helper/SensitizeHelper.java)
- [ServletHelper（Servlet工具）](https://gitee.com/kensenzhao/youlan-boot/blob/master/youlan-common/youlan-common-core/src/main/java/com/youlan/common/core/servlet/helper/ServletHelper.java)

## 加密模块(youlan-common-crypto)

[参考数据加密功能](/docs/java-handbook/function-crypto.md "数据加密")

## 数据库模块(youlan-common-db)

## Excel模块(youlan-common-excel)

## Http模块(youlan-common-http)

## Redis模块(youlan-common-redis)

## IP定位模块(youlan-common-region)

## 数据校验模块(youlan-common-validator)
