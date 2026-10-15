# RFEVM216 Pin Mapping Reference

[Switch to 中文](../../zh/user-guide/04-pin-mapping.md)

This page consolidates the SoM and carrier-board signal mappings into searchable, copyable tables. A dash means the source manual does not specify a value.

## RFSOM216 SoM { #som-pin-mapping }

### QSPI Flash Pin Assignment

| Signal | PS MIO | RFSoC Ball |
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

### eMMC Pin Assignment

| Signal | PS MIO | RFSoC Ball |
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

### EEPROM Pin Assignment

| Signal | PS MIO | RFSoC Ball | Description |
| --- | --- | --- | --- |
| IIC_SCL | PS_MIO24 | AL28 | I2C clock |
| IIC_SDA | PS_MIO25 | AM28 | I2C data |

## RFEVM216 Carrier Board { #carrier-pin-mapping }

### M.2 Interface Pin Assignment

| Signal | RFSoC Ball | J19 Pin | J19 Signal |
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

### USB Interface Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball | Description |
| --- | --- | --- | --- |
| USB_TX_N | BANK505_MGT_TX2_N | AF40 | USB 3.0 transmit negative |
| USB_TX_P | BANK505_MGT_TX2_P | AF39 | USB 3.0 transmit positive |
| USB_RX_N | BANK505_MGT_RX2_N | AG42 | USB 3.0 receive negative |
| USB_RX_P | BANK505_MGT_RX2_P | AG41 | USB 3.0 receive positive |
| USB_DATA0 | BANK502_PS_MIO56 | N29 | USB 2.0 data bit 0 |
| USB_DATA1 | BANK502_PS_MIO57 | R29 | USB 2.0 data bit 1 |
| USB_DATA2 | BANK502_PS_MIO54 | N28 | USB 2.0 data bit 2 |
| USB_DATA3 | BANK502_PS_MIO59 | T30 | USB 2.0 data bit 3 |
| USB_DATA4 | BANK502_PS_MIO60 | U28 | USB 2.0 data bit 4 |
| USB_DATA5 | BANK502_PS_MIO61 | T28 | USB 2.0 data bit 5 |
| USB_DATA6 | BANK502_PS_MIO62 | V28 | USB 2.0 data bit 6 |
| USB_DATA7 | BANK502_PS_MIO63 | T29 | USB 2.0 data bit 7 |
| USB_STP | BANK502_PS_MIO58 | R30 | USB 2.0 stop |
| USB_DIR | BANK502_PS_MIO53 | N30 | USB 2.0 data direction |
| USB_CLK | BANK502_PS_MIO52 | P28 | USB 2.0 clock |
| USB_NXT | BANK502_PS_MIO55 | P29 | USB 2.0 next data |
| USB_RESET_N | BANK501_PS_MIO35 | C33 | USB 2.0 reset |

### Gigabit Ethernet PHY Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball | U48 Pin | U48 Signal |
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

### Micro SD Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball | Description |
| --- | --- | --- | --- |
| SDIO_CLK | BANK501_PS_MIO51 | M31 | SD clock |
| SDIO_CMD | BANK501_PS_MIO50 | M30 | SD command |
| SDIO_DAT0 | BANK501_PS_MIO46 | J31 | SD data bit 0 |
| SDIO_DAT1 | BANK501_PS_MIO47 | L32 | SD data bit 1 |
| SDIO_DAT2 | BANK501_PS_MIO48 | M32 | SD data bit 2 |
| SDIO_DAT3 | BANK501_PS_MIO49 | K31 | SD data bit 3 |
| SDIO_DETECT | BANK501_PS_MIO45 | L30 | Card detect |

### DisplayPort Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball | Description |
| --- | --- | --- | --- |
| GT0_DP_TX_P | PS_MGT_TX3_P | AE37 | DP transmit positive |
| GT0_DP_TX_N | PS_MGT_TX3_N | AE38 | DP transmit negative |
| PS_MGT_DP_CLK_P | PS_MGT_CLK3_P | AB34 | DP reference clock positive |
| PS_MGT_DP_CLK_N | PS_MGT_CLK3_N | AB35 | DP reference clock negative |
| DP_AUX_OUT | BANK501_PS_MIO27 | B34 | DP auxiliary data output |
| DP_AUX_IN | BANK501_PS_MIO30 | C34 | DP auxiliary data input |
| DP_OE | BANK501_PS_MIO29 | B33 | DP auxiliary output enable |
| DP_HPD | BANK501_PS_MIO28 | A33 | DP hot-plug detect |

### J12 QSFP28 Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball |
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

### J14 QSFP28 Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball |
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

### QSFP28 Reference Clock Assignment

| Zynq Pin Name | RFSoC Ball | Clock Source |
| --- | --- | --- |
| MGTREFCLK0N_130 | P35 | LMK04828 SDCLKOUT5 |
| MGTREFCLK0P_130 | P34 | LMK04828 SDCLKOUT5 |
| MGTREFCLK1N_130 | M35 | Carrier-board 156.25 MHz oscillator |
| MGTREFCLK1P_130 | M34 | Carrier-board 156.25 MHz oscillator |
| MGTREFCLK1N_131 | H35 | Carrier-board 156.25 MHz oscillator |
| MGTREFCLK1P_131 | H34 | Carrier-board 156.25 MHz oscillator |

### J12 QSFP28 Low-Speed Signal Handling

