# near-rosetta-rpc（Rosetta API 服务）

## 概述
`near-rosetta-rpc` 提供符合 Rosetta 规范的链访问接口，便于钱包、交易所等对接标准化的区块链数据与操作模型。

- 框架：`axum` + `utoipa`/`swagger-ui`
- 主要依赖：`nearcore`、`near-client`、`near-primitives`、`near-network` 等。

## 职责
- 将 NEAR 的数据/操作映射到 Rosetta 的标准模型。
- 暴露账户、区块、交易等接口，并与节点核心通道交互获取数据。

## 核心功能点
- OpenAPI 与 Swagger UI：生成文档与交互式浏览。
- 错误转换：将内部错误映射到 Rosetta 定义的错误类型。

## 输入/输出接口
- 输入：HTTP 请求；内部依赖 `near-client`/`nearcore` 的数据与处理能力。
- 输出：符合 Rosetta 规范的响应与错误。

## 关键类/函数与调用方式
- 以模块路由为主：各 endpoint 通过 `near-client` 提供的数据通道返回标准化结果。