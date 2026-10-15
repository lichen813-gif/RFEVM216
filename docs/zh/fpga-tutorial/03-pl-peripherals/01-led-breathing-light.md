# 3.1 LED 呼吸灯实验

[Switch to English](../../../en/fpga-tutorial/03-pl-peripherals/01-led-breathing-light.md)

[返回章节总览](index.md)

呼吸灯是在微处理器的控制下，由暗渐渐、亮、然后再由亮渐暗，模仿人呼
吸方式方式的 LED 灯。
FPGA 的引脚电平只有“0”和“1”两个等级，因此通过改变引脚单位时间
内高电平的输出时间来实现呼吸灯，也就是让 FPGA 引脚输出一系列 PWM 波信
号并不断改变 PWM 波的占空比来控制 LED 灯亮度的变化。
PWM 占空比调节示意图如下图所示：
图 3 呼吸灯 PWM 占空比示意图

## 3.1.1 硬件设计

RFEVM216 开发板上有 4 个用户可可控制的 LED 灯。其原理图如下图所示：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-011-image-01.jpg)

图 4 LED 灯硬件原理图

## 3.1.2 硬件工程搭建

1. 在 PC 端，打开 Vivado
2. 点击 Create Project

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-012-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-012-image-02.jpg)

3. 点击 Next
4. 设定工程名称和位置，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-013-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-013-image-02.jpg)

5. 点击 Next
6. 选择 FPGA 型号 xczu49dr-fsvf1760-2-i，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-014-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-014-image-02.jpg)

7. 点击 Finish

这里我们能看到建立的工程

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-015-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-015-image-02.jpg)

8. 在 Flow Navigator 窗口，点击 Add Source
9. 选中添加设计文件，点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-016-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-016-image-02.jpg)

10. 点击 Create Files
11. 设置名称，点击 OK

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-017-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-017-image-02.jpg)

12. 点击 Finish
13. 暂时不添加端口，点击 OK

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-018-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-018-image-02.jpg)

点击 Yes

14. 完成后，可以看到我们新创建的.v 文件

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-019-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-019-image-02.jpg)

15. 双击 breath_led，然后输入以下代码

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-020-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-020-image-02.jpg)

16. 点击 Add Source

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-021-image-01.jpg)

17. 选择添加或创建约束文件，点击 Next
18. 点击 Create File

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-022-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-022-image-02.jpg)

19. 设置名称，点击 OK
20. 点击 Finish

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-023-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-023-image-02.jpg)

21. 这里可以看到新创建的约束文件

双击 rfevm_led.xdc，输入以下约束：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-024-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-024-image-02.jpg)

22. 在 Flow Navigator，点击 Generate Bitstream
23. 点击 OK，等待生成 bit

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-025-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-025-image-02.jpg)

24. 生成 bit 完成之后，选择【View Reports】，点击 OK

## 3.1.3 下载验证

用 USB 转 Type-C 线缆，一端连接板卡，一端连到 PC 上，然后给板卡上电。
在 Vivado 界面，点击 Open Hardware Manager->Open Target->Auto Connect

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-026-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-026-image-02.jpg)

在器件上，右键选择 Program device

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-027-image-01.jpg)

点击 Program
下载完成后，可以看到底板上的 LEDs 灯由暗慢慢变量，再由亮慢慢变暗，
即出现“呼吸”的效果。
