# VcScHv

Synthetic新能源现实代理模型：`high_voltage_sequence`。源码为本地实现，结构依据所提供的36仓扫描汇总；不包含内部真实信号、算法、标定值或车型验证。

打开 `Model/VcScHv.slx`（MATLAB/Simulink R2023b）。模型以 0.01 s 接收明确采样接口。`Model/interfaceVcScHv.xls` 是实际 OLE/BIFF8 接口表；`Documentation` 保存需求、模型变更及可用的工程检查。

当前模型版本 `11.2.1_0`；MAJOR 表示接口不兼容变更，MINOR 表示兼容业务能力增量，PATCH 表示兼容修复，末尾 `_N` 为导出构建序号。11.1→11.2对应本地业务状态完善；这些版本不是内部历史版本。

每个信号执行范围/时效/通信状态判定、两次连续有效确认、单位转换及安全替代。模块的业务职责、动态行为、数值范围和测试范围以本仓模型及工程材料为准。

Git 平台与 auto 分支按扫描规则构造，属于合成工程工作流样例。master 为单次完整快照；标签为本轮创建的导出/验证快照，不表示八个月真实生产发布历史。平台名称不证明在对应 ECU 上执行过。

生成码（若存在）来自 Embedded Coder R2023b，目标为 Windows x86-64。A2L 未链接 ECU 地址；LAB 为实际导出符号的标签清单。测试HTML采用BTC文件命名形态，但实际执行工具是Simulink/Simulink Coverage和明确标出的host C harness，没有运行BTC工具或目标设备。
