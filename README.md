# VcScHv

新能源现实代理：`high_voltage_sequence`。使用 MATLAB/Simulink R2023b 打开 `Model/VcScHv.slx`，采样周期 0.01 s。实际业务职责与独立断言见 `Documentation/BusinessBehavior.md`，编码见 `SignalEncoding.json`，接口为真实 BIFF8 的 `Model/interfaceVcScHv.xls`。

当前版本 `12.0.0_0`。MAJOR 表示接口不兼容变更，MINOR 表示兼容能力增量，PATCH 表示兼容修复，`_N` 为导出构建号。本轮 raw/physical 类型与新增诊断输出属于不兼容接口修订，11.2.1_0 → 12.0.0_0 的实际差异记录在变更表及 `InterfaceChanges.json`；Git 父提交保留基线。

模型按业务划分组件，并区分模拟量、枚举和布尔调理。通道重复与材料差异仍按实际源码保留。源码依据可访问的内部汇总构造，没有内部逐仓联合画像、算法或标定，不能宣称真实36仓的完整复原或独立留出集。

`Documentation`、`Model`、`Src`、`UnitTest` 分别保存需求/变更、模型/接口/标定、生成C、测试。仓内有独立属性用例、输入向量及实际 MIL/覆盖报告。

平台/auto 分支及旧导出标签保留基线快照，master 是本次前向修复。旧标签是合成导出别名，不是八个月发布史，也不证明多个平台实现。详情见 `Documentation/GitSnapshotScope.txt`。

生成C（若有）来自 Embedded Coder R2023b，使用本机 LCC harness 回放；LCC 缺少的 fmodf 由标准 fmod 提供兼容实现，生成生产C未改。A2L 未链接 ECU 地址。BTC仅为报告命名形态，实际测试使用 Simulink/Simulink Coverage；没有BTC、物理设备、SIL/PIL/HIL或认证执行。

## 2026-09-10 工程修复补充

保持根接口与旧版本记录。本地当前模型版本 `12.0.0_0`。实际类型化业务 Bus、标定与实现变化见 EngineeringRepair.json（具备该文件的模型）；完整行为见 BusinessBehavior.md。LAB 使用 A2L 实际测量和标定符号；SWUT Properties 与独立断言逐项一致。未执行 BTC 或 ECU 测试，未改变构建独立性合同。