| QSFP Signal | Handling | SFP Signal | Handling |
| --- | --- | --- | --- |
| SCL | 3.3 V pull-up | TX_FULT | 3.3 V pull-up |
| SDA | 3.3 V pull-up | TX_DISABLE | Ground |
| ModSeIL | 3.3 V pull-up | RATE_SELECT0 | 3.3 V pull-up |
| ResetL | 3.3 V pull-up | RATE_SELECT1 | 3.3 V pull-up |
| ModPrsl | 3.3 V pull-up | LOS | 3.3 V pull-up |
| intL | 3.3 V pull-up | - | - |
| LPMode | Ground | - | - |

### J14 QSFP28 Low-Speed Signal Handling

| QSFP Signal | Handling | SFP Signal | Handling |
| --- | --- | --- | --- |
| SCL | 3.3 V pull-up | TX_FULT | 3.3 V pull-up |
| SDA | 3.3 V pull-up | TX_DISABLE | Ground |
| ModSeIL | 3.3 V pull-up | RATE_SELECT0 | 3.3 V pull-up |
| ResetL | 3.3 V pull-up | RATE_SELECT1 | 3.3 V pull-up |
| ModPrsl | 3.3 V pull-up | LOS | 3.3 V pull-up |
| intL | 3.3 V pull-up | - | - |
| LPMode | Ground | - | - |

### JTAG and UART Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball | Description |
| --- | --- | --- | --- |
| UART0_TX | BANK501_PS_MIO39 | J32 | PS UART data output |
| UART0_RX | BANK501_PS_MIO38 | G32 | PS UART data input |

### GPS Module Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball | Module Signal |
| --- | --- | --- | --- |
| PPS_1S_GPS | IO_L4N_AD12N_88 | L17 | TIMEPLUSE |
| TXD_GPS | BANK501_PS_MIO40 | F32 | TXD_MISO |
| RXD_GPS | BANK501_PS_MIO41 | K32 | RXD_MOSI |

### J3 Board-to-Board Connector Pin Assignment

| Signal | J3 Pin | Zynq Pin Name | RFSoC Ball |
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

### J6 Board-to-Board Connector Pin Assignment

| Signal | J6 Pin | Zynq Pin Name | RFSoC Ball |
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

### J9 Expansion IO Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball |
| --- | --- | --- |
| HD_IO_A_P2 | IO_L9P_AD11P_88 | J14 |
| HD_IO_A_N2 | IO_L9N_AD11N_88 | J13 |
| HD_IO_A_P3 | IO_L6P_HDGC_88 | K15 |
| HD_IO_A_N3 | IO_L6N_HDGC_88 | K14 |
| HD_IO_A_P4 | IO_L10P_AD10P_88 | H13 |
| HD_IO_A_N4 | IO_L10N_AD10N_88 | G13 |
| HD_IO_A_P5 | IO_L7P_HDGC_88 | K17 |

### J10 Expansion IO Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball |
| --- | --- | --- |
| HD_IO_A_P6 | IO_L5P_HDGC_88 | L15 |
| HD_IO_A_N6 | IO_L5N_HDGC_88 | L14 |
| HD_IO_A_P7 | IO_L3P_AD13P_88 | N14 |
| HD_IO_A_N7 | IO_L3N_AD13N_88 | M14 |
| HD_IO_A_P8 | IO_L2P_AD14P_88 | N15 |
| HD_IO_A_N8 | IO_L2N_AD14N_88 | M15 |
| HD_IO_A_P9 | IO_L1P_AD15P_88 | N16 |
| HD_IO_A_N9 | IO_L1N_AD15N_88 | M16 |

### J11 PS Expansion IO Pin Assignment

| Signal | PS MIO | RFSoC Ball |
| --- | --- | --- |
| BANK501_PS_MIO36 | PS_MIO36 | E31 |
| BANK501_PS_MIO37 | PS_MIO37 | E32 |
| BANK501_PS_MIO33 | PS_MIO33 | D32 |
| BANK501_PS_MIO44 | PS_MIO44 | K30 |
| BANK501_PS_MIO31 | PS_MIO31 | D33 |
| BANK501_PS_MIO32 | PS_MIO32 | D34 |
| BANK501_PS_MIO42 | PS_MIO42 | H31 |
| BANK501_PS_MIO43 | PS_MIO43 | G31 |

### User LED Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball |
| --- | --- | --- |
| LEDG0 | IO_L12P_AD8P_88 | G16 |
| LEDG1 | IO_L12N_AD8N_88 | G15 |
| LEDG2 | IO_L8P_HDGC_88 | J16 |
| LEDG3 | IO_L8N_HDGC_88 | H16 |

### MMCX Clock and Trigger Assignment

| Signal | Connector | RFSoC Ball | Description |
| --- | --- | --- | --- |
| CLKIN2 | J27 | - | LMK04828 reference clock input |
| CLKOUT | J24 | - | LMK04828 clock output |
| TRIG_IN | JA33 | H15 | Trigger input |
| TRIG_OUT | JA34 | H14 | Trigger output |
| ADC_CLK | J25 | - | ADC_CLK_225 |
| DAC_CLK | J26 | - | DAC_CLK_229 |
| CLK_IN0 | J23 | - | LMK04828 reference clock input |
| SYSREF_IN_P | J21 | - | LMK04828 reference clock input |
| SYSREF_IN_N | J22 | - | LMK04828 reference clock input |

### Fan Control Pin Assignment

| Signal | Zynq Pin Name | RFSoC Ball |
| --- | --- | --- |
| HD_IO_A_N5 | IO_L7N_HDGC_88 | K16 |
