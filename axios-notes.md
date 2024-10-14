# Axios笔记

### 基本概念

Axios 是一个基于 promise 网络请求库，作用于node.js 和浏览器中。 它是 isomorphic 的(即同一套代码可以运行在浏览器和node.js中)。在服务端它使用原生 node.js http 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests。

#### 特性

- 从浏览器创建 XMLHttpRequests
- 在 node.js 创建 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 超时处理
- 查询参数序列化支持嵌套项处理
- 自动将请求体序列化为：
  - JSON (application/json)
  - Multipart / FormData (multipart/form-data)
  - URL encoded form (application/x-www-form-urlencoded)

- 将 HTML Form 转换成 JSON 进行请求
- 自动转换 JSON 数据
- 获取浏览器和 node.js 的请求进度，并提供额外的信息（速度、剩余时间）
- 为 node.js 设置带宽限制
- 兼容符合规范的 FormData 和 Blob（包括 node.js）
- 客户端支持防御 XSRF

#### 安装

- npm：`npm install axios`
- CDN：`<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`



#### 基本用例

**注意: CommonJS 用法**

为了在CommonJS中使用 `require（）` 导入时获得TypeScript类型推断（智能感知/自动完成），请使用以下方法：

```ts
const axios = require('axios').default;

// axios.<method> 能够提供自动完成和参数类型推断功能
```

##### 用例

- 执行 `GET` 请求

  ```js
  const axios = require('axios')
  // 为给定 ID 的 user 创建请求
  axios.get('/user?ID=12345')
    .then(function (response) {
      // 处理成功情况
      console.log(response);
    })
    .catch(function (error) {
      // 处理错误情况
      console.log(error);
    })
    .finally(function(){
      // 总是会执行  
    });
  
  // 上述请求也可以按以下方式完成（可选）
  axios.get('/user', {
      params: {
        ID: 12345
      }
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    })
    .finally(function(){
      // 总是会执行  
    });
  
  // 支持async/await用法
  async function getUser() {
    try {
      const response = await axios.get('/user?ID=12345');
      console.log(response);
    } catch (error) {
      console.error(error);
    }
  }
  ```

  > **注意:** 由于`async/await` 是ECMAScript 2017中的一部分，而且在IE和一些旧的浏览器中不支持，所以使用时务必要小心。

#### POST 请求

- 执行 `POST` 请求

  ```js
  axios.post('/user', {
      firstName: 'Fred',
      lastName: 'Flintstone'
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
  ```

- 执行多个并发请求

  ```js
  function getUserAccount() {
    return axios.get('/user/12345');
  }
  
  function getUserPermissions() {
    return axios.get('/user/12345/permissions');
  }
  
  const [acct, perm] = await Promise.all([getUserAccount(), getUserPermissions()]);
  // OR
  
  Promise.all([getUserAccount(), getUserPermissions()])
    .then((function (acct, perms) {
      // 两个请求现在都执行完成
    }));
  ```

- 将 HTML Form 转换成 JSON 进行请求

  ```js
  const {data} = await axios.post('/user', document.querySelector('#my-form'), {
    headers: {
      'Content-Type': 'application/json'
    }
  })
  ```

- Forms

  - Multipart (`multipart/form-data`)

  ```js
  const {data} = await axios.post('https://httpbin.org/post', {
      firstName: 'Fred',
      lastName: 'Flintstone',
      orders: [1, 2, 3],
      photo: document.querySelector('#fileInput').files
    }, {
      headers: {
        'Content-Type': 'multipart/form-data'
      }
    }
  )
  ```

  - URL encoded form (`application/x-www-form-urlencoded`)

  ```js
  const {data} = await axios.post('https://httpbin.org/post', {
      firstName: 'Fred',
      lastName: 'Flintstone',
      orders: [1, 2, 3]
    }, {
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
      }
  })
  ```

  

### Axios API

#### Axios API

可以通过向 `axios` 传递相关配置来创建请求

