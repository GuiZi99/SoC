# 用Chisel语言在FPGA开发板实现基于RISC-V CPU的片上系统

本选题的目标是在FPGA平台上，完全用Chisel语言实现基于RISC-V CPU的SOC架构，支持串口和片外Flash等外围接口，并形成实验帮助文档。

## 工作内容

1.在重现已有工作的基础上，与人合作在FPGA开发板小脚丫CYC10上用Chisel语言设计实现一个完整的RISC-V32片上系统，支持AXI总线、SDRAM模块、Uart串口、LED模块、片外flash模块等外围模块，并通过测试用例验证功能正确性；（基本目标）
2.撰写Chisel SOC的实现帮助文档（基本目标）
3.对比Verilog和Chisel的实现的性能和开销特征；
4.实现rCore教学操作系统中的Flash模块驱动；（可选目标）

## 相关工作

1.Chisel实现SOC以及操作系统移植帮助文档
2.贺清-用CHisel语言实现RISV-V处理器
3.蒋周奇：RISV-V CPU上的RustSBI（源代码、文档）
4.rCore教学操作系统实验文档第三版
