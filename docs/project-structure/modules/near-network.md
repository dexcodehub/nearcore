# near-network（P2P 网络层）

## 概述
`near-network` 提供对等网络通信、路由与会话管理，负责交易与区块的传播、邻居发现、网络健康与调试信息。

- 关键文件：`chain/network/src/peer_manager/peer_manager_actor.rs`（`PeerManagerActor`）、`chain/network/src/types.rs`（`PeerManagerAdapter`）。
- 框架与依赖：`protobuf`（协议定义/编码）、`tokio`（异步）、`near-o11y`（日志/指标）。

## 职责
- 管理节点与连接、维护路由与带宽控制。
- 广播交易与块，支持分片相关数据的传播。
- 提供网络调试状态（供 `near-jsonrpc`/运维工具查询）。

## 核心功能点
- Peer 管理与路由：`PeerManagerActor` 维护连接与消息分发。
- 协议编解码：通过 `protobuf` 与自定义类型进行高效传输。
- 健康监控与调试：暴露网络图、最近连接、路由、快照等信息。

## 输入/输出接口
- 输入：来自 `near-client` 的发送指令与数据、来自 RPC 的调试查询。
- 输出：交易/块传播、网络信息视图（peer 列表、路由、图）。

## 关键类/函数与调用方式
- `PeerManagerActor`：网络层核心 Actor，对上游暴露发送/查询接口。
- `PeerManagerAdapter`/Sender：供 `near-client` 与 RPC 持有，用于向网络层发起操作。