- **axios（config）**

  ```js
  // 发送 POST 请求
  axios({
    method: 'post',
    url: '/user/12345',
    data: {
      firstName: 'Fred',
      lastName: 'Flintstone'
    }
  });
  ```

  ```js
  // 在 node.js 用GET请求获取远程图片
  axios({
    method:'get',
    url:'http://bit.ly/2mTM3nY',
    responseType:'stream'
  })
    .then(function(response) {
    response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
  });
  ```

- **axios（url[,config]）**

  ```js
  // 发送 GET 请求（默认的方法）
  axios('/user/12345');
  ```

##### 请求方法的别名

为方便起见，为所有支持的请求方法提供了别名

##### axios.request(config)

##### axios.get(url[, config])

##### axios.delete(url[, config])

##### axios.head(url[, config])

##### axios.options(url[, config])

##### axios.post(url[, data[, config]])

##### axios.put(url[, data[, config]])

##### axios.patch(url[, data[, config]])

##### axios.postForm(url[, data[, config]])

##### axios.putForm(url[, data[, config]])

##### axios.patchForm(url[, data[, config]])

> 注意：在使用别名方法时， `url`、`method`、`data` 这些属性都不必在配置中指定。

#### Axios 实例

可以使用自定义配置新建一个 axios 实例

##### axios.create([config])

```js
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: { 'Content-Type': 'application/json',}
});
```

##### 实例方法

以下是可用的实例方法。指定的配置将与实例的配置合并。

##### axios#request(config)

##### axios#get(url[, config])

##### axios#delete(url[, config])

##### axios#head(url[, config])

##### axios#options(url[, config])

##### axios#post(url[, data[, config]])

##### axios#put(url[, data[, config]])

##### axios#patch(url[, data[, config]])

##### axios#getUri([config])

#### 请求配置

这些是创建请求时可以用的配置选项。只有 url 是必需的。如果没有指定 method，请求将默认使用 GET 方法。

