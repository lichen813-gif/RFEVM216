# RFEVM216 管脚映射参考

[Switch to English](../../en/user-guide/04-pin-mapping.md)

本页将核心板与载板的信号映射整理为可检索、可复制的表格。破折号表示原手册未给出对应值。

## RFSOM216 核心板 { #som-pin-mapping }

### QSPI Flash 引脚分配

| 信号名称 | PS MIO | RFSoC 引脚号 |
| --- | --- | --- |
| SPIL_SCLK | PS_MIO0 | BB27 |
| SPIL_MO1 | PS_MIO1 | BA27 |
| SPIL_MO2 | PS_MIO2 | BB26 |
| SPIL_MO3 | PS_MIO3 | BB28 |
| SPIL_MO0 | PS_MIO4 | BA28 |
| SPIL_CS | PS_MIO5 | BA29 |
| SPIH_CS | PS_MIO7 | AY27 |
| SPIH_MO0 | PS_MIO8 | AW27 |
| SPIH_MO1 | PS_MIO9 | AW26 |
| SPIH_MO2 | PS_MIO10 | AV26 |
| SPIH_MO3 | PS_MIO11 | AW28 |
| SPIH_SCLK | PS_MIO12 | AV28 |

### eMMC 引脚分配

| 信号名称 | PS MIO | RFSoC 引脚号 |
| --- | --- | --- |
| EMMC_RST | PS_MIO23 | AM27 |
| EMMC_CLK | PS_MIO22 | AL27 |
| EMMC_CMD | PS_MIO21 | AN28 |
| EMMC_IO0 | PS_MIO13 | AU26 |
| EMMC_IO1 | PS_MIO14 | AU27 |
| EMMC_IO2 | PS_MIO15 | AT27 |
| EMMC_IO3 | PS_MIO16 | AU28 |
| EMMC_IO4 | PS_MIO17 | AT28 |
| EMMC_IO5 | PS_MIO18 | AP28 |
| EMMC_IO6 | PS_MIO19 | AR27 |
| EMMC_IO7 | PS_MIO20 | AP27 |

### EEPROM 引脚分配

| 信号名称 | PS MIO | RFSoC 引脚号 | 说明 |
| --- | --- | --- | --- |
| IIC_SCL | PS_MIO24 | AL28 | I2C 时钟信号 |
| IIC_SDA | PS_MIO25 | AM28 | I2C 数据信号 |

## RFEVM216 载板 { #carrier-pin-mapping }

### M.2 接口引脚分配

| 信号名称 | RFSoC 引脚号 | J19 引脚号 | J19 信号 |
| --- | --- | --- | --- |
| MGT_TX0_N | AH36 | 47 | PETn0 |
| MGT_TX0_P | AH35 | 49 | PETp0 |
| MGT_TX1_N | AG38 | 35 | PETn1 |
| MGT_TX1_P | AG37 | 37 | PETp1 |
| MGT_RX0_N | AJ42 | 41 | PERn0 |
| MGT_RX0_P | AJ41 | 43 | PERp0 |
| MGT_RX1_N | AH40 | 29 | PERn1 |
| MGT_RX1_P | AH39 | 31 | PERp1 |
| MGT_CLK0_N | AF35 | - | - |
| MGT_CLK0_P | AF34 | - | - |

### USB 接口引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 | 说明 |
| --- | --- | --- | --- |
| USB_TX_N | BANK505_MGT_TX2_N | AF40 | USB 3.0 数据发送负 |
| USB_TX_P | BANK505_MGT_TX2_P | AF39 | USB 3.0 数据发送正 |
| USB_RX_N | BANK505_MGT_RX2_N | AG42 | USB 3.0 数据接收负 |
| USB_RX_P | BANK505_MGT_RX2_P | AG41 | USB 3.0 数据接收正 |
| USB_DATA0 | BANK502_PS_MIO56 | N29 | USB 2.0 数据 Bit0 |
| USB_DATA1 | BANK502_PS_MIO57 | R29 | USB 2.0 数据 Bit1 |
| USB_DATA2 | BANK502_PS_MIO54 | N28 | USB 2.0 数据 Bit2 |
| USB_DATA3 | BANK502_PS_MIO59 | T30 | USB 2.0 数据 Bit3 |
| USB_DATA4 | BANK502_PS_MIO60 | U28 | USB 2.0 数据 Bit4 |
| USB_DATA5 | BANK502_PS_MIO61 | T28 | USB 2.0 数据 Bit5 |
| USB_DATA6 | BANK502_PS_MIO62 | V28 | USB 2.0 数据 Bit6 |
| USB_DATA7 | BANK502_PS_MIO63 | T29 | USB 2.0 数据 Bit7 |
| USB_STP | BANK502_PS_MIO58 | R30 | USB 2.0 停止信号 |
| USB_DIR | BANK502_PS_MIO53 | N30 | USB 2.0 数据方向信号 |
| USB_CLK | BANK502_PS_MIO52 | P28 | USB 2.0 时钟信号 |
| USB_NXT | BANK502_PS_MIO55 | P29 | USB 2.0 下一个数据信号 |
| USB_RESET_N | BANK501_PS_MIO35 | C33 | USB 2.0 复位信号 |

