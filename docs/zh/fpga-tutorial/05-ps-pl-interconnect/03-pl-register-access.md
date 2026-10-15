# 5.3 PS 端读写 PL 端的寄存器

[Switch to English](../../../en/fpga-tutorial/05-ps-pl-interconnect/03-pl-register-access.md)

[返回章节总览](index.md)

很多时候，PS/PL 之间只需要简单的数据通路。PS 只需要下发有限的参数
给 PL，PL 只需要向 PS 反馈有限的状态数据。这种情况下，PL 内部只需要实现
AXI-Lite 接口就可以，PS 通过 AXI 接口去访问寄存器，即向 PL 提供参数，也
可以读回 PL 的状态。

## 5.3.1 硬件工程搭建

这里我们依然在上篇 IPI 的工程基础上，去搭建硬件工程。

1. 我们按照之前 IPI 的工程去搭建本实验的硬件工程；
2. 双击 IP，使能 AXI HPM0 LPD 接口；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-190-image-01.jpg)

3. 我们在工程里面添加 up_axi.v 源文件（up_axi 模块实现了 AXI-Lite 协议，这

是 adi 的开源代码，我们只需要关注和使用用户侧信号即可）

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-191-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-191-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-192-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-192-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-192-image-03.jpg)

4. 添加完成之后，我们在 IPI 界面里面右键，添加模块

选择我们刚添加的 up_axi.v 模块

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-193-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-193-image-02.jpg)

点击【OK】

5. 我们选择自动连接【Run Connection Automation】

点击【OK】

6. 我们引出 up_axi 的用户接口信号和时钟复位信号

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-194-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-194-image-02.jpg)

7. Validate 设计

这里提示以下错误，提示时钟频率不一致
我们选中 up_axi，修改 up_axi 总线的频率，重新 validate 即可；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-195-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-195-image-02.jpg)

8. 我们新建顶层文件，例化 bd 文件，和寄存器读写模块；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-196-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-196-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-196-image-03.jpg)

9. 生成 bit，导出硬件工程 xsa 文件；

## 5.3.2 软件工程搭建

我们在 vivado 下搭建好硬件工程，导出 xsa 文件后，在工程目录下面创建
vitis 文件夹作为 vitis 的工作目录。

1. 登录 vitis，选择本工程路径下面的 vitis 文件夹作为工作目录，点击【Launch】
2. 编译硬件平台
3. 新建应用程序

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-197-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-197-image-02.jpg)

中间部分步骤省略，设置应用程序名称
最后选择“Hello World”模板，点击【Finish】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-198-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-198-image-02.jpg)

4. 修改 helloworld.c 文件，添加寄存器读写代码，我们在硬件工程里面使能了 3

个寄存器，这里我们对这三个寄存器进行读写测试；

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-199-image-01.jpg)

5. 编译应用程序

## 5.3.3 下载验证

我们在 vitis 里面 debug，应用程序。

1. 在应用程序上面右键，选择【Debug As】->【Debug configurations...】

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-200-image-01.jpg)

2. 这里我们 Step Over 单步运行程序

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-201-image-01.jpg)

同时打开 chipscope，观测寄存器的读写信号，我们分别设置读写请求为触发信
号，然后单步运行 c 程序，查看 chipscope 信号变化

3. 我们在 vitis 里面执行代码，可以看到 ila 里面信号变化

往寄存器偏移地址 0 里面写 0x01020304

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-202-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-202-image-02.jpg)

往寄存器偏移地址 4 里面写 0x05060708
往寄存器偏移地址 8 里面写 0x090a0b0c
从寄存器偏移地址 0 里面读回 0x01020304

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-203-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-203-image-02.jpg)
