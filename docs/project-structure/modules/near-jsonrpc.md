# near-jsonrpc（对外 JSON-RPC 服务）

## 概述
`near-jsonrpc` 基于 Axum 提供 HTTP 服务，对外暴露节点状态查询、账户/合约视图、交易提交等接口，并维护 OpenAPI 描述。

- 关键入口：`start_http`（`chain/jsonrpc/src/lib.rs`）
- 处理器：`JsonRpcHandler`（方法路由与 sender 调用）
- 文档：`chain/jsonrpc/README.md`、`chain/jsonrpc/openapi`

## 职责
- 对外提供稳定的 RPC 接口（非 `EXPERIMENTAL_` 方法承诺稳定）。
- 将请求转发到 `near-client` 的 view/process 通道或 `near-network` 调试接口。
- 暴露健康检查、状态页与 Prometheus 指标（按配置）。

## 核心功能点
- Axum 路由与中间件：CORS、限流、trace。
- OpenAPI 生成：`openapi` crate 生成规范描述。
- Polling 配置：对部分操作进行等待与重试（如 Sandbox Patch）。

## 输入/输出接口
- 输入：HTTP/JSON-RPC 请求；内部 sender（client/view_client/process_tx/peer_manager）。
- 输出：标准 JSON-RPC 响应、错误类型转换（`RpcFrom`/`RpcInto`）。

## 关键类/函数与调用方式
- `JsonRpcHandler`：封装 sender 并实现具体方法，如 `query`、`network_info`、`client_config`。
- `start_http(config, ..)`：启动服务并注册路由与调试/指标端点。