## 4-3 proxyTable : Vue 跨域-针对vue-cli3

```js
# 原理
1 跨域是浏览器禁止的，服务端并不禁止跨域
2 所以浏览器发给自己的服务端，然后由自己的服务端再转发给要跨域的服务端，做一层代理
3 vue-cli的proxyTable用的是http-proxy-middleware中间件
4 只能用于开发环境，生产环境不得行


# 步骤
// 1 在Vue文件根目录下创建vue.config.js
module.exports = {
    devServer: {
        proxy: {
            '/api': {
                target: 'http://127.0.0.1:4000',
                changeOrigin: true,
                pathRewrite: {
                    '^/api': ''
                }
            }

        }
    }
}

// 2 server.js
const express = require('express')
const app = express()
let ydx = {
    hapi: "yes"
}
app.get('/', (req, res) => res.send('Hello World!'))
app.get("/user", (req, res) => {
    res.status(200).json(ydx)
})
app.listen(4000, () => {
    console.log('Example app listening on port 4000!')
})

//3  Vue Conmponent
<template></template>
<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {};
  },
  mounted() {
    axios.get("/api/user").then((req, res) => {
      console.log(req.data);
    });
  }
};
</script>

<style>
</style>

// 4 npm run dev/serve 一定要重新打包一次，才生效（20分钟亲测）

# proxyTable 参数说明
target：接口域名
changeOrigin：开启代理
pathRewrite： /api 代替了 target的地址

```