```js
{
  // `url` 是用于请求的服务器 URL
  url: '/user',

  // `method` 是创建请求时使用的方法
  method: 'get', // 默认值

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'backend.base.url',

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 它只能用于 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 数组中最后一个函数必须返回一个字符串， 一个Buffer实例，ArrayBuffer，FormData，或 Stream
  // 你可以修改请求头。
  transformRequest: [function (data, headers) {
    // 对发送的 data 进行任意转换处理

    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对接收的 data 进行任意转换处理

    return data;
  }],

  // 自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` 是与请求一起发送的 URL 参数
  // 必须是一个简单对象或 URLSearchParams 对象
  params: {
    ID: 12345
  },

  // `paramsSerializer`是可选方法，主要用于序列化`params`
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function (params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求体被发送的数据
  // 仅适用 'PUT', 'POST', 'DELETE 和 'PATCH' 请求方法
  // 在没有设置 `transformRequest` 时，则必须是以下类型之一:
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属: FormData, File, Blob
  // - Node 专属: Stream, Buffer
  data: {
    firstName: 'Fred'
  },
  
  // 发送请求体数据的可选语法
  // 请求方式 post
  // 只有 value 会被发送，key 则不会
  data: 'Country=Brasil&City=Belo Horizonte',

  // `timeout` 指定请求超时的毫秒数。
  // 如果请求时间超过 `timeout` 的值，则请求会被中断
  timeout: 1000, // 默认值是 `0` (永不超时)

  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default

  // `adapter` 允许自定义处理请求，这使测试更加容易。
  // 返回一个 promise 并提供一个有效的响应 （参见 lib/adapters/README.md）。
  adapter: function (config) {
    /* ... */
  },

  // `auth` HTTP Basic Auth
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // `responseType` 表示浏览器将要响应的数据类型
  // 选项包括: 'arraybuffer', 'document', 'json', 'text', 'stream'
  // 浏览器专属：'blob'
  responseType: 'json', // 默认值

  // `responseEncoding` 表示用于解码响应的编码 (Node.js 专属)
  // 注意：忽略 `responseType` 的值为 'stream'，或者是客户端请求
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // 默认值

  // `xsrfCookieName` 是 xsrf token 的值，被用作 cookie 的名称
  xsrfCookieName: 'XSRF-TOKEN', // 默认值

  // `xsrfHeaderName` 是带有 xsrf token 值的http 请求头名称
  xsrfHeaderName: 'X-XSRF-TOKEN', // 默认值

  // `onUploadProgress` 允许为上传处理进度事件
  // 浏览器专属
  onUploadProgress: function (progressEvent) {
    // 处理原生进度事件
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  // 浏览器专属
  onDownloadProgress: function (progressEvent) {
    // 处理原生进度事件
  },

  // `maxContentLength` 定义了node.js中允许的HTTP响应内容的最大字节数
  maxContentLength: 2000,

  // `maxBodyLength`（仅Node）定义允许的http请求内容的最大字节数
  maxBodyLength: 2000,

  // `validateStatus` 定义了对于给定的 HTTP状态码是 resolve 还是 reject promise。
  // 如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，
  // 则promise 将会 resolved，否则是 rejected。
  validateStatus: function (status) {
    return status >= 200 && status < 300; // 默认值
  },

  // `maxRedirects` 定义了在node.js中要遵循的最大重定向数。
  // 如果设置为0，则不会进行重定向
  maxRedirects: 5, // 默认值

  // `socketPath` 定义了在node.js中使用的UNIX套接字。
  // e.g. '/var/run/docker.sock' 发送请求到 docker 守护进程。
  // 只能指定 `socketPath` 或 `proxy` 。
  // 若都指定，这使用 `socketPath` 。
  socketPath: null, // default

  // `httpAgent` and `httpsAgent` define a custom agent to be used when performing http
  // and https requests, respectively, in node.js. This allows options to be added like
  // `keepAlive` that are not enabled by default.
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // `proxy` 定义了代理服务器的主机名，端口和协议。
  // 您可以使用常规的`http_proxy` 和 `https_proxy` 环境变量。
  // 使用 `false` 可以禁用代理功能，同时环境变量也会被忽略。
  // `auth`表示应使用HTTP Basic auth连接到代理，并且提供凭据。
  // 这将设置一个 `Proxy-Authorization` 请求头，它会覆盖 `headers` 中已存在的自定义 `Proxy-Authorization` 请求头。
  // 如果代理服务器使用 HTTPS，则必须设置 protocol 为`https`
  proxy: {
    protocol: 'https',
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // see https://axios-http.com/zh/docs/cancellation
  cancelToken: new CancelToken(function (cancel) {
  }),

  // `decompress` indicates whether or not the response body should be decompressed 
  // automatically. If set to `true` will also remove the 'content-encoding' header 
  // from the responses objects of all decompressed responses
  // - Node only (XHR cannot turn off decompression)
  decompress: true // 默认值
}
```

#### 响应结构

一个请求的响应包含以下信息。

```js
{
  // `data` 由服务器提供的响应
  data: {},

  // `status` 来自服务器响应的 HTTP 状态码
  status: 200,

  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: 'OK',

  // `headers` 是服务器响应头
  // 所有的 header 名称都是小写，而且可以使用方括号语法访问
  // 例如: `response.headers['content-type']`
  headers: {},

  // `config` 是 `axios` 请求的配置信息
  config: {},

  // `request` 是生成此响应的请求
  // 在node.js中它是最后一个ClientRequest实例 (in redirects)，
  // 在浏览器中则是 XMLHttpRequest 实例
  request: {}
}
```

当使用 `then` 时，您将接收如下响应:

```js
axios.get('/user/12345')
  .then(function (response) {
    console.log(response.data);
    console.log(response.status);
    console.log(response.statusText);
    console.log(response.headers);
    console.log(response.config);
  });
```

当使用 catch，或者传递一个rejection callback作为 then 的第二个参数时，响应可以通过 error 对象被使用，正如在错误处理部分解释的那样。

#### 默认配置

您可以指定默认配置，它将作用于每个请求。

##### 全局 axios 默认值

```js
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

##### 自定义实例默认值

```js
// 创建实例时配置默认值
const instance = axios.create({
  baseURL: 'https://api.example.com'
});

// 创建实例后修改默认值
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
```

##### 配置的优先级

配置将会按优先级进行合并。它的顺序是：在lib/defaults.js中找到的库默认值，然后是实例的 defaults 属性，最后是请求的 config 参数。后面的优先级要高于前面的。下面有一个例子。

```js
// 使用库提供的默认配置创建实例
// 此时超时配置的默认值是 `0`
const instance = axios.create();

// 重写库的超时默认值
// 现在，所有使用此实例的请求都将等待2.5秒，然后才会超时
instance.defaults.timeout = 2500;

// 重写此请求的超时时间，因为该请求需要很长时间
instance.get('/longRequest', {
  timeout: 5000
});
```

#### 拦截器

在请求或响应被 then 或 catch 处理前拦截它们。

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

如果你稍后需要移除拦截器，可以这样：

```js
const myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```

可以给自定义的 axios 实例添加拦截器。

```js
const instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});
```

#### 错误处理

```js
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // 请求成功发出且服务器也响应了状态码，但状态代码超出了 2xx 的范围
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // 请求已经成功发起，但没有收到响应
      // `error.request` 在浏览器中是 XMLHttpRequest 的实例，
      // 而在node.js中是 http.ClientRequest 的实例
      console.log(error.request);
    } else {
      // 发送请求时出了点问题
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```

使用 validateStatus 配置选项，可以自定义抛出错误的 HTTP code。

```js
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // 处理状态码小于500的情况
  }
})
```

使用 `toJSON` 可以获取更多关于HTTP错误的信息。

```js
axios.get('/user/12345')
  .catch(function (error) {
    console.log(error.toJSON());
  });
```







### 个人定义封装实例

#### 通用封装

在项目的 `src` 目录下创建一个名为 `api` 的文件夹，并在其中创建一个名为 `index.js` 的文件。在这个文件中，我们将封装一个通用的请求方法，用于处理所有的 API 请求。

```js
import axios from 'axios';

// 请求实例
const instance = axios.create({
  baseURL: import.meta.env.VITE_API_URL,  // api基础地址
  timeout: 1000,  // 请求超时时间
  headers: { 'Content-Type': 'application/json; charset=utf-8', },
})
/
// 请求拦截，添加token,
// interceptors下的request属性，这个request就是请求拦截器
// use函数挂载一个回调函数，这个config就是我们的请求对象
instance.interceptors.request.use(
  (config)=>{
    const token = localStorage.getItem('token')
    if (token) {
      config.headers['Authorization'] = `JWT ${token}`
    }
    return config
  },
  (error) => {
    return Promise.reject(error)
  }
)

//响应拦截
instance.interceptors.response.use(
  (response) => {
    // 对响应数据做点什么，例如检查状态码
    if (response.status === 200) {
      return response.data;
    } else {
      throw new Error(response.statusText);
    }
  },
  (error) => {
    // 对响应错误做点什么
    return Promise.reject(error);
  }
);
// 默认暴露
export default instance;
```



#### 另一种

```js
import axios from "axios"
import { get } from 'lodash-es'

/**
 * @description 创建请求实例
 */
function createService() {
  // 创建 axios 实例
	const service = axios.create({
    baseURL: import.meta.env.VITE_API_URL,  // api基础地址
		timeout: 5000,  // 请求超时，超过请求将被取消
    // headers: 设定了默认的请求头部信息，'Content-Type'
    // 'application/json; charset=utf-8'，表示客户端请求的主体数据类型是 JSON。
		headers: {
			'Content-Type': 'application/json;charset=utf-8',
		},
	});
  // 请求拦截
  // interceptors下的 request 是请求拦截器
  // use 函数挂载一个回调函数，这个config就是我们的请求对象
  service.interceptors.request.use(
    (config) => config,
    (error) => {
      console.log(error)
      return Promise.reject(error)
    }
  );
  // 相应拦截
  service.interceptors.response.use(
    (response) => {
      // 对响应数据做点什么，例如检查状态码
      if (response.status === 200) {
        return response.data;
      } else {
        throw new Error(response.statusText)
      }
    },
    (error) => {
      // 对响应错误做点什么
      return Promise.reject(error)
    }
  )
}

/**
 * @description 创建请求方法
 * @param {Object} service axios 实例
 */

function createRequestFunction(service) {
  return function (config) {
    const configDefault = {
      headers: {
        'Content-Type': get(config, 'headers.Content-Type', 'application/json'),
      },
      timeout: 5000,
      baseURL: import.meta.env.VITE_API_URL,
      data: {}
    }
  }
}

// 用于真实网络请求的实例和请求方法
export const service = createService();
export const request = createRequestFunction(service);
```









#### 模仿别人的封装

- 安装依赖 `cnpm i axios  js-cookie qs`

- 在项目的 `src` 目录下创建一个名为 `utils` 的文件夹，并在其中创建一个名为 `storage.js` 的文件。

  ```js
  function createService() {
    // 创建 axios 实例
  	const service = axios.create({
      baseURL: import.meta.env.VITE_API_URL,  // api基础地址
  		timeout: 5000,  // 请求超时，超过请求将被取消
      // headers: 设定了默认的请求头部信息，'Content-Type'
      // 'application/json; charset=utf-8'，表示客户端请求的主体数据类型是 JSON。
  		headers: {
  			'Content-Type': 'application/json;charset=utf-8',
  		},
      //paramsSerializer: 这里设置了一个函数用于对请求的参数进行序列化。
  		paramsSerializer: {
  			serialize(params) {
  				interface paramsObj {
  					[key: string]: any;
  				}
  				let result: paramsObj = {};
  				for (const [key, value] of Object.entries(params)) {
            // 如果参数值为非空的代赋值继续，如果为空字符串，那么这个参数将会被忽略不发送。
  					if (value !== '') {
  						result[key] = value;
  					}
            // 如果参数的值是布尔类型，在发送时会被转换成 'True' 或 'False' 字符串。
  					if (typeof value === 'boolean') {
  						result[key] = value ? 'True' : 'False';
  					}
  				}
          // 调用 qs.stringify(result) 将处理后的参数对象转换为拼接在 URL 后的查询字符串。
  				return qs.stringify(result);
  			},
  		},
  	});
  }
  ```
  
- 在 `utils` 文件夹中创建一个名为 `request.js` 的文件。

  ```js
  import axios, { AxiosInstance, AxiosRequestConfig } from 'axios';
  import { ElMessage, ElMessageBox } from 'element-plus';
  import { Session } from '/@/utils/storage';
  import qs from 'qs';
  
  // 配置新建一个 axios 实例
  const service: AxiosInstance = axios.create({
  	baseURL: import.meta.env.VITE_API_URL,
  	timeout: 50000,
  	headers: { 'Content-Type': 'application/json' },
  	paramsSerializer: {
  		serialize(params) {
  			return qs.stringify(params, { allowDots: true });
  		},
  	},
  });
  
  // 添加请求拦截器
  service.interceptors.request.use(
  	(config: AxiosRequestConfig) => {
  		// 在发送请求之前做些什么 token
  		if (Session.get('token')) {
  			config.headers!['Authorization'] = `${Session.get('token')}`;
  		}
  		return config;
  	},
  	(error) => {
  		// 对请求错误做些什么
  		return Promise.reject(error);
  	}
  );
  
  // 添加响应拦截器
  service.interceptors.response.use(
  	(response) => {
  		// 对响应数据做点什么
  		const res = response.data;
  		if (res.code && res.code !== 0) {
  			// `token` 过期或者账号已在别处登录
  			if (res.code === 401 || res.code === 4001) {
  				Session.clear(); // 清除浏览器全部临时缓存
  				window.location.href = '/'; // 去登录页
  				ElMessageBox.('你已被登出，请重新登录', '提示', {})
  					.then(() => {})
  					.catch(() => {});
  			}
  			return Promise.reject(service.interceptors.response);
  		} else {
  			return response.data;
  		}
  	},
  	(error) => {
  		// 对响应错误做点什么
  		if (error.message.indexOf('timeout') != -1) {
  			ElMessage.error('网络超时');
  		} else if (error.message == 'Network Error') {
  			ElMessage.error('网络连接错误');
  		} else {
  			if (error.response.data) ElMessage.error(error.response.statusText);
  			else ElMessage.error('接口路径找不到');
  		}
  		return Promise.reject(error);
  	}
  );
  
  // 导出 axios 实例
  export default service;
  ```

  

- 在 `utils` 文件夹中创建一个名为 `service.js` 的文件。

  ```js
  import axios from 'axios';
  import { get } from 'lodash-es';
  import { ElMessage, ElMessageBox } from 'element-plus';
  import type { Action } from 'element-plus';
  
  // @ts-ignore
  import { errorLog, errorCreate } from './tools.ts';
  // import { env } from "/src/utils/util.env";
  // import { useUserStore } from "../store/modules/user";
  import { Local, Session } from '/@/utils/storage';
  import qs from 'qs';
  import { getBaseURL } from './baseUrl';
  /**
   * @description 创建请求实例
   */
  function createService() {
  	// 创建一个 axios 实例
  	const service = axios.create({
  		timeout: 20000,
  		headers: {
  			'Content-Type': 'application/json;charset=utf-8',
  		},
  		paramsSerializer: {
  			serialize(params) {
  				interface paramsObj {
  					[key: string]: any;
  				}
  				let result: paramsObj = {};
  				for (const [key, value] of Object.entries(params)) {
  					if (value !== '') {
  						result[key] = value;
  					}
  					if (typeof value === 'boolean') {
  						result[key] = value ? 'True' : 'False';
  					}
  				}
  				return qs.stringify(result);
  			},
  		},
  	});
  	// 请求拦截
  	service.interceptors.request.use(
  		(config) => config,
  		(error) => {
  			// 发送失败
  			console.log(error);
  			return Promise.reject(error);
  		}
  	);
  	// 响应拦截
  	service.interceptors.response.use(
  		(response) => {
  			if (response.config.responseType === 'blob') {
  				return response;
  			}
  			const dataAxios = response.data;
  			// 这个状态码是和后端约定的
  			const { code } = dataAxios;
  			// swagger判断
  			if (dataAxios.swagger != undefined) {
  				return dataAxios;
  			}
  			// 根据 code 进行判断
  			if (code === undefined) {
  				// 如果没有 code 代表这不是项目后端开发的接口
  				errorCreate(`非标准返回：${dataAxios}， ${response.config.url}`, false);
  				return dataAxios;
  			} else {
  				// 有 code 代表这是一个后端接口 可以进行进一步的判断
  				switch (code) {
  				case 400:
  					Local.clear();
  					Session.clear();
  					errorCreate(`${dataAxios.msg}: ${response.config.url}`);
  					window.location.reload();
  					break;
  				case 401:
  					Local.clear();
  					Session.clear();
  					dataAxios.msg = '登录认证失败，请重新登录';
  					ElMessageBox.(dataAxios.msg, '提示', {
  						confirmButtonText: 'OK',
  						callback: (action: Action) => {
  							window.location.reload();
  						},
  					});
  					errorCreate(`${dataAxios.msg}: ${response.config.url}`);
  					break;
  				case 2000:
  					// @ts-ignore
  					if (response.config.unpack === false) {
  						//如果不需要解包
  						return dataAxios;
  					}
  					return dataAxios;
  				case 4000:
  					errorCreate(`${dataAxios.msg}: ${response.config.url}`);
  					return dataAxios;
  				default:
  					// 不是正确的 code
  					errorCreate(`${dataAxios.msg}: ${response.config.url}`);
  					return dataAxios;
  				}
  			}
  		},
  		(error) => {
  			const status = get(error, 'response.status');
  			switch (status) {
  			case 400:
  				error.message = '请求错误';
  				break;
  			case 401:
  				Local.clear();
  				Session.clear();
  				error.message = '登录授权过期，请重新登录';
  				ElMessageBox.(error.message, '提示', {
  				confirmButtonText: 'OK',
  				callback: (action: Action) => {
  				window.location.reload();
  			},
  			});
  				break;
  			case 403:
  				error.message = '拒绝访问';
  				break;
  			case 404:
  				error.message = `请求地址出错： ${error.response.config.url}`;
  			break;
  			case 408:
  				error.message = '请求超时';
  			break;
  			case 500:
  				error.message = '服务器内部错误';
  			break;
  			case 501:
  				error.message = '服务未实现';
  			break;
  			case 502:
  				error.message = '网关错误';
  			break;
  			case 503:
  				error.message = '服务不可用';
  			break;
  			case 504:
  				error.message = '网关超时';
  			break;
  
  ```

  













#### 结合 Pinia 和 Axios 封装

在 Vue3 项目中结合 Pinia 和 Axios 封装统一的请求接口，可以按照以下步骤进行：

1. 安装 axios：`npm install pinia axios`

2. 在 `src` 目录下创建一个名为 `api` 的文件夹，并在其中创建一个名为 `index.js` 的文件。在这个文件中，我们将使用 Axios 来发送请求，并使用 Pinia 来管理状态。

3. 在 `api/index.js` 文件中，编写如下代码：

   ```js
   import { createStore } from 'pinia';
   import axios from 'axios';
   
   // 创建 Pinia store
   const apiStore = createStore({
     id: 'api',
     state: () => ({
       baseURL: 'https://api.example.com', // 设置基础 URL
       headers: {
         'Content-Type': 'application/json',
       },
     }),
     actions: {
       async get(url, params) {
         try {
           const response = await axios.get(this.baseURL + url, {
             params,
             headers: this.headers,
           });
           return response.data;
         } catch (error) {
           throw error;
         }
       },
       async post(url, data) {
         try {
           const response = await axios.post(this.baseURL + url, data, {
             headers: this.headers,
           });
           return response.data;
         } catch (error) {
           throw error;
         }
       },
       async put(url, data) {
         try {
           const response = await axios.put(this.baseURL + url, data, {
             headers: this.headers,
           });
           return response.data;
         } catch (error) {
           throw error;
         }
       },
       async delete(url) {
         try {
           const response = await axios.delete(this.baseURL + url, {
             headers: this.headers,
           });
           return response.data;
         } catch (error) {
           throw error;
         }
       },
     },
   });
   
   export default apiStore;
   ```

   

4. 在项目的 `main.js` 文件中，引入并使用 Pinia：

   ```js
   import { createApp } from 'vue';
   import App from './App.vue';
   import apiStore from './api';
   
   const app = createApp(App);
   app.use(apiStore);
   app.mount('#app');
   ```

   

5. 现在，你可以在 Vue3 项目中使用 `apiStore` 来发送统一格式的请求了。例如：

   ```js
   // 发送 GET 请求
   apiStore.get('/users', { page: 1, limit: 10 }).then((response) => {
     console.log(response);
   });
   
   // 发送 POST 请求
   apiStore.post('/users', { name: '张三', age: 18 }).then((response) => {
     console.log(response);
   });
   
   ```

   



#### 总结

