### 千兆以太网 PHY 引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 | U48 引脚号 | U48 信号 |
| --- | --- | --- | --- | --- |
| PHY_TX_CLK | BANK502_PS_MIO64 | U30 | 29 | GTX_CLK |
| PHY_TXD0 | BANK502_PS_MIO65 | V30 | 28 | TX_D0 |
| PHY_TXD1 | BANK502_PS_MIO66 | V29 | 27 | TX_D1 |
| PHY_TXD2 | BANK502_PS_MIO67 | W28 | 26 | TX_D2 |
| PHY_TXD3 | BANK502_PS_MIO68 | Y29 | 25 | TX_D3 |
| PHY_TX_CTRL | BANK502_PS_MIO69 | W29 | 37 | TX_CTRL |
| PHY_RX_CLK | BANK502_PS_MIO70 | AA28 | 32 | RX_CLK |
| PHY_RXD0 | BANK502_PS_MIO71 | AB28 | 33 | RX_D0 |
| PHY_RXD1 | BANK502_PS_MIO72 | AC28 | 34 | RX_D1 |
| PHY_RXD2 | BANK502_PS_MIO73 | AA29 | 35 | RX_D2 |
| PHY_RXD3 | BANK502_PS_MIO74 | Y30 | 36 | RX_D3 |
| PHY_RX_CTRL | BANK502_PS_MIO75 | AC29 | 38 | RX_CTRL |
| PHY_MDC | BANK502_PS_MIO76 | AB30 | 16 | MDC |
| PHY_MDIO | BANK502_PS_MIO77 | AA30 | 17 | MDIO |
| PS_POR_B | BANK501_PS_MIO26 | A34 | 43 | RESET_N |

### Micro SD 卡引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 | 说明 |
| --- | --- | --- | --- |
| SDIO_CLK | BANK501_PS_MIO51 | M31 | SD 时钟信号 |
| SDIO_CMD | BANK501_PS_MIO50 | M30 | SD 命令信号 |
| SDIO_DAT0 | BANK501_PS_MIO46 | J31 | SD 数据 Bit0 |
| SDIO_DAT1 | BANK501_PS_MIO47 | L32 | SD 数据 Bit1 |
| SDIO_DAT2 | BANK501_PS_MIO48 | M32 | SD 数据 Bit2 |
| SDIO_DAT3 | BANK501_PS_MIO49 | K31 | SD 数据 Bit3 |
| SDIO_DETECT | BANK501_PS_MIO45 | L30 | SD 卡检测信号 |

### DisplayPort 引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 | 说明 |
| --- | --- | --- | --- |
| GT0_DP_TX_P | PS_MGT_TX3_P | AE37 | DP 数据发送正 |
| GT0_DP_TX_N | PS_MGT_TX3_N | AE38 | DP 数据发送负 |
| PS_MGT_DP_CLK_P | PS_MGT_CLK3_P | AB34 | DP 参考时钟正 |
| PS_MGT_DP_CLK_N | PS_MGT_CLK3_N | AB35 | DP 参考时钟负 |
| DP_AUX_OUT | BANK501_PS_MIO27 | B34 | DP 辅助数据输出 |
| DP_AUX_IN | BANK501_PS_MIO30 | C34 | DP 辅助数据输入 |
| DP_OE | BANK501_PS_MIO29 | B33 | DP 辅助数据输出使能 |
| DP_HPD | BANK501_PS_MIO28 | A33 | DP 热插拔检测 |

