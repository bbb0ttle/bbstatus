# bbstatus

`status.lan.bbki.ng` 的状态页前端 —— 自包含单文件仪表盘，消费 Gatus API 展示各服务在线状态、延迟与可用率。

## 文件

- `index.html` — 全部 UI（HTML + CSS + fetch 轮询，无构建依赖、无外部 CDN）
- `nginx.conf` — 静态服务 + `/api/` 反代到 `gatus:8081` 的 server 块

## 部署

运行于 gift pc 的 `status-dash` 容器（`nginx:alpine`，`once` docker 网络），文件挂载自 `~/gatus/status-dash/`（该目录即本仓库的 clone）。更新流程：

```bash
cd ~/gatus/status-dash && git pull
docker compose -f ~/gatus/docker-compose.yml restart status-dash
```

数据来源：Gatus `GET /api/v1/endpoints/statuses`。探测配置见 bbinfra `infra/monitoring/gatus/`。
