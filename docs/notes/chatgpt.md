### 猴子也能学会的腾讯云函数搭建 OpenAI 国内代理教程

https://github.com/Ice-Hazymoon/openai-scf-proxy
https://ai.okmiku.com/chat


### chatgpt 提示词  promot 咒语生成器
https://newzone.top/chatgpt/


### openai 代理

```js
  const express = require('express')
  const {
    createProxyMiddleware
  } = require('http-proxy-middleware');
  const app = express()
  const port = 9000

  app.use('/', createProxyMiddleware({
    target: 'https://api.openai.com',
    changeOrigin: true,
    onProxyRes: function (proxyRes, req, res) {
      proxyRes.headers['Access-Control-Allow-Origin'] = '*';
    }
  }));

  app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`)
  })
```


### Vega AI：图片创作平台
https://www.yuque.com/popponyj/aigc/iqhrspenqlxlvdgf?%23%E3%80%8AVega%20AI%EF%BC%9A%E5%9B%BE%E7%89%87%E5%88%9B%E4%BD%9C%E5%B9%B3%E5%8F%B0%E3%80%8B=


### PlaygroundAI：图片生成器
https://playgroundai.com/