### J12 QSFP28 引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- |
| QSFP_RX0_N | MGTYRXN0_130 | L42 |
| QSFP_RX0_P | MGTYRXP0_130 | L41 |
| QSFP_RX1_N | MGTYRXN1_130 | J42 |
| QSFP_RX1_P | MGTYRXP1_130 | J41 |
| QSFP_RX2_N | MGTYRXN2_130 | G42 |
| QSFP_RX2_P | MGTYRXP2_130 | G41 |
| QSFP_RX3_N | MGTYRXN3_130 | F40 |
| QSFP_RX3_P | MGTYRXP3_130 | F39 |
| QSFP_TX0_N | MGTYTXN0_130 | K39 |
| QSFP_TX0_P | MGTYTXP0_130 | K38 |
| QSFP_TX1_N | MGTYTXN1_130 | J37 |
| QSFP_TX1_P | MGTYTXP1_130 | J36 |
| QSFP_TX2_N | MGTYTXN2_130 | H39 |
| QSFP_TX2_P | MGTYTXP2_130 | H38 |
| QSFP_TX3_N | MGTYTXN3_130 | G37 |
| QSFP_TX3_P | MGTYTXP3_130 | G36 |

### J14 QSFP28 引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- |
| QSFP_RX0_N | MGTYRXN0_131 | E42 |
| QSFP_RX0_P | MGTYRXP0_131 | E41 |
| QSFP_RX1_N | MGTYRXN1_131 | D40 |
| QSFP_RX1_P | MGTYRXP1_131 | D39 |
| QSFP_RX2_N | MGTYRXN2_131 | C42 |
| QSFP_RX2_P | MGTYRXP2_131 | C41 |
| QSFP_RX3_N | MGTYRXN3_131 | B40 |
| QSFP_RX3_P | MGTYRXP3_131 | B39 |
| QSFP_TX0_N | MGTYTXN0_131 | F35 |
| QSFP_TX0_P | MGTYTXP0_131 | F34 |
| QSFP_TX1_N | MGTYTXN1_131 | E37 |
| QSFP_TX1_P | MGTYTXP1_131 | E36 |
| QSFP_TX2_N | MGTYTXN2_131 | C37 |
| QSFP_TX2_P | MGTYTXP2_131 | C36 |
| QSFP_TX3_N | MGTYTXN3_131 | A37 |
| QSFP_TX3_P | MGTYTXP3_131 | A36 |

### QSFP28 参考时钟分配

| Zynq 引脚名 | RFSoC 引脚号 | 时钟来源 |
| --- | --- | --- |
| MGTREFCLK0N_130 | P35 | LMK04828 的 SDCLKOUT5 输出 |
| MGTREFCLK0P_130 | P34 | LMK04828 的 SDCLKOUT5 输出 |
| MGTREFCLK1N_130 | M35 | 载板 156.25 MHz 晶振差分输出 |
| MGTREFCLK1P_130 | M34 | 载板 156.25 MHz 晶振差分输出 |
| MGTREFCLK1N_131 | H35 | 载板 156.25 MHz 晶振差分输出 |
| MGTREFCLK1P_131 | H34 | 载板 156.25 MHz 晶振差分输出 |

### J12 QSFP28 低速信号处理

| QSFP 低速信号 | 处理方式 | SFP 低速信号 | 处理方式 |
| --- | --- | --- | --- |
| SCL | 上拉 3.3 V | TX_FULT | 上拉 3.3 V |
| SDA | 上拉 3.3 V | TX_DISABLE | 接地 |
| ModSeIL | 上拉 3.3 V | RATE_SELECT0 | 上拉 3.3 V |
| ResetL | 上拉 3.3 V | RATE_SELECT1 | 上拉 3.3 V |
| ModPrsl | 上拉 3.3 V | LOS | 上拉 3.3 V |
| intL | 上拉 3.3 V | - | - |
| LPMode | 接地 | - | - |

### J14 QSFP28 低速信号处理

| QSFP 低速信号 | 处理方式 | SFP 低速信号 | 处理方式 |
| --- | --- | --- | --- |
| SCL | 上拉 3.3 V | TX_FULT | 上拉 3.3 V |
| SDA | 上拉 3.3 V | TX_DISABLE | 接地 |
| ModSeIL | 上拉 3.3 V | RATE_SELECT0 | 上拉 3.3 V |
| ResetL | 上拉 3.3 V | RATE_SELECT1 | 上拉 3.3 V |
| ModPrsl | 上拉 3.3 V | LOS | 上拉 3.3 V |
| intL | 上拉 3.3 V | - | - |
| LPMode | 接地 | - | - |

