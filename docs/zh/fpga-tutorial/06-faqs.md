# 6. 常见问题

[Switch to English](../../en/fpga-tutorial/06-faqs.md)

> 本章内容来自中文原始 PDF。图示和软件界面截图保留原标签，以便与硬件和软件实际界面对应。  
> Source PDF: `RFEVM216开发平台FPGA教程.pdf`  
> Source pages: 222-223

<a id="page-222"></a>
## 原 PDF 第 222 页

220 / 223  
6 FAQs  
常见问题解答  
1. 提供的例程，登录 vitis，编译/下载失败？  
例程路径更换之后，Vitis 软件里面 platform 路径需要根据当前实际路径重新  
指定：  
Xilinx->Platform Repositories...  
这里添加当前的路径就可以

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 222, figure 1](../../assets/fpga-tutorial/page-222-image-01.jpg)

---

<a id="page-223"></a>
## 原 PDF 第 223 页

221 / 223  
或者删掉 platform，重新建一个 platform，名称和之前设置一样也可以。

### 图示

![RFEVM216 Development Platform FPGA Tutorial, page 223, figure 1](../../assets/fpga-tutorial/page-223-image-01.jpg)
