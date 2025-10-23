# near-client（客户端协调器）

## 概述
`near-client` 协调节点的主要业务流程：从网络接收消息、驱动链状态更新、与运行时执行交互，并向上提供视图与处理接口给 RPC 与工具。

- 关键文件：`chain/client/src/client_actor.rs`（`ClientActorInner`）
- 主要依赖：`near-chain`、`near-network`、`near-store`、`node-runtime`、`near-pool`、`near-o11y`。

## 职责
- 驱动区块生产与验证、分片协调与交易处理。
- 暴露 view/process 通道供 `near-jsonrpc` 使用（查询、交易提交）。
- 管理与网络层/存储层的交互与错误处理。

## 核心功能点
- Actor/消息通道：将网络、链、运行时通过异步消息进行解耦。
- 区块与分片：与 `near-chain`、`near-chunks` 共同完成区块/分片处理。
- 指标与日志：集成 `near-o11y`，输出 tracing 与 Prometheus 指标。

## 输入/输出接口
- 输入：来自 `near-network` 的块与交易消息；来自 RPC 的查询与交易处理请求。
- 输出：链状态更新、查询结果、节点状态视图、错误与事件日志。

## 关键类/函数与调用方式
- `ClientActorInner`：核心协调器，维护与链、网络、运行时、存储的连接。
- `ViewClient`/`Client` 发送通道：`near-jsonrpc` 通过 sender 与 client 交互完成查询与处理。