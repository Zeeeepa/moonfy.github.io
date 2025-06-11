[`返回首页`](../README.md)

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
| type              | string        | 是 | CloudFlareTask   |  
| websiteURL        | string        | 是 | 网页地址，一般固定值。   |  
| proxy             | string        | 是 |    代理地址，支持以下格式：有密码http代理：http://user:pass@45.91.239.47:62930 没有密码http代理：http://45.91.239.47:62930  没有密码的socks5代理： socks5://5.252.190.52:64585               |  


#### 请求示例
  
 
```
{
    "clientKey": "cc9c18d3e263515c2c072b36a7125eecc078618f",
    "task": {
      "type": "CloudFlareTaskS3",
      "websiteURL": "https://nowsecure.in",
      "proxy": "http://JN3wWChA:Dsg7ckfv@45.91.239.47:62930", //请用你自己的代理，这个只是演示
      "waitLoad": false, // 是否需要等待加载完成（如果你需要完整内容就写true，会增加识别时间）
      "requiredCookies": ["cf_clearance"] // 可以要求获取指定Cookies名称，可不填，不一定能获取到
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
| user_agent           | string         | 使用的ua值，请使用返回的值进行后续请求。   | 
| cookies              | Object|返回的cookies值，请使用返回的值进行后续请求，一般cloudflare5s盾的cookies包含cf_clearance值这个cookie值有一定的有效期，有的网站长达1小时所以1小时内不需要重复请求，但是也需要注意请求的频率  | 
| request_headers      | Object|请求时的headers，建议你在使用时带上这个值放到你的请求的headers中。   | 
| headers              | Object         | 请求成功后响应的headers。   | 
| content              | string         | 返回的网页内容源码。   | 


#### 响应示例

```
{
  "errorId": 0,
  "status": "ready"
  "solution": {
    "cf": true,
    "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.4 Safari/605.1.15",
    "cookies": {
      "cf_clearance": "zqKrlel6E6_SM2707VdArsu2c5.bYqLKU3DOl4tlkCE-1691687641-0-1-8d7f630c.c91f3e0f.da7e3cec-250.0.0"
    },
    "heders": {
      "accept-ch": "Sec-CH-UA-Bitness, Sec-CH-UA-Arch, Sec-CH-UA-Full-Version, Sec-CH-UA-Mobile, Sec-CH-UA-Model, Sec-CH-UA-Platform-Version, Sec-CH-UA-Full-Version-List, Sec-CH-UA-Platform, Sec-CH-UA, UA-Bitness, UA-Arch, UA-Full-Version, UA-Mobile, UA-Model, UA-Platform-Version, UA-Platform, UA",
      "server": "cloudflare",
      "vary": "Accept-Encoding",
      "x-frame-options": "SAMEORIGIN"
    },
    "request_headers": {
      ":authority": "raffle.bstn.com",
      ":method": "GET",
      ":path": "/",
      ":scheme": "https",
      "accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
      "accept-encoding": "gzip, deflate, br",
      "accept-language": "zh-CN,zh;q=0.9",
      "upgrade-insecure-requests": "1",
      "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
    },
    "content": "xxxx"
    },
}
```

#### 响应说明
- 识别成功：当errorId等于0 并且status等于 ready，结果在solution里面。

- 正在识别中：当errorId等于0 并且status等于 processing，请3秒后重试。

- 出错了：当errorId 大于0，请根据errorDescription了解出错误信息
