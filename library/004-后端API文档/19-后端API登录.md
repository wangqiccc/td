# 后端API登录
>维护人员：**侯宁洲**  
>创建时间：2019-3-24

## 获取科研成果
获取科研成果接口，主要用于后端管理与小程序端。

### 接口详情
### 请求地址
/api/Admindenglu/Adminlogin

### 请求类型
POST

### 请求参数
| 参数名 | 类型 | 必填 | 描述 | 默认值 | 参考值 |
| ----- | :---: | :---: | --- | --- | --- |
| username    | string | 是  | 用户名 | -  | admin |
| password  | string | 是 | 密码 | - | 123456 |

### 返回正确JSON示例
```javascript
{
    "code": 200,
    "msg": "登录成功",
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOjEsInVzZXJuYW1lIjoiYWRtaW4iLCJyb2xlIjowfQ.65CxTUycPIEmgundT3nY1DXAeoZdCzB0DIlj7BA8cWY",
        "username": "admin",
        "role": 0
    }
}
```
### 返回错误JSON示例
```javascript
{
    "code": 404,
    "msg": "密码错误"
}

```

### 备注说明
无

#### 修改日志
无


## 发送token

### 发送方式
| 方式 | Header Two     |
| :------------- | :------------- |
| get            | xxxx.com?token=token字符串      |
| post           | `{token:'token'}`             |
| request.headers | `{'x-access-token':'token'}` |


### token验证结果
```
{
    "code": 401,
    "msg": "验证失败"
}
{
    "code": 401,
    "msg": "请传入token"
}
```

### 示例
```
// axios添加请求拦截器
instance.interceptors.request.use(config => {
	// 在发送请求之前做某事，比如说 设置token
	config.headers['x-access-token'] = 'token';
	return config;
}, error => {
	// 请求错误时做些事
	return Promise.reject(error);
});


// 添加响应拦截器
instance.interceptors.response.use(response => {
	// 对响应数据做些事
	if (response.status === 401) { //token验证失败
        //跳转至登录页
	}
	return response;
}, error => {
	return Promise.reject(error.response.data); // 返回接口返回的错误信息
})

```
