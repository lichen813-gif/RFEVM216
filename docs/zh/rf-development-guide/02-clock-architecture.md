# 2.1 时钟架构

[Switch to English](../../en/rf-development-guide/02-clock-architecture.md)

## 2.1 硬件架构介绍

### 2.1.1 RFSoC 器件时钟转发特性

RFSoC 在芯片内集成了数据转换器，第三代 RFSoC 系列器件均包含 4 个
ADC Tile 和 4 个 DAC Tile，每个 ADC 和 DAC Tile 内可能包含 1 个（ZU43DR）
或 2 个（ZU47DR/48DR）或者 4 个（ZU49DR）Channel，这取决于芯片型号。
RFEVM216 开发板上使用 ZU49DR 器件，每个 ADC Tile 包含 4 路 ADC，
每个 DAC Tile 包含 4 路 DAC。
每个 Tile 都可以独立配置，工作在不同的采样时钟频率上，采样时钟可以来
自于外部高频时钟输入，可以来自与每个 Tile 内部 PLL 倍频后的时钟，也可以
来自于其他 Tile 分发的参考时钟。
第三代 RFSoC 器件相比之前几代产品引入了时钟转发特性，不在需要为每
个 Tile 都提供独立的采样时钟，节省了引脚数量，降低了外围电路的复杂度。
时钟转发的方式共分为两种，一种是参考时钟转发，一种是采样时钟转发。
所谓参考时钟转发 ， 是指外部时钟芯片提供低噪声低频时钟到一个
ADC/DAC Tile 的专用时钟管脚，该时钟管脚在 Tile 间转发，通过每个 Tile 内的
PLL 倍频出所需的采样时钟。
而采样时钟转发有两种途径，一是外部时钟芯片直接提供低噪声高频的采样
时钟到一个 ADC/DAC Tile 的专用时钟管脚，采样时钟将在 Tile 间分发，无需通
过内部 PLL 倍频，直接提供给 ADC/DAC Channel 作为采样时钟；

![RFEVM216 射频开发指南图示](../../assets/rf-development-guide/page-004-image-01.jpg)

时钟芯片提供低噪声低频时钟到一个 ADC/DAC Tile 的专用时钟管脚，该时
钟在此 Tile 内通过 PLL 倍频到采样频率，随后将此采样时钟在 Tile 间分发。
以上仅为时钟分发方式的简化解释，会有一些使用的限制和建议，建议用户
参考 PG269 Chapter 4 Clock-on-chip Clock Distribution 章节阅读。
用户也可以打开 Vivado，选择器件型号后在 RF Data Converter IP 内根据原
理图和目标设计进行配置。
下图是 RFEVM216 开发板时钟时钟结构配置：

![RFEVM216 射频开发指南图示](../../assets/rf-development-guide/page-005-image-01.jpg)

![RFEVM216 射频开发指南图示](../../assets/rf-development-guide/page-005-image-02.jpg)

### 2.1.2 RFEVM216 开发板时钟结构

这里我们仅介绍 RFEVM216 开发板与 RF 数据转换器相关的时钟部分，这部
分时钟均由 RFSOM 核心板上 LMK04828 时钟芯片提供。
LMK04828 是一个双环路抖动清除器和时钟发生器，一级回路的参考时钟输
入可为外部参考时钟；二级回路的参考输入为板上的 96MHz VCXO。其中
DAC_REFCLK 和 ADC_REFCLK 作为 RF-ADC/RF-DAC 低频参考时钟输入；
PL_CLK、PL_SYSREF 和 DAC_SYSREF 均可作为 MTS(Multi-Tile Synchronization)
应用。
RFEVM216 开发板上的芯片型号为 ZU49DR，其 4 个 ADC Tile 和 4 个 DAC

![RFEVM216 射频开发指南图示](../../assets/rf-development-guide/page-006-image-01.jpg)

![RFEVM216 射频开发指南图示](../../assets/rf-development-guide/page-006-image-02.jpg)
