# CORS

```js
# 原理
服务端设置 Access-Control-Allow-Origin 就可以开启 CORS。 该属性表示哪些域名可以访问资源，如果设置通配符则表示所有网站都可以访问资源。

```

```js
# 栗子 Express
# server.js
const express = require('express')
const app = express()
let ydx = {
    hapi: "yes"
}
app.get('/', (req, res) => res.send('Hello World!'))
app.get("/user", (req, res) => {
    res.header('Access-Control-Allow-Origin', "*");
    // res.header('Access-Control-Allow-Origin', 'http://localhost:8888');
    res.status(200).json(ydx)
})
app.listen(3000, () => console.log('Example app listening on port 3000!'))


# client.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>AJAX-cors</title>
</head>
<body>
    <script src="./node_modules/axios/dist/axios.js"></script>
    <script>
        try {
            axios.get("http://127.0.0.1:3000/user")
                .then((result) => {
                    console.log(result.data);
                }).catch((err) => {
                    console.log(err);
                });
        } catch (error) {
            console.log(error);
        }
    </script>
</body>

</html>
```
