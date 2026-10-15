# 6. 常见问题

[Switch to English](../../en/fpga-tutorial/06-faqs.md)

常见问题解答

1. 提供的例程，登录 vitis，编译/下载失败？

例程路径更换之后，Vitis 软件里面 platform 路径需要根据当前实际路径重新
指定：
Xilinx->Platform Repositories...
这里添加当前的路径就可以

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-222-image-01.jpg)

或者删掉 platform，重新建一个 platform，名称和之前设置一样也可以。

![RFEVM216 FPGA 教程图示](../../assets/fpga-tutorial/page-223-image-01.jpg)
