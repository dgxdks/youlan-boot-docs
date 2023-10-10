> **提示：** Vue中全局挂载对象通常会放在`src/main.js`中进行实现，为了能更好的区分，
> 对当前项目`framework/tools`下的工具挂载是在`framework/index.js`中实现的，最终在main.js进行导入实现全局挂载。开发者如需自定义挂载全局对象，
> 且自定义内容不在`framework`目录下，建议还是在`src/main.js`中实现全局挂载。

!> 版本不断迭代，文档内容可能会与项目最新代码有出入，文档仅做参考，请以最新项目为准！

## $tab对象

> **提示：** 可参照[页签工具(tab.js)](/docs/web-handbook/framework-tools.md?id=页签工具tabjs)，通过`this.$tab`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    TableUtil
} from '@/framework/tools'

Vue.prototype.$tab = TabUtil
```

## $str对象

> **提示：** 可参照[字符工具(str.js)](/docs/web-handbook/framework-tools.md?id=字符工具strjs)，通过`this.$str`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    StrUtil
} from '@/framework/tools'

Vue.prototype.$str = StrUtil
```

## $storage对象

> **提示：** 可参照[存储工具(storage.js)](/docs/web-handbook/framework-tools.md?id=存储工具storagejs)，通过`this.$storage`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    StorageUtil
} from '@/framework/tools'

Vue.prototype.$storage = StorageUtil
```

## $crypto对象

> **提示：** 可参照[加密工具(crypto.js)](/docs/web-handbook/framework-tools.md?id=加密工具cryptojs)，通过`this.$crypto`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    CryptoUtil
} from '@/framework/tools'

Vue.prototype.$crypto = CryptoUtil
```

## $url对象

> **提示：** 可参照[URL工具(url.js)](/docs/web-handbook/framework-tools.md?id=URL工具urljs)，通过`this.$url`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    UrlUtil
} from '@/framework/tools'

Vue.prototype.$url = UrlUtil
```

## $cookie对象

> **提示：** 可参照[Cookie工具(cookie.js)](/docs/web-handbook/framework-tools.md?id=Cookie工具cookiejs)，通过`this.$cookie`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    CookieUtil
} from '@/framework/tools'

Vue.prototype.$cookie = CookieUtil
```

## $auth对象

> **提示：** 可参照[权限工具(auth.js)](/docs/web-handbook/framework-tools.md?id=权限工具authjs)，通过`this.$auth`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    AuthUtil
} from '@/framework/tools'

Vue.prototype.$auth = AuthUtil
```

## $array对象

> **提示：** 可参照[数组工具(array.js)](/docs/web-handbook/framework-tools.md?id=数组工具arrayjs)，通过`this.$array`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    ArrayUtil
} from '@/framework/tools'

Vue.prototype.$array = ArrayUtil
```

## $dict对象

> **提示：** 可参照[数据字典工具(dict.js)](/docs/web-handbook/framework-tools.md?id=数据字典工具dictjs)，通过`this.$dict`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    DictUtil
} from '@/framework/tools'

Vue.prototype.$dict = DictUtil
```

## $upload对象

> **提示：** 可参照[上传工具(upload.js)](/docs/web-handbook/framework-tools.md?id=上传工具uploadjs)，通过`this.$upload`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    UploadUtil
} from '@/framework/tools'

Vue.prototype.$upload = UploadUtil
```

## $obj对象

> **提示：** 可参照[对象工具(object.js)](/docs/web-handbook/framework-tools.md?id=对象工具objectjs)，通过`this.$obj`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    ObjectUtil
} from '@/framework/tools'

Vue.prototype.$obj = ObjectUtil
```

## $validator对象

> **提示：** 可参照[表单校验工具(validator.js)](/docs/web-handbook/framework-tools.md?id=表单校验工具validatorjs)，通过`this.$validator`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    ValidatorUtil
} from '@/framework/tools'

Vue.prototype.$validator = ValidatorUtil
```

## $download对象

> **提示：** 可参照[下载工具(download.js)](/docs/web-handbook/framework-tools.md?id=下载工具downloadjs)，通过`this.$download`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    DownloadUtil
} from '@/framework/tools'

Vue.prototype.$download = DownloadUtil
```

## $modal对象

> **提示：** 可参照[模态框工具(modal.js)](/docs/web-handbook/framework-tools.md?id=模态框工具modaljs)，通过`this.$modal`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    ModalUtil
} from '@/framework/tools'

Vue.prototype.$modal = ModalUtil
```

## $date对象

> **提示：** 可参照[时间工具(date.js)](/docs/web-handbook/framework-tools.md?id=时间工具datejs)，通过`this.$date`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    DateUtil
} from '@/framework/tools'

Vue.prototype.$date = DateUtil
```

## $config对象

> **提示：** 可参照[系统参数工具(config.js)](/docs/web-handbook/framework-tools.md?id=系统参数工具configjs)，通过`this.$config`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    ConfigUtil
} from '@/framework/tools'

Vue.prototype.$config = ConfigUtil
```

## $env对象

> **提示：** 可参照[环境参数工具(env.js)](/docs/web-handbook/framework-tools.md?id=环境参数工具envjs)，通过`this.$env`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    EnvUtil
} from '@/framework/tools'

Vue.prototype.$env = EnvUtil
```

## $json对象

> **提示：** 可参照[Json工具(json.js)](/docs/web-handbook/framework-tools.md?id=Json工具jsonjs)，通过`this.$json`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    JsonUtil
} from '@/framework/tools'

Vue.prototype.$json = JsonUtil
```

## $highlight对象

> **提示：** 可参照[代码高亮工具(highlight.js)](/docs/web-handbook/framework-tools.md?id=代码高亮工具highlightjs)，通过`this.$highlight`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import {
    HighLightUtil
} from '@/framework/tools'

Vue.prototype.$highlight = HighLightUtil
```

## $tools对象

> **提示：** 可参照[全量工具包(index.js)](/docs/web-handbook/framework-tools.md?id=全量工具包indexjs)，通过`this.$tools`在Vue中进行调用

* 关键代码

```javascript
import Vue from 'vue'
import Tools from '@/framework/tools'

Vue.prototype.$tools = Tools
```