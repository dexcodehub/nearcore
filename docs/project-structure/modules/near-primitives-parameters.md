# near-primitives 与 near-parameters（协议类型与参数）

## 概述
`near-primitives` 提供协议层的统一类型与视图（交易、块、账户、查询结果等），`near-parameters` 定义协议参数（费用、限制、特性开关）。

## 职责
- 类型标准化：保障跨模块（链、运行时、RPC）统一的结构与序列化。
- 参数治理：集中定义参数并供各模块读取，支持 `nightly`/`test_features` 等特性。

## 核心功能点
- 序列化/反序列化：配合 `borsh`/`serde` 保障稳定的数据交换。
- Feature 控制：部分功能（如 estimator、test_utils）通过 features 暴露。

## 输入/输出接口
- 输入：无（作为依赖被引用）。
- 输出：类型定义与参数配置；供 `near-chain`、`node-runtime`、`near-jsonrpc` 引用。

## 关键类/函数与调用方式
- 类型与视图结构：被各模块直接 import 使用（如 `near_primitives::views`）。
- 参数读取：各模块通过 `near-parameters` 的 API 获取当前协议配置。