### JTAG 与 UART 引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 | 说明 |
| --- | --- | --- | --- |
| UART0_TX | BANK501_PS_MIO39 | J32 | PS UART 数据输出 |
| UART0_RX | BANK501_PS_MIO38 | G32 | PS UART 数据输入 |

### GPS 模块引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 | 模块信号 |
| --- | --- | --- | --- |
| PPS_1S_GPS | IO_L4N_AD12N_88 | L17 | TIMEPLUSE |
| TXD_GPS | BANK501_PS_MIO40 | F32 | TXD_MISO |
| RXD_GPS | BANK501_PS_MIO41 | K32 | RXD_MOSI |

### J3 板对板连接器管脚分配

| 信号名称 | J3 序号 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- | --- |
| HD_IO_C_P4 | 3 | IO_L2P_AD10P_89 | J12 |
| HD_IO_C_N4 | 5 | IO_L2N_AD10N_89 | J11 |
| HD_IO_C_P5 | 9 | IO_L11P_AD1P_89 | C10 |
| HD_IO_C_N5 | 11 | IO_L11N_AD1N_89 | B10 |
| HD_IO_C_P6 | 15 | IO_L12P_AD0P_89 | A10 |
| HD_IO_C_N6 | 17 | IO_L12N_AD0N_89 | A9 |
| HD_IO_C_P7 | 21 | IO_L7P_HDGC_AD5P_89 | E10 |
| HD_IO_C_N7 | 23 | IO_L7N_HDGC_AD5N_89 | E9 |
| HD_IO_C_P8 | 27 | IO_L12P_AD0P_89 | H11 |
| HD_IO_C_N8 | 29 | IO_L12N_AD0N_89 | G10 |
| HD_IO_C_P9 | 33 | IO_L3P_AD9P_89 | H10 |
| HD_IO_C_N9 | 35 | IO_L3N_AD9N_89 | H9 |
| HD_IO_C_P10 | 39 | IO_L9P_AD3P_89 | D9 |
| HD_IO_C_N10 | 41 | IO_L9N_AD3N_89 | C9 |
| HD_IO_C_P11 | 45 | IO_L5P_HDGC_AD7P_89 | G12 |
| HD_IO_C_N11 | 47 | IO_L5N_HDGC_AD7N_89 | G11 |

### J6 板对板连接器管脚分配

| 信号名称 | J6 序号 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- | --- |
| HD_IO_B_P0 | 3 | IO_L6P_HDGC_87 | F15 |
| HD_IO_B_N0 | 5 | IO_L6N_HDGC_87 | E14 |
| HD_IO_B_P1 | 9 | IO_L7P_HDGC_87 | C15 |
| HD_IO_B_N1 | 11 | IO_L7N_HDGC_87 | C14 |
| HD_IO_B_P2 | 15 | IO_L8P_HDGC_87 | B16 |
| HD_IO_B_N2 | 17 | IO_L8N_HDGC_87 | B15 |
| HD_IO_B_P3 | 21 | IO_L11P_AD9P_87 | A15 |
| HD_IO_B_N3 | 23 | IO_L11N_AD9N_87 | A14 |
| HD_IO_B_P4 | 27 | IO_L10P_AD10P_87 | D16 |
| HD_IO_B_N4 | 29 | IO_L10N_AD10N_87 | C16 |
| HD_IO_B_P5 | 33 | IO_L3P_AD13P_87 | D14 |
| HD_IO_B_N5 | 35 | IO_L3N_AD13N_87 | C13 |
| HD_IO_B_P6 | 39 | IO_L5P_HDGC_87 | A13 |
| HD_IO_B_N6 | 41 | IO_L5N_HDGC_87 | A12 |
| HD_IO_B_P7 | 45 | IO_L9P_AD11P_87 | E16 |
| HD_IO_B_N7 | 47 | IO_L9N_AD11N_87 | E15 |
| HD_IO_B_P8 | 4 | IO_L1P_AD15P_87 | F12 |
| HD_IO_B_N8 | 6 | IO_L1N_AD15N_87 | E12 |
| HD_IO_B_P9 | 10 | IO_L12P_AD8P_87 | F14 |
| HD_IO_B_N9 | 12 | IO_L12N_AD8N_87 | F13 |
| HD_IO_B_P10 | 16 | IO_L2P_AD14P_87 | D13 |
| HD_IO_B_N10 | 18 | IO_L2N_AD14N_87 | D12 |
| HD_IO_B_P11 | 22 | IO_L4P_AD12P_87 | B13 |
| HD_IO_B_N11 | 24 | IO_L4N_AD12N_87 | B12 |
| HD_IO_C_P0 | 28 | IO_L8P_HDGC_AD4P_89 | E11 |
| HD_IO_C_N0 | 30 | IO_L8N_HDGC_AD4N_89 | D11 |
| HD_IO_C_P1 | 34 | IO_L6P_HDGC_AD6P_89 | F10 |
| HD_IO_C_N1 | 36 | IO_L6N_HDGC_AD6N_89 | F9 |
| HD_IO_C_P2 | 40 | IO_L10P_AD2P_89 | C11 |
| HD_IO_C_N2 | 42 | IO_L10N_AD2N_89 | B11 |
| HD_IO_C_P3 | 46 | IO_L1P_AD11P_89 | K12 |
| HD_IO_C_N3 | 48 | IO_L1N_AD11N_89 | K11 |

