[`返回首页`](../README.md)

#### 创建任务
通过 createTask方法 创建识别任务

请求节点： 
国际节点
 https://api.1captcha.vip 
 

请求地址： https://api.1captcha.vip/createTask

请求格式：POST application/json
通过率不是100%，通过率只有10%~90%不等，多测试。
#### 对象结构

| 属性 | 类型 | 必须 | 说明 | 
|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|
| type              | string        | 是 | HCaptchaTaskProxyless   |  
| websiteURL        | string        | 是 | hCaptcha 网页地址，一般固定值。   |  
| websiteKey        | string        | 是 | hCaptcha 网站密钥，固定值。   |  
| userAgent         | string        | 否 | 非必须，与请求网站所用的userAgent相同，如果接口返回的值与你提交的值不同，请使用接口返回的值| 
| isInvisible       | string        | 否 | 非必须，如果遇到隐型版本的请传true值   |  
| rqdata            | string        | 否 | 非必须，discord等网站可能需要获取rqdata字段   |  

#### 请求示例

 
```
{
    "clientKey": "cc9c18d3e263515c2c072b36a7125eecc078618f",
    "task": {
        "websiteURL": "https://democaptcha.com/demo-form-eng/hcaptcha.html",
        "websiteKey": "338af34c-7bcb-4c7c-900b-acbec73d7d43",  // 这里是示例，具体的值你要去你的目标网站上找。。
        "type": "HCaptchaTaskProxyless",
        // 非必须，但如果传此值，提交的时候也需要使用这个值做为userAgent，如果接口返回的值与你提交的值不同，请使用接口返回的值
        "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36", // 与你请求网站时用的相同
        // 非必须，如果遇到隐型版本的请传true值
        "isInvisible": false,
        // 普通网站非必须，discord等网站可能需要获取rqdata字段
        "rqdata": ""
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
根据系统负载，您将在 10s 到 120s 的时间间隔内得到结果，300秒自动超时


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
| respKey              | Integer        | 部份网站需要，如果有返回此值，请一起提交 |  


#### 响应示例

```
{
    "errorId": 0,
    "errorCode": null,
    "errorDescription": null,
    "solution": {
        "gRecaptchaResponse": "3AHJ_q25SxXT-pmSeBXjzScW-EiocHwwpwqtk1QXlJnGnU......",
        // 提交的时候需要用这个值做为userAgent提交，如果返回的userAgent值与你提交的不同，请使用接口返回的值
        // 部份网站需要，如果有返回此值，请一起提交
        "respKey":"E0_eyJ0eXAiOiJKV1OiJIUzI1NiJ9.eyJkYXRhIakpRNjBXRTljVWEdoYmt5a2NqVGlGdWpsSlpmVjcza...",
    },
    "status": "ready"
}
```

#### 响应说明
- 识别成功：当errorId等于0 并且status等于 ready，结果在solution里面。

- 正在识别中：当errorId等于0 并且status等于 processing，请3秒后重试。

- 出错了：当errorId 大于0，请根据errorDescription了解出错误信息

