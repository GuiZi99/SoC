#### 1．毕业设计（论文）选题的内容

用Chisel语言在FPGA开发板实现基于RISC-V CPU的片上系统



#### 2．研究方案

##### 2.1本选题的主要任务

(1)在重现已有工作的基础上，与人合作在FPGA开发板小脚丫CYC10上用Chisel语言设计实现一个完整的RISC-V32片上系统，支持AXI总线、SDRAM模块、Uart串口、LED模块、片外flash模块等外围模块，并通过测试用例验证功能正确性；
(2)撰写Chisel SOC的实现帮助文档；
(3)对比Verilog和Chisel的实现的性能和开销特征；
(4)实现rCore教学操作系统中的Flash模块驱动；



##### 2.2技术方案的分析、选择

（1）FPGA,全称Field Programmable Gate Array（现场可编程门阵列），这个“门”指的是FPGA内部芯片的主要组成部分——庞大数量的寄存器和门电路。它是一种硬件可重构的体系结构，可以满足现在对不同计算任务来定制不同硬件的技术要求。
简单地对FPGA重新编程就改变了硬件包裹，系统设计师可以轻易地改变处理器内核，甚至在硬的或软的处理器之间转换，无需修改其他系统硬件。
（2）Chisel语言是UC Berkeley开发的一种开源硬件构造语言。它是建构在Scala语言之上的领域专用语言（DSL），支持高度参数化的硬件生成器。它是一种硬件构造语言(非HLS，不是C到门级电路)，具有抽象数据类型和接口等特点。Chisel 的特点能够有效的解决现在硬件开发时间和空间花费大的问题。
（3）STEP-MAX10 是小脚丫平台基于Altera公司芯片开发的FPGA开发板。STEP-MAX10搭载的核心FPGA芯片采用了Altera公司MAX10系列下的10M08SCM153采用了DIP40封装，板卡尺寸为52mm*18mm，小巧精致，携带方便。另外，板载资源也是十分丰富，包含4路轻触按键，4路拨码开关，8路用户LED，2路RGB_LED三色灯，此外，板卡集成了下载器，一根MicroUSB数据线即可完成开发板的供电与下载。
（4）RISC-V 始于加利福尼亚大学伯克利分校，是一种全新并完全开源的精简指令集架构，具有设计简单，模块化强，工具链完整等一系列优点，同时拥有大量开源实现与流片案例，能够在开源社区得到有力支持。通过开源代码即可配置其相应软件开发过程所需的交叉编译工具链。
（5）AXI4协议是amba协议中比较新的一个协议，目前应用的也很广泛。例如在ZYNQ核的ARM与FPGA部分信息交互中就大量应用了AXI4总线协议。
（6）SDRAM模块，通过quartus的qsys直接搭建，在qsys中有SDRAM的IP核，该IP核使用的是avalon总线接口，所以在使用中还需要加入AXI4协议和AVALON总线协议的转换桥。
（7）片外flash模块，小脚丫开发板上有一个64Mbit的Flash，该Flash是QSPI Flash，QSPI是Queued SPI的简写，是Motorola公司推出的SPI接口的拓展，比SPI应用更广泛，在SPI协议的基础上，Motorola公司对其功能进行了增强，增加了队列传输机制，推出了队列串行外围接口协议（即QSPI协议）。QSPI是一种专用的通信接口，连接单、双或四（条数据线）SPI Flash存储介质。

使用该flash可以考虑分析QSPI Flash的芯片手册，把命令整理出状态机图，然后编写控制器对flash实现读写功能。

（8）Uart串口模块，是我们各类芯片最常用的一种异步通信接口，通过串口我们就可以建立起计算机和我们实验板之间的通信和控制关系。

实验中为了节约资源，Uart控制器只包含发送功能，且波特率硬件写死为115200。需要注意的是，Uart在仿真的时候需要在接收端模拟一个串口，在每个比特发送的中间时刻都进行采样，最后形成字节，然后回显在modelsim上，这样才完成仿真。

（9）帮助文档，因为之前的工作中，使用chisel的内容比较少，所以缺乏一些帮助文档，而从前人留下的文档来看，gitbook形式的帮助文档比较好实现且便于阅读，所以打算采用gitbook的方式来实现整个项目的帮助文档，包括环境搭建，语言帮助，复现帮助，实验分析等内容。

（10）性能对比，因为本项目是用chisel来完成硬件描述，和大多数项目使用verilog不一样，所以需要一个对Verilog和Chisel的实现的性能和开销特征的对比。




##### 2.3实施技术方案所需的条件

1)硬件：STEP-MAX10-小脚丫FPGA开发板
2)软件：IntelliJ IDEA、Verilator



##### 2.4存在的主要问题和技术关键

目前存在的主要问题是

（1）SDRAM的转换桥部分存在未解决的问题

（2）片外Flash模块的实现方案有限

（3）对于两种语言实现的性能和开销特征的对比不是很有概念



##### 2.5预期能够达到的研究目标

（1）实现一个完整的RISC-V32片上系统，支持AXI总线、SDRAM模块、Uart串口、LED模块、片外flash模块等外围模块

（2）实现rCore教学操作系统中的Flash模块驱动



#### 3．课题计划进度表

一月：熟悉RISC-V架构，熟悉Chisel语言，完成复现工作
二月：完成SDRAM转换桥和片外Flash控制模块的编写
三月：尝试移植操作系统，通过测试用例验证功能正确性
四月：完成帮助文档和性能对比的工作
五月：编写修订完成论文，准备答辩



#### 4．参考文献

（1) RISC-V: The Free and Open RISC Instruction Set Architecture

（2) Reusability is FIRRTL Ground:Hardware Construction Languages, Compiler Frameworks, and Transformations

（3) Lee Y, Waterman A, Cook H, et al. An Agile Approach to Building RISC-V Microprocessors[J]. IEEE Micro, 2016, 36(2): 8-20.

（4) Sharat K, Bandishte S, Varghese K, et al. A Custom Designed RISC-V ISA Compatible Processor for SoC[C]. vlsi design and test, 2017: 570-577.

（5) The RISC-V Reader: An Open Architecture Atlas David Patterson, Andrew Waterman Edition: 1st

（6) 《Chisel Tutorials (Release branch)》

（7) Chisel 3 wiki

（8) Short Users Guide to Chisel

（9) step-max10_硬件手册v1.2

（10) step-max10_nios_ii搭建教程