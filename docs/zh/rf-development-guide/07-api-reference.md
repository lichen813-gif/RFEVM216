# 附录 A：API 介绍

[Switch to English](../../en/rf-development-guide/07-api-reference.md)

附录 A-API 介绍
详细 API 介绍请参考官方文档：
https://docs.xilinx.com/r/en-US/pg269-rf-data-converter
此处只对常用的 API 进行介绍。
配置 RFDC 工作状态
XRFdc_SetMixerSettings
功能：传递 Mixer/NCO 设置用于更新相应的块级寄存器。使用新值更新驱动程
序结构体。
函数原型：
u32 XRFdc_SetMixerSettings(XRFdc *InstancePtr, u32 Type, u32 Tile_Id, u32
Block_Id, XRFdc_Mixer_Settings *MixerSettingsPtr);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Type RF-ADC 或 RF-DAC RF-ADC:0 ; RF-DAC:1
Tile_Id RF-ADC/RF-DAC tile 编号 0~3
Block_Id 块内的 RF-ADC/RF-DAC 块编号 0~3
*MixerSettingsPtr 指向传递混频器 /NCO 设置的
XRFdc_Mixer_Settings 结构的指
针
XRFdc_SetQMCSettings
功能：QMC 设置被填充到相应的寄存器中。使用新值更新程序结构体。
函数原型：
u32 XRFdc_SetQMCSettings(XRFdc *InstancePtr, u32 Type, u32 Tile_Id, u32
Block_Id, XRFdc_QMC_Settings *QMCSettingsPtr);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Type RF-ADC 或 RF-DAC RF-ADC:0 ; RF-DAC:1
Tile_Id RF-ADC/RF-DAC tile 编号 0~3
Block_Id 块内的 RF-ADC/RF-DAC 块编号 0~3
*QMCSettngs 指向用于更新相应寄存器的
XRFdc_QMC_Settings 结构的指
针
XRFdc_SetFabClkOutDiv
功能：使用此 API 设置 PL 时钟输出的分频器。
函数原型：
u32 XRFdc_SetFabClkOutDiv(XRFdc *InstancePtr, u32 Type, u32 Tile_Id, u16
FabClkDiv);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Type RF-ADC 或 RF-DAC RF-ADC:0 ; RF-DAC:1
Tile_Id RF-ADC/RF-DAC tile 编号 0~3
Block_Id 块内的 RF-ADC/RF-DAC 块编号 0~3
FabClkDiv 为 tile 设置的 PL 时钟分频器
时钟分频器有效值：
Macro Description
XRFDC_FAB_CLK_DIV1 Divided by 1
XRFDC_FAB_CLK_DIV2 Divided by 2
XRFDC_FAB_CLK_DIV4 Divided by 4
XRFDC_FAB_CLK_DIV8 Divided by 8
XRFDC_FAB_CLK_DIV16 Divided by 16
配置 ADC 相关工作状态
XRFdc_SetDecimationFactor
功能：此 API 函数为请求的 RF-ADC 设置抽取因子，并根据抽取因子更新 FIFO
写入宽度。
函数原型：
u32 XRFdc_SetDecimationFactor(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id,
u32 DecimationFactor);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Tile_Id RF-ADC tile 编号 0~3
Block_Id 块内的 RF-ADC 块编号 0~3
DecimationFactor RF-ADC 设置的抽取因子
有效的抽取因子：
Macro Description
XRFDC_INTERP_DECIM_OFF Interpolation is OFF
XRFDC_INTERP_DECIM_1X 1X Decimation factor
XRFDC_INTERP_DECIM_2X 2X Decimation factor
XRFDC_INTERP_DECIM_3X 3X Decimation factor
XRFDC_INTERP_DECIM_4X 4X Decimation factor
XRFDC_INTERP_DECIM_5X 5X Decimation factor
XRFDC_INTERP_DECIM_6X 6X Decimation factor
XRFDC_INTERP_DECIM_8X 8X Decimation factor
XRFDC_INTERP_DECIM_10X 10X Decimation factor
XRFDC_INTERP_DECIM_12X 12X Decimation factor
XRFDC_INTERP_DECIM_16X 16X Decimation factor
XRFDC_INTERP_DECIM_20X 20X Decimation factor
XRFDC_INTERP_DECIM_24X 24X Decimation factor
XRFDC_INTERP_DECIM_40X 40X Decimation factor
XRFdc_SetFabRdVldWords
功能：此 API 函数通过写入相应的寄存器来设置所请求的 RF-ADC 的读取 PL 数
据率。
函数原型：
u32 XRFdc_SetFabRdVldWords(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32
FabricRdVldWords);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Tile_Id RF-ADC tile 编号 0~3
Block_Id 块内的 RF-ADC 块编号 0~3
FabricRdVldWords RF-ADC 设置的 PL 数据速率
XRDdc_SetDSA
功能：设置 DSA 值，更新相应的块级寄存器。
函数原型：
u32 XRFdc_SetDSA(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id,
XRFdc_DSA_Settings *SettingsPtr);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Tile_Id RF-ADC tile 编号 0~3
Block_Id 块内的 RF-ADC 块编号 0~3
*SettingsPtr 指向 XRFdc_DSA_Settings 的指
针，用于传递 DSA 设置。
配置 DAC 相关工作状态
XRFdc_SetInterpolationFactor
功能：此 API 函数为请求的 RF-DAC 设置插值因子，并根据插值因子更新 FIFO
的读取宽度。
函数原型：
u32 XRFdc_SetInterpolationFactor(XRFdc *InstancePtr, u32 Tile_Id, u32
Block_Id, u32 InterpolationFactor);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Tile_Id RF-DAC tile 编号 0~3
Block_Id 块内的 RF-DAC 块编号 0~3
InterpolationFactor RF-DAC 设置的插值因子
插值因子有效值：
Macro Description
XRFDC_INTERP_DECIM_OFF Interpolation is OFF
XRFDC_INTERP_DECIM_1X 1X interpolation factor
XRFDC_INTERP_DECIM_2X 2X interpolation factor
XRFDC_INTERP_DECIM_3X 3X interpolation factor
XRFDC_INTERP_DECIM_4X 4X interpolation factor
XRFDC_INTERP_DECIM_5X 5X interpolation factor
XRFDC_INTERP_DECIM_6X 6X interpolation factor
XRFDC_INTERP_DECIM_8X 8X interpolation factor
XRFDC_INTERP_DECIM_10X 10X interpolation factor
XRFDC_INTERP_DECIM_12X 12X interpolation factor
XRFDC_INTERP_DECIM_16X 16X interpolation factor
XRFDC_INTERP_DECIM_20X 20X interpolation factor
XRFDC_INTERP_DECIM_24X 24X interpolation factor
XRFDC_INTERP_DECIM_40X 40X interpolation factor
XRFdc_SetFabWrVldWords
功能：此 API 函数通过写入相应的寄存器来设置请求的 RF-DAC 的写入结构数
据速率。
函数原型：
u32 XRFdc_SetFabWrVldWords(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32
FabricWrVldWords);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Tile_Id RF-DAC tile 编号 0~3
Block_Id 块内的 RF-DAC 块编号 0~3
*FabricDataRatePtr RF-DAC 设置的结构数据速率
XRFdc_SetDACVOP
功能：VOP uA 电流用于更新相应的块级寄存器，动态调整信号强度。
函数原型：
u32 XRFdc_SetDACVOP(XRFdc *InstancePtr, u32 Tile_Id, u32 Block_Id, u32
uACurrent);
参数参数说明取值
*InstancePtr 指向驱动程序实例的指针
Tile_Id RF-DAC tile 编号 0~3
Block_Id 块内的 RF-DAC 块编号 0~3
uACurrent 电流，单位㎂ 2250 ㎂~40500 ㎂
注：对于 ES1 硅，电流范围是 6425 ㎂至 32000 ㎂（数值将被四舍五入到最近的
增量）；对于生产性硅，范围是 2250 ㎂至 40500 ㎂（数据将被四舍五入到最近
的增量）。
