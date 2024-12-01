## @SensitiveField

!> 当前数据脱敏功能是借助数据返回接口调用方时框架进行Jackson序列化实现的，数据在从持久化层读取后以及返回调用方之前并不是脱敏的。

### 参数说明

| 参数              | 类型            | 默认值 | 描述                                        |
|-----------------|---------------|-----|-------------------------------------------|
| type            | SensitiveType | 无   | 脱敏类型                                      |
| prefixNoMaskLen | int           | 0   | 左侧需要保留明文的长度(SensitiveType.CUSTOM_MASK时有效) |
| suffixNoMaskLen | int           | 0   | 右侧需要保留明文的长度(SensitiveType.CUSTOM_MASK时有效) |
| maskStr         | String        | *   | 自定义脱敏字符                                   |

### SensitiveType枚举

| 枚举           | 描述                  |
|--------------|---------------------|
| USER_ID      | 用户ID类型              |
| CHINESE_NAME | 中文名                 |
| ID_CARD      | 身份证号                |
| FIXED_PHONE  | 座机号                 |
| MOBILE_PHONE | 手机号                 |
| ADDRESS      | 地址                  |
| EMAIL        | 电子邮件                |
| PASSWORD     | 密码                  |
| CAR_LICENSE  | 中国大陆车牌，包含普通车辆、新能源车辆 |
| BANK_CARD    | 银行卡                 |
| IPV4         | IPv4地址              |
| IPV6         | IPv6地址              |
| FIRST_ONLY   | 只显示第一个字符            |
| CUSTOM_MASK  | 自定义脱敏               |

### 使用示例

```java

@Data
public class SensitiveClass {

    @SensitiveField(type = SensitiveType.PHONE, prefixNoMaskLen = 3, suffixNoMaskLen = 4, maskStr = "*")
    private String phone;

    @SensitiveField(type = SensitiveType.CHINESE_NAME)
    private String name;
}
```