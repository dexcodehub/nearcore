# near-epoch-manager（纪元与验证者管理）

## 概述
`near-epoch-manager` 根据链状态与协议参数，管理纪元（Epoch）切换、验证者席位分配与选举，影响区块生产与分片安排。

- 关键文件：`chain/epoch-manager/src/lib.rs`（`EpochManager`、`EpochManagerHandle`）
- 主要依赖：`near-primitives`、`near-store`、`near-parameters`、`near-o11y`。

## 职责
- 计算每个纪元的验证者集合与权重。
- 维护分片分配策略与席位变更。
- 为链与客户端提供纪元相关查询。

## 核心功能点
- 纪元边界与切换：根据区块高度最终性与规则触发。
- 席位分配：基于质押与协议参数计算。
- 与链交互：提供当期/下期的验证者/分片安排。

## 输入/输出接口
- 输入：链状态、历史与参数。
- 输出：纪元信息（验证者集合、分片分配、规则）。

## 关键类/函数与调用方式
- `EpochManager`：对外暴露读写接口；供 `near-chain` 和 `near-client` 查询。