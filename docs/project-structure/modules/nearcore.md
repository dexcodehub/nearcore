# nearcore（节点组装库）

## 概述
`nearcore` 负责组装并统一管理节点的核心子系统，包括链处理、网络、运行时、RPC、指标等，向上为 `neard` 提供启动与集成能力。

- 入口文件：`nearcore/src/lib.rs`
- 主要依赖：`near-client`、`near-chain`、`near-network`、`node-runtime`、`near-store`、`near-jsonrpc`、`near-rosetta-rpc` 等。

## 职责
- 初始化并连接核心模块（client、chain、network、runtime、store）。
- 管理服务生命周期与特性（`json_rpc`、`rosetta_rpc`、`sandbox`、`nightly`）。
- 暴露对外接口供 `neard` 调用（例如启停、配置与 IO trace）。

## 核心功能点
- 依赖协调：在一个统一上下文下启动网络、链、RPC。
- 性能指标：集成 `near-performance-metrics` 暴露性能与内存统计。
- IO Trace：在某些特性下记录执行路径用于分析/估算。

## 输入/输出接口
- 输入：配置、协议参数、特性开关。
- 输出：启动与管理各子系统；提供 handler/sender 给 RPC 与工具使用。

## 关键类/函数与调用方式
- 库初始化方法：组合 `near-client`、`near-network`、`near-chain` 的构造与消息通道。
- RPC 集成：在 `json_rpc` 特性下，调用 `near-jsonrpc::start_http` 启动 Axum 服务。
- Rosetta 集成：在 `rosetta_rpc` 特性下，启动对外兼容的 Rosetta 接口。