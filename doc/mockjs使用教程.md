[TOC]

## 1. 模拟数据

getAuth.ajax.js:

```javascript
/**
 * 这个是网站登陆后获取的用户信息接口模拟数据
 * API: /ac/getAuth.ajax
 */
export default {
    "status": 200,
    "data": {
        a:11,
    }
    "error": null,
    "pageDto": null
}
```

## 2. mock配置文件

mockAPI.js:

```javascript
/**
 * 本地模拟数据
 */
import Mock from 'mockjs';
// 只有本地开发才引入Mock
// const Mock = process.env.NODE_ENV === 'development' && require('mockjs')
import auth from './getAuth.ajax.js';

if (Mock) {
  // 拦截获取用户信息API
  Mock.mock('/ac/getAuth.ajax','post', auth);
}
```

## 3. 只有在开发环境下才引入这个配置文件

process.env.NODE_ENV === 'development' && require('./mockAPI')







## 参考资料

http://mockjs.com/

https://github.com/nuysoft/Mock/wiki