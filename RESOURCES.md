# RESOURCES — celld 学习资源地图

## 主教材（官方，按优先级）

| 优先级 | 资源 | 说明 |
|---|---|---|
| P0 | [README.md](https://github.com/denoland/celld/blob/main/README.md) | 全局地图：架构、安装、容器、部署、运维 |
| P0 | [docs/guarantees.md](https://github.com/denoland/celld/blob/main/docs/guarantees.md) | 协议论证核心：bucket 要求、storage test、fencing、RPO=0 |
| P1 | [docs/README.md](https://github.com/denoland/celld/blob/main/docs/README.md)（708 行） | 开发/部署契约：cell 状态机、D1/KV/Queue、env vars |
| P1 | [docs/cloudflare-compat.md](https://github.com/denoland/celld/blob/main/docs/cloudflare-compat.md) | Workers API 兼容面 |
| P1 | [crates/ltx/README.md](https://github.com/denoland/celld/blob/main/crates/ltx/README.md) | LTX 血统与文件格式兼容说明 |
| P2 | docs/limitations.md / security.md / testing.md / telemetry.md / wasm.md | 边界、安全模型、kill-test 方法 |

## 源码锚点（crates/）

```
crates/
├── celld/    # 主守护进程（~40 文件）
│   ├── main.rs        (212K)  命令行/编排
│   ├── actor.rs       (158K)  消息循环
│   ├── ltx_repl.rs    (143K)  cell 复制
│   ├── node_log.rs    (211K)  节点日志（fleet 复制核心）
│   ├── control_plane.rs(107K) 控制平面
│   ├── ownership_store.rs (23K) 所有权记录（cas 写）
│   ├── storage.rs     (149K)  对象存储适配
│   ├── protocol.rs    (18K)   bucket 上的持久类型（deploy 契约）
│   └── replication.rs (17K)
├── logic/    # Worker 逻辑层（isolate/cron/kv/queue/sqlite/wake/pressure）
└── ltx/      # SQLite 复制库（vendored 自 rustyriver/Litestream）
```

- MyST：`crates/celld/protocol.rs` L11-44（Manifest 类型）、`guarantees.md` 全文
- 关键行号可后续深入时再 pin commit SHA

## 周边/迁移参照

- [Litestream](https://github.com/benbjohnson/litestream) — LTX 格式起源（v0.5.11/0.5.16）
- [superfly/ltx](https://github.com/superfly/ltx) — LTX v0.5.2 参考实现
- [rustyriver](https://github.com/mikenomitch/rustyriver) — Rust 重实现（celld-ltx 的直接母体）
- [Cloudflare Durable Objects 文档](https://developers.cloudflare.com/durable-objects/) — API 兼容基准
- 未认证存储列表：B2/Hetzner/DO Spaces（条件写缺失）— guarantees.md L30-33

## 一次运行即可验证

```sh
curl -fsSL https://celld.dev/install.sh | sh   # 或 docker run ghcr.io/denoland/celld
celld dev                                       # 本地一个 node + local object store，无需云桶
```