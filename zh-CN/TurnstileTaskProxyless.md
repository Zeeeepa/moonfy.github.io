#### 创建任务
通过 createTask方法 创建识别任务

请求节点： 
国际节点
 https://api.1captcha.vip 
 

请求地址： https://api.1captcha.vip/createTask

请求格式：POST application/json

#### 对象结构

| 属性 | 类型 | 必须 | 说明 | 
|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|:--------------------------------------------:|
| type              | string        | 是 | TurnstileTaskProxyless   |  
| websiteURL        | string        | 是 | 网页地址，一般固定值。   |  
| websiteKey        | string        | 是 | 网站密钥，一般固定值。   |  

#### 请求示例
  
 
```
{
    "clientKey":"cc9c18d3e263515c2c072b36a7125eecc078618f",
    "task":
    {
        "type":"TurnstileTaskProxyless",
        "websiteURL":"https://react-turnstile.vercel.app",
        "websiteKey":"1x00000000000000000000AA"
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
| token   | string         | 识别结果：response值。一次性使用，有效期120s，建议在60s内使用。   |  


#### 响应示例

```
{
    "errorId": 0,
    "errorCode": null,
    "errorDescription": null,
    "solution": {
        "token": "0.ufq5RgSVZd11DPSX1brdrxnEs28KcVlKj2ORchqxSy2q9yAW6ciq3hriXDF4x……"
    },
    "status": "ready"
}
```

#### 响应说明
- 识别成功：当errorId等于0 并且status等于 ready，结果在solution里面。

- 正在识别中：当errorId等于0 并且status等于 processing，请3秒后重试。

- 出错了：当errorId 大于0，请根据errorDescription了解出错误信息