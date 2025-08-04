# 如何找到 reCAPTCHA 需要的各项参数

> 每个网站都不一样，如果以下方式都不能解决问题，烦请您自己多研究研究，您可以的。

## 方法一：通过浏览器控制台 Network 发送的请求获取参数

### 1. 搜索关键词 anchor

打开包含验证码的网页，按 `F12` → `Network`

**获取 websiteKey**：
- 可以在 URL 中找到，例如以下链接中 `k` 值为 `6LfW6wATAAAAAHLqO2pb8bDBahxlMxNdo9g947u9`

```
https://www.google.com/recaptcha/api2/anchor?ar=1&k=6LfW6wATAAAAAHLqO2pb8bDBahxlMxNdo9g947u9&co=aHR0cHM6Ly9yZWNhcHRjaGEtZGVtby5hcHBzcG90LmNvbTo0NDM.&hl=en&v=qljbK_DTcvY1PzbR7IG69z1r&size=normal&cb=3gteobhlohbk
```

**获取 websiteURL**：
- 这个 URL 请求中的 `referer` 值：一般就是目标网站的域名
- 示例：`referer: https://recaptcha-demo.appspot.com/`

### 2. 获取 pageAction 值

reCAPTCHA v3 需要 action 值，而且必须正确，通过网页源代码中搜索关键词 `grecaptcha`

**pageAction 值**：其中 `action: xxxxx` 就是我们要的值，例如：

```javascript
grecaptcha.ready(function() {
    grecaptcha.execute('6LdpS-gUAAAAAL3Qr2yP7rkrQjkKBVvEY_48JS5l', 
    {action: 'login'}).then(function(token) {
    });
});
```

> 如果网页中搜索不到，则可能是 js 被混淆、加密了，需要尝试其他方式：  
> 请参照这个单独的教程：[如何找 reCAPTCHA V3 的 action 值]

## 方法二：通过自动识别函数获取参数

打开出现验证码的网页，按 `F12` 键，进入 `Console`，输入自定义函数 `findRecaptchaClients()` 执行

### 自动识别函数代码：

```javascript
function findRecaptchaClients() {
  // eslint-disable-next-line camelcase
  if (typeof (___grecaptcha_cfg) !== 'undefined') {
    // eslint-disable-next-line camelcase, no-undef
    return Object.entries(___grecaptcha_cfg.clients).map(([cid, client]) => {
      const data = { id: cid, version: cid >= 10000 ? 'V3' : 'V2' };
      const objects = Object.entries(client).filter(([_, value]) => value && typeof value === 'object');

      objects.forEach(([toplevelKey, toplevel]) => {
        const found = Object.entries(toplevel).find(([_, value]) => (
          value && typeof value === 'object' && 'sitekey' in value && 'size' in value
        ));
     
        if (typeof toplevel === 'object' && toplevel instanceof HTMLElement && toplevel['tagName'] === 'DIV'){
            data.pageurl = toplevel.baseURI;
        }
        
        if (found) {
          const [sublevelKey, sublevel] = found;

          data.sitekey = sublevel.sitekey;
          const callbackKey = data.version === 'V2' ? 'callback' : 'promise-callback';
          const callback = sublevel[callbackKey];
          if (!callback) {
            data.callback = null;
            data.function = null;
          } else {
            data.function = callback;
            const keys = [cid, toplevelKey, sublevelKey, callbackKey].map((key) => `['${key}']`).join('');
            data.callback = `___grecaptcha_cfg.clients${keys}`;
          }
        }
      });
      return data;
    });
  }
  return [];
}
```

### 执行函数

在 Console 执行这个函数 `findRecaptchaClients()` 即可找到对应的信息

### 返回结果示例：

```json
[
    {
        "id": "0",
        "version": "V2",
        "sitekey": "6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_mJ-",
        "function": "onSuccess",
        "callback": "___grecaptcha_cfg.clients['0']['l']['l']['callback']",
        "pageurl": "https://www.google.com/recaptcha/api2/demo"
    }
]
```

## 操作截图示例

> 不会操作的，可以参考下面的图片说明
