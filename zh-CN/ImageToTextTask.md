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
| type              | string        | 是 | ImageToTextTask   |  
| body            | string        | 是 | 图片的base64编码内容（不要换行符）。   |  
| imageType       | string        | 是 | 图片种类,提供该值可以提升识别精度。  [imageType类型清单](/zh-CN/imageType.md)    |  
 

#### 请求示例

 
```
{
  clientKey: 'nrfRuRHVkUsGRDirAzSSpASFCS',
  task: {
    type: 'ImageToTextTask',
    body: '/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQH/2wBDAQEBAQEBAQEBAQEBAQEBAQE
BAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQH/wAARCABSAPgDASIAAhEBAxEB/8QAHQAAAQUBAQEBAAAAAAAAAAAACAAFBgcJBAoDAv/EADAQAAIDAQACAgICAQUAAQMFA
AMEAQIFBgcIEhMR',
    imageType:"Yandex2025" 
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
  errorId: 0,
  errorCode: null,
  errorDescription: null,
  status: 'ready',
  solution: {
    gRecaptchaResponse: 'insensibly unburden'
  }
}
```

#### 响应说明
- 识别成功：当errorId等于0 并且status等于 ready，结果在solution里面。

- 正在识别中：当errorId等于0 并且status等于 processing，请3秒后重试。

- 出错了：当errorId 大于0，请根据errorDescription了解出错误信息