### J9 扩展 IO 管脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- |
| HD_IO_A_P2 | IO_L9P_AD11P_88 | J14 |
| HD_IO_A_N2 | IO_L9N_AD11N_88 | J13 |
| HD_IO_A_P3 | IO_L6P_HDGC_88 | K15 |
| HD_IO_A_N3 | IO_L6N_HDGC_88 | K14 |
| HD_IO_A_P4 | IO_L10P_AD10P_88 | H13 |
| HD_IO_A_N4 | IO_L10N_AD10N_88 | G13 |
| HD_IO_A_P5 | IO_L7P_HDGC_88 | K17 |

### J10 扩展 IO 管脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- |
| HD_IO_A_P6 | IO_L5P_HDGC_88 | L15 |
| HD_IO_A_N6 | IO_L5N_HDGC_88 | L14 |
| HD_IO_A_P7 | IO_L3P_AD13P_88 | N14 |
| HD_IO_A_N7 | IO_L3N_AD13N_88 | M14 |
| HD_IO_A_P8 | IO_L2P_AD14P_88 | N15 |
| HD_IO_A_N8 | IO_L2N_AD14N_88 | M15 |
| HD_IO_A_P9 | IO_L1P_AD15P_88 | N16 |
| HD_IO_A_N9 | IO_L1N_AD15N_88 | M16 |

### J11 PS 扩展 IO 管脚分配

| 信号名称 | PS MIO | RFSoC 引脚号 |
| --- | --- | --- |
| BANK501_PS_MIO36 | PS_MIO36 | E31 |
| BANK501_PS_MIO37 | PS_MIO37 | E32 |
| BANK501_PS_MIO33 | PS_MIO33 | D32 |
| BANK501_PS_MIO44 | PS_MIO44 | K30 |
| BANK501_PS_MIO31 | PS_MIO31 | D33 |
| BANK501_PS_MIO32 | PS_MIO32 | D34 |
| BANK501_PS_MIO42 | PS_MIO42 | H31 |
| BANK501_PS_MIO43 | PS_MIO43 | G31 |

### 用户 LED 管脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- |
| LEDG0 | IO_L12P_AD8P_88 | G16 |
| LEDG1 | IO_L12N_AD8N_88 | G15 |
| LEDG2 | IO_L8P_HDGC_88 | J16 |
| LEDG3 | IO_L8N_HDGC_88 | H16 |

### MMCX 时钟与触发信号分配

| 信号名称 | 连接器 | RFSoC 引脚号 | 说明 |
| --- | --- | --- | --- |
| CLKIN2 | J27 | - | LMK04828 参考时钟输入 |
| CLKOUT | J24 | - | LMK04828 时钟输出 |
| TRIG_IN | JA33 | H15 | 触发信号输入 |
| TRIG_OUT | JA34 | H14 | 触发信号输出 |
| ADC_CLK | J25 | - | ADC_CLK_225 |
| DAC_CLK | J26 | - | DAC_CLK_229 |
| CLK_IN0 | J23 | - | LMK04828 参考时钟输入 |
| SYSREF_IN_P | J21 | - | LMK04828 参考时钟输入 |
| SYSREF_IN_N | J22 | - | LMK04828 参考时钟输入 |

### 风扇控制引脚分配

| 信号名称 | Zynq 引脚名 | RFSoC 引脚号 |
| --- | --- | --- |
| HD_IO_A_N5 | IO_L7N_HDGC_88 | K16 |
