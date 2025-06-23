## Overview
### 目前支持的接口
官网地址 https://1captcha.vip
新用户加群联系管理赠送 1000 测试点 QQ群：717826273  ![52555d689e54fbef453e53e0021274d](https://github.com/user-attachments/assets/9c81c975-5ee3-46ea-aedc-f7606039c6c6)

接口参数与yescaptcha基本一致,如从yescaptcha迁移1captcha，将https://api.yescaptcha.com替换为 https://api.1captcha.vip 即可

| 类型 | 说明 | 消耗点数 | 运行状态 | 独享/包月 |
|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|
| [HCaptchaTaskProxyless](/zh-CN/HCaptchaTaskProxyless.md)| HCaptcha 协议接口,使用内置代理           | `7` | ✅  |  ❌ |
| HCaptchaTask                       | HCaptcha 协议接口,需传入代理             | `7` | ✅  |  ❌ |
| [RecaptchaV2TaskProxyless](/zh-CN/RecaptchaV2TaskProxyless.md)           | reCaptchaV2协议接口,使用内置代理         | `4` | ✅  |  ✅ | 
| RecaptchaV2Task                    | reCaptchaV2协议接口,需传入代理           | `4` |✅   |  ❌|    
| [TurnstileTaskProxyless](/zh-CN/TurnstileTaskProxyless.md)              | CloudflareTurnstile协议接口              | `6` |✅  |  ✅|
| [CloudFlareTask](/zh-CN/CloudFlareTask.md)                         | CloudFlare5秒盾协议接口,需要传入代理     | `7` | ✅ |   ✅|
| [RecaptchaV3TaskProxyless](/zh-CN/RecaptchaV3TaskProxyless.md)               | reCaptcha V3 协议接口,使用内置代理       | `6` |✅   |  ✅|
| [ReCaptchaV3EnterpriseTaskProxyless](/zh-CN/ReCaptchaV3EnterpriseTaskProxyless.md)    | 企业版 reCaptcha V3 协议接口,使用内置代理| `7` |✅  |  ✅|
| [ImageToTextTask](/zh-CN/ImageToTextTask.md)    | ImageToTextTask协议接口,可以识别Yandex等多类OCR图片 ![example7](https://github.com/user-attachments/assets/e0fe623c-0771-406b-87e1-3318796c7282) | `6` |✅  |  ✅ |




### 传入代理说明
 
* 使用账密认证或者无需白名单认证的代理, 格式请传 ip:port 或 usr:pwd@ip:port
* 使用粘性/会话代理(即 n 分钟内 ip 保持不变的类型)
* 注意代理使用次数, 不要固定一个代理

    
### 名词说明

* `点数`: 服务消耗的点数, `1RMB = 1,000 点` (`1RMB = 1,000 points`)
* `clientKey`: 用户令牌, 调用服务需要传入该参数, 在用户主页可以查看


# 充值点数说明:充值最高赠送60%,打造全球最低价格验证码平台

| 充值点数            | 赠送比例   | 赠送点数    |  
|:-----------------:|:-----------------:|:-----------------:| 
| `10,000` 点     | `50%` | `5000` |  
| `5,000,000` 点  | `60%` | `3,000,000` | 
 

### 返利说明

* 邀请返利: 直接邀请的用户充值时, 得充值的 `20%` 点数 
 

