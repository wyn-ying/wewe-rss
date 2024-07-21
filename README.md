<div align="center">
<img src="https://raw.githubusercontent.com/cooderl/wewe-rss/main/assets/logo.png" width="80" alt="预览"/>

<h1 align="center"><a href="https://github.com/cooderl/wewe-rss">原版WeWe RSS</a></h1>

更优雅的微信公众号订阅方式。

![主界面](https://raw.githubusercontent.com/cooderl/wewe-rss/main/assets/preview1.png)

</div>

## 功能
- [x]  基于![v2.3.1](https://github.com/cooderl/wewe-rss/blob/828453b9d4ade57de42bc905fe266ba685839527/README.md)
- [x]  支持通过/feeds/filter.(json|rss|atom)接口，使用title_include和title_exclude参数对标题进行过滤
- [x]  支持通过/feeds/feedid接口，使用title_include和title_exclude参数对标题进行过滤，使用update=true实时更新feedid

## 部署

### Docker Compose 部署

可参考 [docker-compose.sqlite.yml](https://github.com/cooderl/wewe-rss/blob/main/docker-compose.sqlite.yml)

未测试 [docker-compose.yml](https://github.com/cooderl/wewe-rss/blob/main/docker-compose.yml)

### Docker 命令启动

#### Sqlite

```sh
docker run -d \
  --name wewe-rss \
  -p 4000:4000 \
  -e DATABASE_TYPE=sqlite \
  -e AUTH_CODE=123567 \
  -v $(pwd)/data:/app/data \
  wynying92/wewe-rss-sqlite:latest
```

#### Mysql

与原版相比，不支持Mysql方式

### 本地部署

未测试本地部署

## 环境变量

- `DATABASE_URL` （**必填项**）数据库地址，例如 `mysql://root:123456@127.0.0.1:3306/wewe-rss`。

- `DATABASE_TYPE` 数据库类型，使用 `sqlite` 时需要填写 `sqlite`。

- `AUTH_CODE` 服务端接口请求授权码，如果设置为空字符或不设置将不启用。(`/feeds`路径不需要)

- `SERVER_ORIGIN_URL` 服务端访问地址，用于生成RSS的完整路径（外网访问时，设置为服务器的公网 IP 或者域名地址）。

- `MAX_REQUEST_PER_MINUTE` 每分钟最大请求次数，默认 60。

- `FEED_MODE` 输出模式，可选值 `fulltext`（RSS全文模式会使接口响应会变慢，占用更多内存）。

- `CRON_EXPRESSION` 定时更新订阅源Cron表达式，默认为 `35 5,17 * * *`。

## 支持钉钉通知

进入wewe-rss-dingtalk目录按照README.md指引部署

## 使用方式

1. 进入账号管理，点击添加账号，微信扫码登录微信读书账号。
<img width="400" src="./assets/preview2.png"/>

1. 进入公众号源，点击添加，通过提交微信公众号分享链接，订阅微信公众号。
  **（添加频率过高容易被封控，等24小时解封）**
<img width="400" src="./assets/preview3.png"/>


## 账号状态说明

- 今日小黑屋 
  > 账号被封控，等一天恢复
  > 如果账号正常，可以通过重启服务/容器清除小黑屋记录

- 禁用
  > 不使用该账号

- 失效
  > 账号登录状态失效，需要重新登录

## 本地开发

1. 安装 nodejs 18 和 pnpm；
2. 修改环境变量`cp ./apps/web/.env.local.example ./apps/web/.env`和`cp ./apps/server/.env.local.example ./apps/server/.env`
3. 执行 `pnpm install && pnpm dev` 即可。⚠️ 注意：此命令仅用于本地开发，不要用于部署！
4. 前端访问 `http://localhost:5173` ，后端访问 `http://localhost:4000`

## 风险声明

为了确保本项目的持久运行，某些接口请求将通过`weread.111965.xyz`进行转发。请放心，该转发服务不会保存任何数据。

## License

[MIT](https://raw.githubusercontent.com/cooderl/wewe-rss/main/LICENSE) @cooderl
