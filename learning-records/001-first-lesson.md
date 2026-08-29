# Learning Record 001

- **日期**: 2026-08-29
- **主题**: 第 1 课「celld：无共识的分布式状态层」
- **交付物**:
  - Feishu doc: https://feishu.cn/docx/OPUwdmdvaoQi98xparEciNzknwd
  - Lesson HTML: `/root/research/celld-teach/lessons/0001-celld-no-consensus-state-layer.html`
  - 速查表: `/root/research/celld-teach/reference/cheatsheet.html`
- **核心收获**:
  - 条件写所有权：对象存储 CAS = 仲裁者，不需要成员/选举协议
  - epoch 前缀 fencing：不阻止旧主写，只保证旧主写不可见
  - RPO=0 双路径：bucket proof（单节点）vs fleet proof（2+ 节点，follower fsync）
  - 2 节点分水岭：CELLD_DURABILITY=fleet，单节点退回 bucket proof 慢
  - LTX 血脉：Litestream → superfly/ltx → rustyriver → celld-ltx
  - 对比锚点：OceanBase Paxos vs 单写者+外仲裁；Mongo Atlas shard vs cell 分片
- **待确认方向**（用户回复 A/B/C/D）:
  - A. 跑起来观察 cell 状态机
  - B. 源码深潜 node_log.rs / ltx_repl.rs
  - C. 单写者复制家族横向对比（Litestream/Turso/rqlite）
  - D. 部署到真实 bucket + kill-test