# vecRoR
RISC-V binary translator to run RVV 1.0 program in RVV 0.7.1 machine.
# 开发背景
由于RVV 1.0是RISC-V 向量指令的第一个稳定版本，可以一定程度上提升RISC-V处理器运行软件的性能表现，并已被多数主流编译器所支持。然而，大部分RISC-V处理器仅支持RVV 0.7.1，仅有SpacemiT K1、SG 2044（玄铁C920）等少数RISC-V处理器支持RVV 1.0，并且RVV 0.7.1与RVV 1.0互不兼容，使得经过RVV 1.0优化的软件不能在不支持RVV 1.0的RISC-V处理器中运行，且软件为保证兼容性基本不开RVV 1.0优化，在图形计算等领域可能无法完全发挥处理器性能。
# 基本原理
通过二进制翻译技术在仅支持RVV 0.7.1的RISC-V处理器中用基础指令与RVV 0.7.1指令模拟RVV 1.0指令，并运行RVV 1.0优化的的二进制程序。检测该处理器是否支持H扩展，假如支持H扩展，使用H扩展加速同架构虚拟化；假如不支持，使用常规二进制翻译。

原理参照了[Box64](https://github.com/ptitSeb/box64)与[rvv-rollback](https://github.com/RISCVtestbed/rvv-rollback)，使用纯C语言编写以保证翻译效率，非RVV 1.0的指令进行直通。
