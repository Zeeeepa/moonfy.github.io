
[`返回首页`](../README.md)
#### 创建任务
通过 createTask方法 创建识别任务

请求节点： 
国际节点
 https://api.1captcha.vip 
 

请求地址： https://api.1captcha.vip/createTask

请求格式：POST application/json

#### 对象结构

注意：某些网站可能需要ua匹配，请直接使用我们指纹所用的ua，一般我们会跟随chrome版本进行更新

user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36

sec-ch-ua: "Google Chrome";v="137", "Not-A.Brand";v="24", "Chromium";v="137"


| 属性 | 类型 | 必须 | 说明 | 
|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|
| type              | string        | 是 | RecaptchaV3TaskProxyless   |  
| websiteURL        | string        | 是 | ReCaptchaV3 网页地址，一般固定值。   |  
| websiteKey        | string        | 是 | ReCaptchaV3 网站密钥，固定值。   |  
| pageAction        | string        | 是 | 此值必须正确，否则识别的结果无效   | 
| checkField        | string        | 否 | reload 包中 protobuf 9的新值，可进行二次验证   | 
| websiteTitle        | string        | 否 | 加载recaptcha的网站页面，使用js控制台运行“document.title”获取title ,部分网站传该值可以获得较高分数  | 
| isInvisible        | Bool       | 否 | 对于reCaptcha V3类型， 该参数一般都为true，如果用户不提供，则默认自动设置为true   | 

#### 请求示例

 
```
{
    "clientKey": "cc9c18d3e263515c2c072b36a7125eecc078xxxx",
    "task": {
        "websiteURL" : "https://antcpt.com/score_detector",
        "websiteKey" : "6LcR_okUAAAAAPYrPe-HK_0RULO1aZM15ENyM-Mf",
        "pageAction" : "homepage", // 有单独找action值的教程，看上面说明
        "websiteTitle":"Score detector for reCAPTCHA v3",
        "type" : "RecaptchaV3TaskProxyless"
    }
}
```

#### 响应示例

```
{
    "errorId": 0,
    "errorCode": "",
    "errorDescription": "",
    "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006" // 请记录此ID
}
```

#### 获取结果
使用 getTaskResult 方法获取识别结果

请求节点： 
国际节点
 https://api.1captcha.vip 
 
请求地址： https://api.1captcha.vip/getTaskResult

请求格式：POST application/json
 


```
{
    "clientKey":"cc9c18d3e263515c2c072b36a7125eecc078618f3",
    "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"
}
```
#### 响应结果

| 属性 | 类型 |  说明 | 
|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|
| errorId              | Integer        | 错误提示： 0 - 没有错误，1 - 有错误   |  
| errorCode            | string         | 错误代码   |  
| errorDescription     | string         | 错误详细描述   |  
| status               | string         | **processing** - 正在识别中，请3秒后重试。    **ready** - 识别完成，在solution参数中找到结果   |  
| solution             | Object         | 识别结果，不同类型的任务结果会有所区别。   |  
| gRecaptchaResponse   | string         | 识别结果：response值。一次性使用，有效期120s，建议在60s内使用。   |  


#### 响应示例

```
{
    "errorId": 0,
    "errorCode": null,
    "errorDescription": null,
    "solution": {
        "gRecaptchaResponse": "03AGdBq25SxXT-pmSeBXjzScW-EiocHwwpwqtk1QXlJnGnU......"，
        "cookies": {
      _GRECAPTCHA: '09ANMylNCtUe-OQKWe7FMbTxJq5RJkVt4ZzBFamXKETH0B_StVVQeGOwTxeyph_XvQ9mNw50EN_TlO9958bEtYeSQ'
    }
    },
    "status": "ready"
}
```

#### 响应说明
- 识别成功：当errorId等于0 并且status等于 ready，结果在solution里面。

- 正在识别中：当errorId等于0 并且status等于 processing，请3秒后重试。

- 出错了：当errorId 大于0，请根据errorDescription了解出错误信息
