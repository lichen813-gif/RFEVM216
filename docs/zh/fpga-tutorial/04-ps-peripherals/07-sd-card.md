# 4.7 SD 卡读写 TXT 文本实验

[Switch to English](../../../en/fpga-tutorial/04-ps-peripherals/07-sd-card.md)

[返回章节总览](index.md)

RFEVM216 底板上 SD 卡接口为小卡的设计，可以连接 Micro SD 卡（也叫
TF 卡），MPSOC 内部集成了两个 SD 卡控制器，并且 Xilinx Vitis 的 standlone
已经移植好了 FATFS（Vitis 软件中叫做 xilffs）文件系统，FATFS 是一个完全开
源免费的 FAT 文件系统模块，专门为小型的嵌入式系统而设计。它完全用标准 C
语言编写，所以有良好的硬件平台独立性，可以很方便的移植到各种嵌入式处理
器中。因此在 Vitis 中添加 xilffs 库后，就可以在程序中使用 FATFS 中的 API 函
数来操作 SD 卡。
使用者无需理会 FATFS 的内部结构和复杂的 FAT 协议，只需要调用 FATFS
模块提供给用户的一系列应用接口函数，如 f_open、f_read、f_write 和 f_close
等，就可以像在 PC 上读/写文件那样简单。

## 4.7.1 硬件设计

我们的 RFEVM216 开发板上面有一个 SD 卡接口，可以连接 Micro SD 卡（TF
卡），原理图如下图所示：

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-141-image-01.jpg)

图 15 Micro SD 卡原理图
由上图可知，SD 卡共有四根数据线（SDIO_DAT0~SDIO_DAT3），连接至
MPSOC 的引脚。图中 SDIO_DETECT 信号是 TF 卡检测信号，用于标志开发板
是否连接了 TF 卡。当开发板没有连接 TF 卡时，此信号为高电平；而当开发板
连接了 TF 卡之后，此信号为低电平，表示开发板已经连接了 TF 卡。

## 4.7.2 软件设计

BSP 库文件里面添加 xilffs 库
双击 platform.spr，选中 Board Support Package，点击 Modify BSP Settings...

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-142-image-01.jpg)

使能“xilffs”库，点击“OK”
添加完 FATFS 库之后，对 TF 卡的操作会简单很多，我们只需要在程序中调用
FATFS 的库函数即可。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-143-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-143-image-02.jpg)

添加完成之后，重新编译 platform
新建应用程序 File->New->Application Project
点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-144-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-144-image-02.jpg)

点击 Next

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-145-image-01.jpg)

设置应用名称，点击“Next”

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-146-image-01.jpg)

点击“Next”

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-147-image-01.jpg)

这里我们选择 Empty Application(C)作为模板，点击“Finish”

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-148-image-01.jpg)

这里我们可以看到新建的应用工程。
接下来为应用工程新建一个源文件“main.c”

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-149-image-01.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-149-image-02.jpg)

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-150-image-01.jpg)

我们在新建的 main.c 文件中输入下列代码：

#include "xparameters.h"

#include "xil_printf.h"

#include "ff.h"

#include "xstatus.h"

#define FILE_NAME "WE5G.txt" //定义文件名

const char src_str[30] = "www.v3t.com.cn"; //定义文本内容
//main 函数
int main()
{

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-151-image-01.jpg)

int status,len;
char dest_str[30] = "";
static FATFS fatfs;
FIL fil; //文件对象
UINT bw; //f_write 函数返回已写入的字节数
UINT br; //f_read 函数返回已读出的字节数
//注册一个工作区(挂载分区文件系统)
//在使用任何其它文件函数之前，必须使用 f_mount 函数为每个使用卷注册一个工作区
status = f_mount(&fatfs,"1:/", 1); //挂载 SD 卡
if (status != FR_OK) {
xil_printf("\r\nUnable to mount FATfs\r\n");
return -1;
}
xil_printf("Success to open SD card!\r\n");
len = strlen(src_str); //计算字符串长度
//打开一个文件,如果不存在，则创建一个文件
status=f_open(&fil,"1:/WE5G.txt",FA_OPEN_ALWAYS | FA_WRITE | FA_READ);
if (status != FR_OK) {
xil_printf("Unable to open file!\r\n");
return -1;
}
xil_printf("Success to open file.\r\n");
//移动打开的文件对象的文件读/写指针 0:指向文件开头
f_lseek(&fil, 0);
//向文件中写入数据
f_write(&fil,(void*) src_str,len,&bw);
xil_printf("write file return:%d.\r\n",bw);
//SD 卡读数据
//sd_read_data(FILE_NAME,(u32)dest_str,len);
f_lseek(&fil, 0);
f_read(&fil,(void*)dest_str,len,&br);
f_close(&fil);
xil_printf("read file return:%d.\r\n",bw);
//比较写入的字符串和读出的字符串是否相等
if (strcmp(src_str, dest_str) == 0)
xil_printf("src_str is equal to dest_str,SD card test success!\r\n");
else
xil_printf("src_str is not equal to dest_str,SD card test failed!\r\n");
return 0;
}
在 main 函数中，实现的功能是向 TF 卡中读写 TXT 文本，并比较写入的数
据和读出的数据是否一致。程序首先调用 f_mount()函数挂载 TF 卡，接下来根据
待写入字符串的长度，通过 f_write()函数和 f_read()函数对 TF 卡中的 TXT 文本
进行写入和读出，然后比较写入和读出的值，并打印比较的结果。

## 4.7.3 下载验证

首先我们将下载线（USB 转 Type-C 线缆）与开发板的 JTAG 接口连接，另
外一端与电脑连接。接下来插入 TF 卡。最后打开开发板的电源开关。
右键应用工程，选择 Run As->Launch Hardware(Single Application Debug)
打开串口终端，下载完成后，可以查看串口输出：
由上图可知，显示写入的字符和读出的字符一致，说明 TF 卡读写测试成功。
接下来从开发板的卡槽中取出 TF 卡，通过连接读卡器来插入电脑的 USB
接口，此时可以看到 TF 卡中的文件内容如下图所示。

![RFEVM216 FPGA 教程图示](../../../assets/fpga-tutorial/page-153-image-01.jpg)

打开“WE5G.txt”文本，可以看到文本的内容，如下图所示：

## 4.7.4 参考文档

http://elm-chan.org/fsw/ff/00index_e.html
