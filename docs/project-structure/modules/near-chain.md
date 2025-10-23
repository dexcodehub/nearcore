# near-chain（链与区块处理）

## 概述
`near-chain` 实现区块验证与生产、链状态管理、重组/回滚、快照等核心链逻辑。

- 关键文件：`chain/chain/src/chain.rs`（`Chain`）
- 主要依赖：`near-primitives`、`near-store`、`node-runtime`、`near-epoch-manager`、`near-network`、`near-o11y`。

## 职责
- 处理入站区块/分片数据，验证并应用到链状态。
- 管理链的分叉与最终性、执行回滚与重组。
- 与运行时协作执行交易与合约逻辑。

## 核心功能点
- 最终性与重组：维护最佳链与分叉处理。
- 状态证明与校验：生成/验证状态证明。
- 与运行时耦合：通过 `node-runtime` 执行状态变更。

## 输入/输出接口
- 输入：来自网络与交易池的区块/分片与交易；纪元信息与协议参数。
- 输出：链状态更新、区块事件、最终性信息、快照与校验结果。

## 关键类/函数与调用方式
- `Chain`：对外提供区块/状态处理的 API；供 `near-client` 驱动调用。
- 与网络/存储接口：通过 `near-network` 获取数据、`near-store` 读写状态。