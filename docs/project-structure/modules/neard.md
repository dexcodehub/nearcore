# neard（二进制入口）

## 概述
`neard` 是 NEAR 节点的可执行入口，负责命令行解析、配置读取、特性开关以及将 `nearcore` 组装后的各服务启动起来。

- 入口文件：`neard/src/main.rs`
- CLI 定义：`neard/src/cli.rs`
- 主要依赖：`nearcore`、`near-client`、`near-network`、`near-jsonrpc`、运维工具 crates 等。

## 职责
- 解析 CLI 与配置（支持多特性开关，如 `json_rpc`、`rosetta_rpc`、`sandbox`）。
- 初始化日志与指标（`near-o11y`）。
- 启动网络、链、RPC 等核心服务。
- 提供运维命令：如快照导出、状态查看、调试工具对接等。

## 核心功能点
- Feature 组合控制：在 `Cargo.toml` 中通过 features 启用/禁用子系统。
- 运行时参数：通过 `near-config-utils` 读取配置文件、环境参数。
- 进程资源限制：`rlimit`、jemalloc 调优。

## 输入/输出接口
- 输入：命令行参数、配置文件、环境变量。
- 输出：启动各子系统（网络、链、RPC），进程状态与日志输出。

## 关键类/函数与调用方式
- `main()`：解析 CLI 后调用 nearcore 组装服务。
- `cli.rs` 中的子命令：调用对应工具或启动路径，如 `start`, `view`, `state-parts` 等。
- 与 `nearcore` 的交互：通过库公开的初始化与启动接口进行集成。