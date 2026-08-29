# MISSION — 为什么学 celld

## 推断动机（2026-08-29 · 飞书无 clarify，按 user profile 推断）

用户 kejun 是**数据库行业从业者 + 产品开发**（非限于 OceanBase/前端）：
`denoland/celld` 是 Deno 官方 2025-04 开源的一个 Rust 项目（4.3k stars），核心命题
**「self-hosted, distributed Durable Objects」**——把 Cloudflare 的 Durable Objects
运行时搬到自己的机器上，用 S3/对象存储当控制平面，**不引入共识服务**。

这恰好命中 kejun 的三大关注点交集：
1. **数据库架构**：SQLite + LTX 事务格式 + WAL 复制的分布式化，无 Paxos/Raft
2. **产品开发**：celld 重新定义了“平台运行时”的成本结构（空闲 cell 近零成本）
3. **Agent 工程**：文档里明确 AI agent 是首选用例（每个 agent 一个 cell）

## 成功标准

学完后用户应能：
1. 讲清 celld 的**三条核心机制**：conditional-write 所有权、epoch fencing、RPO=0 确认规则
2. 解释 **fleet proof vs bucket proof** 两种持久化路径及为什么 2 节点是分水岭
3. 对比 celld 与**传统分布式数据库（Paxos/Raft 多副本）**的设计取舍——为什么 celld 敢不要共识
4. 知道 LTX 的血统（Litestream → rustyriver → celld-ltx）及它在复制链中的角色
5. （元层）把「对象存储条件写 = 免费的领导权仲裁」这一思想迁移到自己的系统设计

## 约束

- Alpha 项目、PR 关闭、邮件提 patch——技术出货阶段，学习以官方文档+源码为准
- 中文课程、Feishu 交付、术语「记忆/内存」按用户习惯