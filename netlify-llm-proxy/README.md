# netlify-llm-proxy

使你能够直接访问那些在中国大陆需要代理才能够访问的 LLM api 服务

## 1. 准备文件

目录结构如下所示

```bash
 .
├──  netlify.toml
└──  empty.html
```

netlify.toml 内容为:

```toml
[[redirects]]
  from = "/google/*"
  to = "https://generativelanguage.googleapis.com/:splat"
  status = 200
  force = true

[[redirects]]
  from = "/chutes/*"
  to = "https://llm.chutes.ai/:splat"
  status = 200
  force = true

...
```

empty.html 内容为空即可

## 2. 上传文件

访问 [netlify](https://netlify.com)，注册登录后，上传文件夹，创建 Site，自定义自己喜欢的 site name

## 3. API 地址

- https://<site_name>.netlify.app/google
- https://<site_name>.netlify.app/chutes
- ...
