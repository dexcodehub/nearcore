# node-runtime（执行引擎）

## 概述
`node-runtime` 提供交易与合约的执行环境，协调状态读写、Gas 计量与费用规则，并与 VM 运行器（如 Wasmtime）对接。

- 关键文件：`runtime/runtime/src/lib.rs`（`Runtime`）
- 关联模块：`near-vm-runner`（VM 调用）、`near-primitives`（类型）、`near-parameters`（参数）、`near-store`（状态存储）。

## 职责
- 执行交易与合约调用，产生状态变更与执行结果。
- 计量 Gas 与费用、记录日志与事件。
- 提供执行视图（例如合约调用返回值）。

## 核心功能点
- VM 集成：通过 `near-vm-runner` 调用实际的 Wasm 执行引擎。
- IO Trace（特性）：可在编译/运行时记录 IO 序列用于分析与估算。
- 沙盒（特性）：在测试/沙盒模式下提供状态注入与快速验证。

## 输入/输出接口
- 输入：交易、合约代码、当前状态与协议参数。
- 输出：执行结果（返回值/日志）、状态写入（`near-store`）。

## 关键类/函数与调用方式
- `Runtime`：提供对外的执行 API；由 `near-chain`/`near-client` 驱动调用。
- `near-vm-runner`：通过 features 选择具体 VM 后端并传入执行上下文。