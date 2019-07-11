# 原理
JSONP 的原理很简单，就是利用 <script> 标签没有跨域限制的漏洞。通过 <script> 标签指向一个需要访问的地址并提供一个回调函数来接收数据当需要通讯时。

# 优势：兼容性好

# get限制
JSONP 使用简单且兼容性不错，但是只限于 get 请求。
### 4-1-1 Express +JSONP 模拟

```js
# --------------------server.js		端口3000
const express = require('express')
const app = express()
let user = {
    yrf: "haha",
    ydx: "hapi"
}
app.get('/', (req, res) => res.send('Hello World!'))
app.get("/user", (req, res) => {
    res.jsonp(user)
})
app.listen(3000, () => console.log('Example app listening on port 3000!'))


# ---------------client.html		端口8000
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>AJAX-跨域</title>
</head>
<body>
    <div id="haha">test</div>
    <script>
        let haha = document.getElementById("haha")
        function foo(data) {
            console.log(data);
             haha.innerHTML = data.ydx
        }
    </script>
# 注意 有顺序！
    <script src="http://127.0.0.1:3000/user?callback=foo"></script>
</body>
</html>

```
