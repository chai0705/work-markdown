# 1.摄像头组成

对于手机上的摄像头，很多厂家往往是设计为一个摄像头模组(CameraCompact Module)，简称CCM。
![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311300926482.png)

CCM 包含四大件： 镜头(lens)、传感器（sensor）、软板（FPC）、图像处理芯片（DSP）。

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311300926401.png)

决定一个摄像头好坏的重要部件是：镜头（lens）、图像处理芯片 （DSP）、传感器（sensor）。

# 2. 摄像头原理

景物(SCE)通过镜头（LENS）生成的光学图像投射到图像传感器(Sensor)表面上，然后转为电信号，经过A/D（模数转换）转换后变为数字图像信号，再送到数字信号处理芯片（DSP）中加工处理，转换成标准的RGB、YUV等格式图像信号，再通过I/O接口传输到CPU中处理，通过display就可以看到图像了

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311300927790.png)

# 3.摄像头相关技术指标

## 3.0 常见缩略语

| 名称   | 含义                                |
| ------ | ----------------------------------- |
| 3A算法 | AEC, AWB, AF算法                    |
| AEC    | Auto Exposure Control, 自动曝光控制 |
| AWB    | Auto White Balance, 自动白平衡      |
| AF     | Auto Focus, 自动对焦                |
| TE     | Time Exposure, 曝光时间             |
| FBC    | Frame Buffer Compressed, 帧缓冲压缩 |
| IQ     | Image Quality, 图像质量             |

## 3.1. 图像压缩方式JPEG

(joint photographic expert group)静态图像压缩方式。一种有损图像的压缩方式。压缩比越大，图像质量也就越差。
当图像精度要求不高存储空间有限时，可以选择这种格式。目前大部分数码相机都使用JPEG格式。

## 3.1 图像噪音

指的是图像中的杂点干扰，表现为图像中有固定的彩色杂点。

## 3.2 白平衡处理技术(AWB)

白平衡指不管在任何光源下，都能将白色物体还原为白色。

白平衡是描述显示器或相机中红、绿、蓝三基色混合生成后白色精确度的一项指标。

色温表示光谱成份，光的颜色。色温低表示长波光成分多。当色温改变时，光源中三基色（红、绿、蓝）的比例会发生变化，需要调节三基色的比例来达到彩色的平衡，这就是白平衡调节的实际。

图象传感器的图象数据被读取后，系统将对其进行针对镜头的边缘畸变的运算修正，然后经过坏像处理后被系统送进去进行白平衡处理（在不同的环境光照下，人类的眼睛可以把一些“白”色的物体都看成白色，是因为人眼进行了修正。但是SENSOR没有这种功能，因此需要对SENSOR输出的信号进行一定的修正，这就是白平衡处理技术）。

## 3.4. 彩色深度（色彩位数）

反映对色彩的识别能力和成像的色彩表现能力，就是用多少位的二进制数字来记录三种原色。实际就是A/D转换器的量化精度，是指将信号分成多少个等级，常用色彩位数（bit）表示。彩色深度越高，获得的影像色彩就越艳丽动人。

非专业的SENSOR一般是24位；专业型SENSOR至少是36位。24位的SENSOR，感光单元能记录的光亮度值最多有2^8=256级，每一种原色用一个8位的二进制数字来记录，最多记录的色彩是256×256×256约16，77万种。

36位的SENSOR，感光单元能记录的光亮度值最多有2^12=4096级，每一种原色用一个12位的二进制数字来记录，最多记录的色彩是4096×4096×4096约68.7亿种。

## 3.5. 图像格式(image Format/ Color space)

像素格式，比如: RGB24，RGB565，RGB444，YUV4:2:2等。
RGB24,I420是目前最常用的两种图像格式。

1.RGB24
表示R、G、B ，3种基色都用8个二进制位表示，那么红色、绿色、蓝色各有256种，那么由这三种基色构成的颜色就是256X256X256=16,777,216种，约等于1677万。
这就是计算机表示颜色的原理，同样也是手机屏幕和显示器屏幕等显示颜色的原理。

颜色对应RGB值

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311300951502.png)

2.YUV
YUV 和我们熟知的 RGB 类似，是一种颜色编码格式。
YUV 包含三个分量，其中 Y 表示明亮度（Luminance 或 Luma），也就是灰度值。
而 U 和 V 则表示色度（Chrominance 或 Chroma），作用是描述图像色彩及饱和度，用于指定像素的颜色。
没有 UV 分量信息，一样可以显示完整的图像，只不过是黑白的灰度图像。
YUV的采样方式
4:4:4表示完全取样（每一个Y对应一组UV分量)
4:2:2表示2:1的水平取样，垂直完全采样(每两个Y共用一组UV分量)
4:2:0表示2:1的水平取样，垂直2：1采样(每四个Y共用一组UV分量)
4:1:1表示4:1的水平取样，垂直完全采样(每四个Y共用一组UV分量)
存储方式举例：

YUV 4:2:0其颜色的一种存放格式如图所示：

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311300951100.png)



## 3.6. 分辨率（Resolution）

所谓分辨率就是指画面的解析度，由多少象素构成的数值越大，图像也就越清晰。

分辨率不仅与显示尺寸有关，还会受到显像管点距、视频带宽等因素的影响。

我们通常所看到的分辨率都以乘法形式表现的，比如1024*768，其中的1024表示屏幕上水平方向显示的点数，768表示垂直方向的点数。

![image-20231130095332908](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311300953980.png)

## 3.7. 帧率

帧率指的就是1秒钟时间里传输、显示图片的帧数，每一帧就是一个画面，快速连续的多帧就形成了运动的动态效果。高的帧率可以得到更加流畅，更加逼真的画面。

## 3.8. 码流

码流就是指视频数据在单位时间内的数量大小，也叫码率，是视频编码画面质量控制中最重要的部分，同样的分辨率和帧率下，视频码流越大，画面质量越高，对应的存储容量也就越大。

## 3.9. 曝光

曝光就是图像的明暗程度 ，照片太暗称为曝光不足 ，照片太亮称为曝光过度。曝光由光圈、曝光时间、ISO三者共同决定。

光圈：控制进光量。
曝光时间：光到达的时间长度。
ISO：增益，或称为感光度。

# 4 摄像头接口

摄像头常用接口包括：USB、DVP、MIPI

## 4.1.USB

我们常用的电脑摄像头接口是USB接口，这种摄像头比较常见，需要支持UVC（USB Video Class）协议。

## 4.2.DVP

还有一部分的摄像头（比如说某些支持DVP接口的硬件）是DVP(Digital Video Port)摄像头数据并口传输协议，

DVP是并口，提供8-bit或10-bit并行传输数据线、HSYNC(Horizontal sync)行同步线、VSYNC(Vertical sync)帧同步线和PCLK(Pixel Clock)时钟同步线。

DVP总线PCLK极限约在96M左右，而且走线长度不能过长，所有DVP最大速率最好控制在72M以下，PCB layout较容易画

以OV3640摄像头为例：
DVP分为三个部分：

输出总线

输入总线

电源总线

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311300954861.png)

## 4.3 mipi（CSI）

移动产业处理器接口(Mobile Industry Processorinterface，MIPI)

常见的智能手机上的摄像头是MIPI接口，

CSI是相机串行接口（CMOS Sensor Interface）的简称。

MIPI总线速率lvds接口耦合，走线必须差分等长，并且需要保护，故对PCB走线以及阻抗控制要求高一点（一般来讲差分阻抗要求在85欧姆~125欧姆之间）

MIPI是LVDS低压差分串口，只需要要CLKP/N、DATAP/N——最大支持4-lane，一般2-lane即可。

MIPI接口比DVP的接口信号线少，由于是低压差分信号，产生的干扰小，抗干扰能力也强。

DVP接口在信号完整性方面受限制，速率也受限制。

500W还可以勉强用DVP，800W及以上都采用MIPI接口。

所以高清摄像头我们都选用MIPI接口 。

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301000795.png)

# 5.摄像头常用术语

~~~
AE(Auto Exposure):自动曝光。
AF(Auto Focus)   :自动对焦。
AWB(Auto White Balance)：自动白平衡。
3A  :指自动曝光(AE)、自动对焦(AF)和自动白平衡(AWB)算法。
Async Sub Device：在Media Controller结构下注册的V4L2异步子设备，例：Sensor、MIPI DPHY。
Bayer Raw（或Raw Bayer）  :Bayer是相机内部的原始图片，一般后缀为.raw。.raw格式内部的存储方式有：RGGB、BGGR、GRBG等。
CIF     ：Rockchip芯片中的VIP模块，接收Sensor数据并保存到内存中，仅转存数据，无ISP功能。
DVP(Digital Video Port)  ：一种并行数据传输接口。
Entity  ：Media Controller架构下的各节点。
Frame   ：帧。
HSYNC   ：行同步信号，HSYNC有效时，接收到的信号属于同一行。
IOMMU(Input Output Memory Management Unit)：Rockchip芯片中的IOMMU模块，用于将物理上分散的内存页映射成CIF、ISP可见的连续内存。
IQ(Image Quality) ：指为Bayer Raw Camera调试的IQ xml，用于3A tunning。
ISP(Image Signal Processing) ：图像信号处理。
Media Controller ：Linux内核中的一种媒体框架，用于拓扑结构的管理。
MIPI-DPHY     ：Rockchip芯片中符合MIPI-DPHY协议的控制器。
MP(Main Path):Rockchip芯片ISP驱动的一个输出节点，一般用来拍照和抓取Raw图。
PCLK(Pixel Clock) :指Sensor输出的Pixel Clock。
Pipeline          ：Media Controller架构的各Entity之间相互连接形成的链路。
SP(Self Patch)    :Rockchip芯片ISP驱动的一个输出节点。
V4L2(Video4Linux2)   ：指Linux内核的视频处理模块。
VICAP(Video Capture) :视频捕获。
VIP(Video Input Processor):在Rockchip芯片中，曾作为CIF的别名
VSYNC  ：场同步信号，VSYNC有效时，接收到的信号属于同一帧。
~~~

# 6.mipi基本概念

## 1. MIPI

MIPI：移动产业处理器接口(Mobile Industry Processorinterface)
是MIPI联盟发起的为移动应用处理器制定的开放标准。

**MIPI官网**

```bash
https://www.mipi.org
```

**MIPI联盟**
即移动产业处理器接口（MIPI）联盟，由美国德州仪器（TI）、 意法半导体（ST）、 英国ARM和芬兰诺基亚（Nokia）4家公司共同成立， 旨在定义并推广用于移动应用处理器接口的开放标准。

## 2.CSI

MIPI-CSI-2协议是MIPI联盟协议的子协议，专门针对摄像头芯片的接口而设计。

由于其高速，低功耗的特点，MIPI-CSI2协议极大的支持了高清摄像头领域的发展.

正是由于它的普及，手机上五百万像素的摄像头才得以变为前置摄像头，该类接口技术主要掌握在日本东芝，韩国三星以及美国豪威三家公司。

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301004585.png)

1. CSI协议有两个版本协议，分别为CSI-2和CSI-3；
2. CSI-2协议遵循的物理标准有两个，分别为C-PHY和D-PHY；
3. CSI-3协议的物理标准对应M-PHY，且应用层协议栈还需要连接Uni-Pro层。

D-PHY与C-PHY区别：
从实用角度来看，主要是数据线和时钟线的区别，还有传输速率，C-PHY通过某些技术改良，使数据传输速度更快。

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301008321.png)

[瑞芯微](https://so.csdn.net/so/search?q=瑞芯微&spm=1001.2101.3001.7020)3568用的CSI-2 && D-PHY

所以内核中，我们会看到CSI2 和 D-PHY相关代码。

# 7、MIPI协议

MIPI并不是一个单一的接口或协议，而是包含了一套协议和标准，以满足各种子系统独特的要求。MIPI的标准异常复杂，包含非常多的应用领域。

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301008761.png)

由上图可得：

显示设备采用的DSI协议
摄像头采用的CSI协议
RF IC采用的DigRF协议
存储设备采用的UFS
1. DCS（Display Command Set）
用于显示模块命令模式下的标准化命令集；

2. DBI, DPI (Display Bus Interface, Display Pixel Interface)
DBI：与具有显示控制器和帧缓冲器的显示模块的并行接口。
DPI：与显示模块的并行接口，不带显示控制器或帧缓冲器。

3. DSI, CSI (Display Serial Interface, Camera Serial Interface)
DSI：主机处理器与显示模块之间的高速串行接口；
CSI：主机处理器与摄像头模块之间的高速串行接口；

4. D-PHY
为DSI（显示屏）和CSI-2（摄像头）提供物理层通路定义。

5. M-PHY
为DigRF、CSI-3、UFS、LLI、SSIC、M-PCIE提供物理层通路定义。

目前比较成熟的接口应用有DSI(显示接口)，和CSI(摄像头接口)，都具有比较复杂的协议结构，下图表示某一个SOC可以作为一个CSI的接收器，同时也可以作为一个DSI的输出器。

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301013141.png)

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301026820.png)

MIPI接口在系统的实现如上图所示，

通常一个camera的模组如图所示，通常包括Lens、Sensor、CSI接口等，其中CSI接口用于视频数据的传
输；

1. SoC的Mipi接口对接Camera，并通过I2C/SPI控制camera模组；
2. MIPI DPHY提供了4 Lane的Rx接口，由Sensor提供Clock，并通过四条数据Lane输入图像数据;
3. DPHY与CSI-2 Host Contrller之间通过PPI（PHY-Protocol Interface）相连，该接口包括了控制，数据，时钟等多条信号
4. CSI-2 Host Contrller通过PPI接口收到数据后进行解析，完成后通过IDI(Image Data Interface)或者IPI(Image Pixel Interface)输出到SoC的其他模块(VICAP或ISP，rk3568是送至VICAP模块)；
5. ISP将处理过的图片输出到MP主通道或SP自身通道，SP一般用来预览图片，SP图片的最大分辨率比MP低；
6. SoC通过APB Slave总线控制CSI-2 Host Contrller的相关寄存器。

# 8.isp

ISP(Image Signal Processor)，即图像信号处理器，用于处理图像信号传感器输出的图像信号。

它在相机系统中占有核心主导的地位，是构成相机的重要设备。ISP 通过一系列数字图像处理算法完成对数字图像的效果处理。

瑞芯微rk3568平台的ISP2.1 处理图像数据的基本流程如下：

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301030273.png)

ISP 包括:

- MIPI serial camera interface(MIPI)
- RAW Processing
- RGB Processing
- YUV Processing
- Memory Interface(MI)

一般抓图的顺序：

1. 摄像头的初始化（输出格式、分辨率、输出速率）
2. 使能摄像头接入主控板卡中的物理通道
3. 使能主控板卡中的ISP（图像信号处理模块）、并让ISP知道当前有效接入的摄像头是哪一个（因为可以多个接入，但只能一个有效）。
4. 告诉ISP输进来的数据如何处理（颜色空间转换、缩放、裁剪、旋转等）、经由那个通道输出到内存/显存（MP主通道、SP自身通道）。
5. 输出到内存

# 9.摄像头调试命令

## 1. [v4l2](https://so.csdn.net/so/search?q=v4l2&spm=1001.2101.3001.7020)-utils工具包

v4l-utils工具是由Linux维护的V4L2开发工具包。

它提供了一套用于配置V4L2子设备属性的V4L2和媒体框架相关工具,测试V4L2设备,并提供开发库,如libv4l2等等。

v4l-utils工具包主要包含两个常用工具，分别是media-ctl、v4l2-ctl

瑞芯微的SDK在Buildroot固件中，已经编译好了v4l2-utils软件包里面的工具（Android通常默认支持）。

ubuntu系统安装方法：

~~~shell
sudo apt install v4l-utils
~~~

## 2.media-ctl

media-ctl是v4l2-utils包中的一个工具，主要用来查看、配置Media Framework的各Entity的信息，如格式、裁剪、链接使能等。

V4l2-ctl 工具则是针对/dev/video0，/dev/video1 等 video设备，它在 video 设备上进行 set_fmt，reqbuf(申请buf)，qbuf(送buf回队列)，dqbuf(从队列取出buf)，stream_on，stream_off 等一系列操作。

~~~
 n为4的倍数(0,1,2,3…)
 /dev/videon+0：视频输出 SP主通道
 /dev/videon+1：视频输出 MP自身通道
 /dev/videon+2：3A统计
 /dev/videon+3：3A参数设置
~~~

### 1）找到video设备

拓扑结构中有多个的Entity，一些是sub device，一些是video device。前者对应的设备节点是/dev/v4l-subdev，后者对应的是/dev/video。多个的video device中，最常关注的是哪个设备可以输出图像。

~~~
$ media-ctl -d /dev/media0 -e "rkisp_selfpath"
/dev/video1
$ media-ctl -d /dev/media0 -e "rkisp_mainpath"
/dev/video0
~~~

上面两个命令分别显示出/dev/media0这个链路中，RKISP的SP及MP节点的设备路径。RKISP有两个视频输出设备，它们都能输出图像。

#### 2）显示拓扑结构

使用以下命令可以显示拓扑结构

~~~
media-ctl -p -d /dev/media0
~~~

~~~shell
root@topeet:~$ media-ctl -p -d /dev/media0
Media controller API version 4.19.255

Media device information
------------------------
driver          rkisp-vir0
model           rkisp0
serial
bus info
hw revision     0x0
driver version  4.19.255

Device topology
- entity 1: rkisp-isp-subdev (4 pads, 7 links)
            type V4L2 subdev subtype Unknown flags 0
            device node name /dev/v4l-subdev0
        pad0: Sink
                [fmt:SBGGR10_1X10/2112x1568 field:none
                 crop.bounds:(0,0)/2112x1568
                 crop:(0,0)/2112x1568]
                <- "rkisp-csi-subdev":1 [ENABLED]
                <- "rkisp_rawrd0_m":0 []
                <- "rkisp_rawrd2_s":0 []
        pad1: Sink
                <- "rkisp-input-params":0 [ENABLED]
        pad2: Source
                [fmt:YUYV8_2X8/2112x1568 field:none colorspace:smpte170m quantization:full-range
                 crop.bounds:(0,0)/2112x1568
                 crop:(0,0)/2112x1568]
                -> "rkisp_mainpath":0 [ENABLED]
                -> "rkisp_selfpath":0 [ENABLED]
        pad3: Source
                -> "rkisp-statistics":0 [ENABLED]

- entity 6: rkisp-csi-subdev (6 pads, 5 links)
            type V4L2 subdev subtype Unknown flags 0
            device node name /dev/v4l-subdev1
        pad0: Sink
                [fmt:SBGGR10_1X10/2112x1568 field:none]
                <- "rockchip-csi2-dphy0":1 [ENABLED]
        pad1: Source
                [fmt:SBGGR10_1X10/2112x1568 field:none]
                -> "rkisp-isp-subdev":0 [ENABLED]
        pad2: Source
                [fmt:SBGGR10_1X10/2112x1568 field:none]
                -> "rkisp_rawwr0":0 [ENABLED]
        pad3: Source
                [fmt:SBGGR10_1X10/2112x1568 field:none]
        pad4: Source
                [fmt:SBGGR10_1X10/2112x1568 field:none]
                -> "rkisp_rawwr2":0 [ENABLED]
        pad5: Source
                [fmt:SBGGR10_1X10/2112x1568 field:none]
                -> "rkisp_rawwr3":0 [ENABLED]

- entity 13: rkisp_mainpath (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video0
        pad0: Sink
                <- "rkisp-isp-subdev":2 [ENABLED]

- entity 19: rkisp_selfpath (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video1
        pad0: Sink
                <- "rkisp-isp-subdev":2 [ENABLED]

- entity 25: rkisp_rawwr0 (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video2
        pad0: Sink
                <- "rkisp-csi-subdev":2 [ENABLED]

- entity 31: rkisp_rawwr2 (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video3
        pad0: Sink
                <- "rkisp-csi-subdev":4 [ENABLED]

- entity 37: rkisp_rawwr3 (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video4
        pad0: Sink
                <- "rkisp-csi-subdev":5 [ENABLED]

- entity 43: rkisp_rawrd0_m (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video5
        pad0: Source
                -> "rkisp-isp-subdev":0 []

- entity 49: rkisp_rawrd2_s (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video6
        pad0: Source
                -> "rkisp-isp-subdev":0 []

- entity 55: rkisp-statistics (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video7
        pad0: Sink
                <- "rkisp-isp-subdev":3 [ENABLED]

- entity 61: rkisp-input-params (1 pad, 1 link)
             type Node subtype V4L flags 0
             device node name /dev/video8
        pad0: Source
                -> "rkisp-isp-subdev":1 [ENABLED]

- entity 67: rockchip-csi2-dphy0 (2 pads, 2 links)
             type V4L2 subdev subtype Unknown flags 0
             device node name /dev/v4l-subdev2
        pad0: Sink
                [fmt:SBGGR10_1X10/2112x1568@10000/300000 field:none]
                <- "m00_b_ov13850 2-0010":0 [ENABLED]
        pad1: Source
                [fmt:SBGGR10_1X10/2112x1568@10000/300000 field:none]
                -> "rkisp-csi-subdev":0 [ENABLED]

- entity 70: m00_b_ov13850 2-0010 (1 pad, 1 link)
             type V4L2 subdev subtype Sensor flags 0
             device node name /dev/v4l-subdev3
        pad0: Source
                [fmt:SBGGR10_1X10/2112x1568@10000/300000 field:none]
                -> "rockchip-csi2-dphy0":0 [ENABLED]

root@topeet:~$
~~~

从entity70信息中可以看到：

- 该Entity完整的名称是：m00_b_ov13850 4-0010
- 它是一个V4L2 subdev(Sub-Device) Sensor
- 它对应的节点是/dev/v4l-subdev3，应用程序（如v4l2-ctl）可以打开它，并进行配置
- 它仅有一个输出（Source）节点，记为pad0
- 它的输出格式是[fmt:SBGGR10/4224x3136]，其中SBGGR10是一种mbus-code的简称
- 它的Source pad0 链接到"rockchip-csi2-dphy0"的pad0，并且当前的状态是 ENABLED。

![在这里插入图片描述](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301039752.png)

#### 3）修改Entity的format、size

举例一，ov3850摄像头支持多个分辨率的输出，默认为1920x1080。现将输出分辨率改为640x480：

~~~shell
media-ctl -d/dev/media0\
--set-v4l2' "m00_b_ov13850 4-0010":0[fmt:SBGGR10/640x480]'
~~~

修改ov3850输出后，rkisp-isp-subdev的大小及video device crop也相应要修改。因为后级的大小不能大于前级的大小。

~~~shell
media-ctl -d/dev/media0 --set-v4l2 ' "rkisp-isp-subdev":0[fmt:SBGGR10/640x480]'
media-ctl -d/dev/media0 --set-v4l2 ' "rkisp-isp-subdev":0[crop: (0, 0)/640x480]'
media-ctl -d/dev/media0 --set-v4l2 ' "rkisp-isp-subdev":2[crop: (0, 0)/640x480]'
v4l2-ctl -d/dev/video0\
--set-selection=target=crop, top=0, left=0, width=640, height=480
~~~

## 3. v4l2-ctl

v4l2-ctl的帮助信息查看：

~~~shell
--all：显示所有可用信息
-C, --get-ctrl <ctrl>[,<ctrl>...]：获取控制器的值 [VIDIOC_G_EXT_CTRLS]
-c, --set-ctrl <ctrl>=<val>[,<ctrl>=<val>...]：设置控制器的值 [VIDIOC_S_EXT_CTRLS]
-D, --info：显示驱动程序信息 [VIDIOC_QUERYCAP]
-d, --device <dev>：使用指定的设备 <dev>，而不是默认的/dev/video0
-e, --out-device <dev>：将输出流的设备设置为指定的设备 <dev>，而不是默认设备（通过--device设置）
-E, --export-device <dev>：将DMA缓冲区导出到指定的设备 <dev>
-z, --media-bus-info <bus-info>：根据给定的总线信息查找媒体设备
-h, --help：显示帮助信息
--help-all：显示所有选项的帮助信息
--help-io：显示输入/输出选项的帮助信息
--help-meta：显示元数据格式选项的帮助信息
--help-misc：显示其他选项的帮助信息
--help-overlay：显示叠加格式选项的帮助信息
--help-sdr：显示SDR格式选项的帮助信息
--help-selection：显示裁剪/选择选项的帮助信息
--help-stds：显示标准和其他视频定时选项的帮助信息
--help-streaming：显示流式传输选项的帮助信息
--help-subdev：显示子设备选项的帮助信息
--help-tuner：显示调谐器/调制器选项的帮助信息
--help-vbi：显示VBI格式选项的帮助信息
--help-vidcap：显示视频捕获格式选项的帮助信息
--help-vidout：显示视频输出格式选项的帮助信息
--help-edid：显示EDID处理选项的帮助信息
-k, --concise：尽可能精简地输出信息
-l, --list-ctrls：显示所有控制器及其值 [VIDIOC_QUERYCTRL]
-L, --list-ctrls-menus：显示所有控制器及其菜单 [VIDIOC_QUERYMENU]
-r, --subset <ctrl>[,<offset>,<size>]+：获取/设置控制器的N维数组的子集
-w, --wrapper：使用libv4l2包装库
--list-devices：列出所有v4l设备
--log-status：将板卡状态记录到内核日志中 [VIDIOC_LOG_STATUS]
--get-priority：查询当前访问优先级 [VIDIOC_G_PRIORITY]
--set-priority <prio>：设置新的访问优先级 [VIDIOC_S_PRIORITY]，<prio>为1（后台）、2（交互式）或3（记录）
--silent：仅设置结果代码，不打印任何消息
--sleep <secs>：睡眠<secs>秒，调用QUERYCAP并关闭文件句柄
--verbose：开启详细的ioctl状态报告
~~~

### 1）列出所有设备

命令：

~~~shell
v4l2-ctl --list-devices
~~~

![image-20231130104312629](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301043671.png)

### 2）指定设备的预览支持格式

~~~
v4l2-ctl --list-formats-ext --device /dev/video0
v4l2-ctl --list-formats-ext --device /dev/video1
~~~

### 3) 获取指定设备的所有信息

~~~
v4l2-ctl --all --device /dev/video0
~~~

![image-20231130104428683](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301044785.png)

### 4） 显示摄像头参数

~~~
v4l2-ctl --list-ctrls --device /dev/video0
~~~

# 10 瑞芯微显示框架

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301055420.png)

1. Sensor输出数据流通过MIPI的lanes传输给rk3568的DPHY控制器
2. CSI控制器从硬件中提取出图像数据
3. VICAP从MIPI接口读取数据
4. 然后将数据传递给给ISP ，ISP 再输出经过一系列图像处理算法后得到图像。
5. MP用于预览图像
6. SP用于缩放
7. VICAP
8. Video Capture通过DVP/MIPI接口从摄像头读取数据，并通过AXI总线将数据传输到主存中。

ISP(图像信号处理)
ISP是一个完整的视频和静止图像输入设备。
这个模块支持集成YCbCr处理图像传感器和简单CMOS传感器 ，提交没有任何综合图像处理Bayer RGB模式图像。

rk3568采用的是ISP21版本。

ISP21 包含了一系列的图像处理算法模块，主要包括：暗电流矫正、坏点矫正、3A、HDR、镜头阴影矫
正、镜头畸变矫正、3DLUT、去噪（包括RAW域去噪，多帧降噪，颜色去噪等）、锐化等。

ISP21包括硬件算法实现及软件逻辑控制部分，RkAiq即为软件逻辑控制部分的实现。

![ ](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311301056555.png)

RkAiq不断从ISP HW获取统计数据，并经过3A等算法生成新的参数反馈给各硬件模块。

RkAiq软件模块主要实现的功能为：从ISP驱动获取图像统计，结合IQ Tuning参数，使用一系列算法计
算出新的ISP、Sensor等硬件参数，不断迭代该过程，最终达到最优的图像效果。



~~~
gst-launch-1.0 filesrc location=/usr/local/test.mp4 ! qtdemux ! decodebin

GST_DEBUG=4 gst-launch-1.0 filesrc location=/usr/local/test.mp4  ! qtdemux ! avdec_h264 ! videoconvert ! fbdevsink
~~~

~~~
0:00:00.000263354  2222   0x558c507200 INFO                GST_INIT gst.c:586:init_pre: Initializing GStreamer Core Library version 1.16.3
0:00:00.006897364  2222   0x558c507200 INFO                GST_INIT gst.c:587:init_pre: Using library installed in /usr/lib/aarch64-linux-gnu
0:00:00.019289579  2222   0x558c507200 INFO                GST_INIT gst.c:605:init_pre: Linux topeet 4.19.232 #13 SMP Sun Nov 5 19:30:39 PST 2023 aarch64
0:00:00.033587391  2222   0x558c507200 INFO                GST_INIT gstmessage.c:128:_priv_gst_message_initialize: init messages
0:00:00.045494894  2222   0x558c507200 INFO                GST_INIT gstcontext.c:84:_priv_gst_context_initialize: init contexts
0:00:00.056305527  2222   0x558c507200 INFO      GST_PLUGIN_LOADING gstplugin.c:318:_priv_gst_plugin_initialize: registering 0 static plugins
0:00:00.068092291  2222   0x558c507200 INFO      GST_PLUGIN_LOADING gstplugin.c:226:gst_plugin_register_static: registered static plugin "staticelements"
0:00:00.080995464  2222   0x558c507200 INFO      GST_PLUGIN_LOADING gstplugin.c:228:gst_plugin_register_static: added static plugin "staticelements", result: 1
0:00:00.095007757  2222   0x558c507200 INFO            GST_REGISTRY gstregistry.c:1733:ensure_current_registry: reading registry cache: /root/.cache/gstreamer-1.0/registry.aarch64.bin
0:00:00.170913754  2222   0x558c507200 INFO            GST_REGISTRY gstregistrybinary.c:621:priv_gst_registry_binary_read_cache: loaded /root/.cache/gstreamer-1.0/registry.aarch64.bin in 0.059814 seconds
0:00:00.183427293  2222   0x558c507200 INFO            GST_REGISTRY gstregistry.c:1592:scan_and_update_registry: Validating plugins from registry cache: /root/.cache/gstreamer-1.0/registry.aarch64.bin
0:00:00.206382535  2222   0x558c507200 INFO            GST_REGISTRY gstregistry.c:1691:scan_and_update_registry: Registry cache has not changed
0:00:00.213439719  2222   0x558c507200 INFO            GST_REGISTRY gstregistry.c:1768:ensure_current_registry: registry reading and updating done, result = 1
0:00:00.227274693  2222   0x558c507200 INFO                GST_INIT gst.c:806:init_post: GLib runtime version: 2.64.6
0:00:00.237572326  2222   0x558c507200 INFO                GST_INIT gst.c:808:init_post: GLib headers version: 2.64.6
0:00:00.247876666  2222   0x558c507200 INFO                GST_INIT gst.c:810:init_post: initialized GStreamer successfully
0:00:00.262181186  2222   0x558c507200 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstplayback.so" loaded
0:00:00.276168981  2222   0x558c507200 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "playbin" named "playbin"
0:00:00.292787399  2222   0x558c507200 INFO                    play gst-play.c:750:do_play:    0 : file:///usr/local/test.mp4
0:00:00.301609608  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<playsink> current NULL pending VOID_PENDING, desired next READY
0:00:00.316493915  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<streamsynchronizer0> current NULL pending VOID_PENDING, desired next READY
0:00:00.332482966  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<streamsynchronizer0> completed state change to READY
0:00:00.347024591  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<streamsynchronizer0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:00.365239173  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'streamsynchronizer0' changed state to 2(READY) successfully
0:00:00.381291802  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playsink> completed state change to READY
0:00:00.394876546  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playsink> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:00.411977050  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'playsink' changed state to 2(READY) successfully
0:00:00.427117128  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playbin> completed state change to READY
0:00:00.440622545  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playbin> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:00.457954030  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<playsink> current READY pending VOID_PENDING, desired next PAUSED
0:00:00.472864876  2222   0x558c507200 INFO                playsink gstplaysink.c:1439:do_async_start:<playsink> Sending async_start message
0:00:00.485219469  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<streamsynchronizer0> current READY pending VOID_PENDING, desired next PAUSED
0:00:00.501386131  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<streamsynchronizer0> completed state change to PAUSED
0:00:00.516016125  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<streamsynchronizer0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:00.534252579  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'streamsynchronizer0' changed state to 3(PAUSED) successfully
0:00:00.550532399  2222   0x558c507200 INFO              GST_STATES gstbin.c:2959:gst_bin_change_state_func:<playbin> child 'playsink' is changing state asynchronously to PAUSED
0:00:00.566045488  2222   0x558c507200 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "uridecodebin"
0:00:00.580062447  2222   0x558c507200 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<uridecodebin0> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:00.596192654  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<uridecodebin0> notifying about state-changed NULL to READY (PAUSED pending)
0:00:00.613212373  2222   0x558c507200 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<uridecodebin0> continue state change READY to PAUSED, final PAUSED
0:00:00.633748143  2222   0x558c507200 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstcoreelements.so" loaded
0:00:00.646733268  2222   0x558c507200 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "filesrc" named "source"
0:00:00.661439672  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseSrc@0x558c76c120> adding pad 'src'
0:00:00.673852010  2222   0x558c507200 INFO                 filesrc gstfilesrc.c:261:gst_file_src_set_location: filename : /usr/local/test.mp4
0:00:00.686212144  2222   0x558c507200 INFO                 filesrc gstfilesrc.c:262:gst_file_src_set_location: uri      : file:///usr/local/test.mp4
0:00:00.699376630  2222   0x558c507200 INFO                 filesrc gstfilesrc.c:468:gst_file_src_start:<source> opening file /usr/local/test.mp4
0:00:00.712217685  2222   0x558c507200 WARN                 basesrc gstbasesrc.c:3600:gst_base_src_start_complete:<source> pad not activated yet
0:00:00.725108031  2222   0x558c507200 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "decodebin"
0:00:00.738254731  2222   0x558c507200 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "typefind" named "typefind"
0:00:00.752508217  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstTypeFindElement@0x558c76f070> adding pad 'sink'
0:00:00.765869275  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstTypeFindElement@0x558c76f070> adding pad 'src'
0:00:00.779688213  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad typefind:sink
0:00:00.791664257  2222   0x558c507200 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad0 and typefind:sink
0:00:00.804611764  2222   0x558c507200 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad0 and typefind:sink, successful
0:00:00.817926159  2222   0x558c507200 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:00.830066981  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstDecodeBin@0x558c774020> adding pad 'sink'
0:00:00.843575027  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element source:(any) to element decodebin0:sink
0:00:00.858415300  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad decodebin0:sink
0:00:00.870543581  2222   0x558c507200 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: source and decodebin0 in same bin, no need for ghost pads
0:00:00.885487679  2222   0x558c507200 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link source:src and decodebin0:sink
0:00:00.898616006  2222   0x558c507200 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked source:src and decodebin0:sink, successful
0:00:00.911706710  2222   0x558c507200 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:00.923750415  2222   0x558c507200 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<source:src> Received event on flushing pad. Discarding
0:00:00.938453616  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current NULL pending VOID_PENDING, desired next READY
0:00:00.953402088  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<typefind> completed state change to READY
0:00:00.967002002  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<typefind> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:00.984119718  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 2(READY) successfully
0:00:00.999516447  2222   0x558c507200 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<decodebin0> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:01.016132536  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<decodebin0> notifying about state-changed NULL to READY (PAUSED pending)
0:00:01.032883948  2222   0x558c507200 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<decodebin0> continue state change READY to PAUSED, final PAUSED
0:00:01.048467620  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current READY pending VOID_PENDING, desired next PAUSED
0:00:01.063703070  2222   0x558c507200 INFO                 filesrc gstfilesrc.c:468:gst_file_src_start:<source> opening file /usr/local/test.mp4
0:00:01.076486091  2222   0x558c507200 WARN                 basesrc gstbasesrc.c:3600:gst_base_src_start_complete:<source> pad not activated yet
0:00:01.089123873  2222   0x558c507200 INFO                 filesrc gstfilesrc.c:468:gst_file_src_start:<source> opening file /usr/local/test.mp4
0:00:01.101968431  2222   0x558c507200 INFO                    task gsttask.c:460:gst_task_set_lock: setting stream lock 0x558c772310 on task 0x558c776170
0:00:01.115275243  2222   0x558c507200 INFO                GST_PADS gstpad.c:6159:gst_pad_start_task:<typefind:sink> created task 0x558c776170
0:00:01.128166463  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<typefind> completed state change to PAUSED
0:00:01.141475900  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<typefind> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:01.141762877  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad typefind:sink
0:00:01.170804141  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 3(PAUSED) successfully
0:00:01.173773362  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-ms-asf
0:00:01.186298278  2222   0x558c507200 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<source> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:01.200290452  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-musepack
0:00:01.216322964  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<source> notifying about state-changed NULL to READY (PAUSED pending)
0:00:01.230433545  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-au
0:00:01.246662332  2222   0x558c507200 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<source> continue state change READY to PAUSED, final PAUSED
0:00:01.260155504  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-msvideo
0:00:01.275240466  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<source> completed state change to PAUSED
0:00:01.289180144  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/qcelp
0:00:01.302581157  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<source> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:01.316199153  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-cdxa
0:00:01.333667716  2222   0x558c507200 FIXME                    bin gstbin.c:4349:gst_bin_query: implement duration caching in GstBin again
0:00:01.346908034  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-vcd
0:00:01.372719055  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-imelody
0:00:01.386492205  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-scc
0:00:01.400475338  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-mcc
0:00:01.414475387  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/midi
0:00:01.427916938  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/riff-midi
0:00:01.441806746  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/mobile-xmf
0:00:01.455733008  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-fli
0:00:01.469262928  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-id3v2
0:00:01.483515248  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-id3v1
0:00:01.497691157  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-apetag
0:00:01.511999181  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-ttafile
0:00:01.525848741  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-mod
0:00:01.539435823  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/mpeg
0:00:01.552793381  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-ac3
0:00:01.566365880  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-dts
0:00:01.579876843  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-gsm
0:00:01.593377889  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/mpeg-sys
0:00:01.607167663  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/mpegts
0:00:01.620746287  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/ogg
0:00:01.634628803  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/mpeg-elementary
0:00:01.648990489  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/mpeg4
0:00:01.662519242  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-h263
0:00:01.676281018  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-h264
0:00:01.689772149  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-h265
0:00:01.703317817  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-nuv
0:00:01.716857071  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-m4a
0:00:01.730428408  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-3gp
0:00:01.744420878  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/quicktime
0:00:01.758272776  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-quicktime
0:00:01.772385987  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/jp2
0:00:01.785654306  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-jpc
0:00:01.799153315  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/mj2
0:00:01.812513211  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for text/html
0:00:01.825845108  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/vnd.rn-realmedia
0:00:01.840879329  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-pn-realaudio
0:00:01.855683151  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-shockwave-flash
0:00:01.870801657  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/xges
0:00:01.884704884  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/dash+xml
0:00:01.898980540  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/vnd.ms-sstr+xml
0:00:01.913899853  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-flv
0:00:01.927411694  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for text/plain
0:00:01.940886206  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for text/utf-16
0:00:01.954368883  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for text/utf-32
0:00:01.967949844  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for text/uri-list
0:00:01.981599342  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/itc
0:00:01.995435782  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-hls
0:00:02.009499997  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/sdp
0:00:02.023410807  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/smil
0:00:02.037345531  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/ttml+xml
0:00:02.051624979  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/xml
0:00:02.065518582  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-wav
0:00:02.078993093  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-aiff
0:00:02.092597386  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-svx
0:00:02.106113310  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-paris
0:00:02.119796930  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-nist
0:00:02.133447594  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-voc
0:00:02.146960894  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-sds
0:00:02.160503941  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-ircam
0:00:02.174166271  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-w64
0:00:02.187641074  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-rf64
0:00:02.201289988  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-shorten
0:00:02.215281291  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ape
0:00:02.229205809  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/jpeg
0:00:02.242666904  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/gif
0:00:02.256028841  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/png
0:00:02.269327200  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/bmp
0:00:02.282669305  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/tiff
0:00:02.296086363  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/webp
0:00:02.309523252  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-exr
0:00:02.323055800  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-portable-pixmap
0:00:02.337599476  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-matroska
0:00:02.351652900  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/mxf
0:00:02.365414972  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-mve
0:00:02.378946937  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-dv
0:00:02.392361661  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-amr-nb-sh
0:00:02.406502286  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-amr-wb-sh
0:00:02.420466759  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/iLBC-sh
0:00:02.434158253  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-sbc
0:00:02.447736297  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-sid
0:00:02.461163562  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-xcf
0:00:02.474689986  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-mng
0:00:02.488274447  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-jng
0:00:02.501725335  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-xpixmap
0:00:02.515563526  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-sun-raster
0:00:02.529702109  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-bzip
0:00:02.543958809  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-gzip
0:00:02.557962361  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/zip
0:00:02.571824175  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-compress
0:00:02.586279775  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for subtitle/x-kate
0:00:02.600176877  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-subtitle-vtt
0:00:02.615063526  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-flac
0:00:02.628577118  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-vorbis
0:00:02.642473054  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-theora
0:00:02.656142383  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ogm-video
0:00:02.670715224  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ogm-audio
0:00:02.685262983  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ogm-text
0:00:02.699783911  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-speex
0:00:02.713425536  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-celt
0:00:02.727058414  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ogg-skeleton
0:00:02.741870406  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for text/x-cmml
0:00:02.755362712  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-executable
0:00:02.770050756  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/aac
0:00:02.783388199  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-spc
0:00:02.796884296  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-wavpack
0:00:02.810747864  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-wavpack-correction
0:00:02.825565982  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-caf
0:00:02.839155696  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/postscript
0:00:02.853584470  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/svg+xml
0:00:02.867242429  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-rar
0:00:02.881357102  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-tar
0:00:02.895327703  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ar
0:00:02.909274681  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ms-dos-executable
0:00:02.924521806  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-dirac
0:00:02.938278924  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for multipart/x-mixed-replace
0:00:02.952965219  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-mmsh
0:00:02.967082225  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/vivo
0:00:02.980573364  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-nsf
0:00:02.994036505  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-gym
0:00:03.007531436  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-ay
0:00:03.021034532  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-gbs
0:00:03.034556294  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-vgm
0:00:03.048048892  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-sap
0:00:03.061557529  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-ivf
0:00:03.075059168  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-kss
0:00:03.088570430  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/pdf
0:00:03.102421749  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/msword
0:00:03.116631206  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/octet-stream
0:00:03.131269963  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/vnd.adobe.photoshop
0:00:03.145969965  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/vnd.wap.wbmp
0:00:03.160062764  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-yuv4mpeg
0:00:03.174523910  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-icon
0:00:03.188152122  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for image/x-degas
0:00:03.201837495  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/octet-stream
0:00:03.216611866  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for application/x-ssa
0:00:03.230620089  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for video/x-pva
0:00:03.244199597  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-xi
0:00:03.257497959  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/audible
0:00:03.271186833  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-tap-tap
0:00:03.285079274  2222   0x558c75faa0 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for audio/x-tap-dmp
0:00:03.298906386  2222   0x558c75faa0 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgsttypefindfunctions.so" loaded
0:00:03.317513245  2222   0x558c75faa0 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/quicktime, variant=(string)iso
0:00:03.331100918  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad typefind:src
0:00:03.342878943  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad typefind:sink
0:00:03.355222465  2222   0x558c75faa0 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link typefind:src and decodepad0:proxypad1
0:00:03.368522286  2222   0x558c75faa0 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked typefind:src and decodepad0:proxypad1, successful
0:00:03.382272404  2222   0x558c75faa0 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:03.463719116  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking typefind:src(0x558c7724f0) and decodepad0:proxypad1(0x558c754a50)
0:00:03.473436679  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked typefind:src and decodepad0:proxypad1
0:00:03.486042972  2222   0x558c75faa0 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link typefind:src and decodepad0:proxypad1
0:00:03.499699181  2222   0x558c75faa0 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked typefind:src and decodepad0:proxypad1, successful
0:00:03.513455716  2222   0x558c75faa0 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:03.525733618  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking typefind:src(0x558c7724f0) and decodepad0:proxypad1(0x558c754a50)
0:00:03.540705723  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked typefind:src and decodepad0:proxypad1
0:00:03.558379323  2222   0x558c75faa0 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstisomp4.so" loaded
0:00:03.570606479  2222   0x558c75faa0 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "qtdemux"
0:00:03.584452840  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstQTDemux@0x7fb01c6190> adding pad 'sink'
0:00:03.596850024  2222   0x558c75faa0 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link typefind:src and qtdemux0:sink
0:00:03.609513770  2222   0x558c75faa0 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked typefind:src and qtdemux0:sink, successful
0:00:03.622648813  2222   0x558c75faa0 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:03.634826389  2222   0x558c75faa0 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<qtdemux0> completed state change to READY
0:00:03.648335319  2222   0x558c75faa0 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<qtdemux0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:03.665577577  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstelement.c:925:gst_element_get_static_pad: no such pad 'video_%u' in element "qtdemux0"
0:00:03.679167875  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstelement.c:925:gst_element_get_static_pad: no such pad 'audio_%u' in element "qtdemux0"
0:00:03.692938409  2222   0x558c75faa0 INFO        GST_ELEMENT_PADS gstelement.c:925:gst_element_get_static_pad: no such pad 'subtitle_%u' in element "qtdemux0"
0:00:03.707382931  2222   0x558c75faa0 INFO                    task gsttask.c:460:gst_task_set_lock: setting stream lock 0x558c772a00 on task 0x558c776830
0:00:03.720506020  2222   0x558c75faa0 INFO                GST_PADS gstpad.c:6159:gst_pad_start_task:<qtdemux0:sink> created task 0x558c776830
0:00:03.733377128  2222   0x558c75faa0 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<qtdemux0> completed state change to PAUSED
0:00:03.746714576  2222   0x558c75faa0 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<qtdemux0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:03.764105869  2222   0x558c75faa0 INFO                typefind gsttypefindelement.c:180:gst_type_find_element_have_type:<typefind> found caps video/quicktime, variant=(string)iso, probability=100
0:00:03.764535169  2222   0x558c75ff00 INFO                 qtdemux qtdemux.c:14202:qtdemux_parse_tree:<qtdemux0> timescale: 1000
0:00:03.781540035  2222   0x558c75faa0 INFO                    task gsttask.c:312:gst_task_func:<typefind:sink> Task going to paused
0:00:03.792837435  2222   0x558c75ff00 INFO                 qtdemux qtdemux.c:14203:qtdemux_parse_tree:<qtdemux0> duration: 10000
0:00:03.816026312  2222   0x558c75ff00 WARN                 qtdemux qtdemux.c:3250:qtdemux_parse_trex:<qtdemux0> failed to find fragment defaults for stream 1
0:00:03.829904175  2222   0x558c75ff00 INFO                 qtdemux qtdemux.c:11664:qtdemux_parse_trak:<qtdemux0> type avc1 caps video/x-h264, stream-format=(string)avc, alignment=(string)au, level=(string)4.1, profile=(string)constrained-baseline, codec_data=(buffer)0142c029ffe1001b6742c0299a7200f0044fcb8088000003000800000301e078c1924001000468ce32c8
0:00:03.860522091  2222   0x558c75ff00 WARN                 qtdemux qtdemux.c:3250:qtdemux_parse_trex:<qtdemux0> failed to find fragment defaults for stream 2
0:00:03.874477531  2222   0x558c75ff00 INFO                 qtdemux qtdemux.c:12390:qtdemux_parse_trak:<qtdemux0> type mp4a caps audio/mpeg, mpegversion=(int)4, framed=(boolean)true, stream-format=(string)raw, level=(string)2, base-profile=(string)lc, profile=(string)lc, codec_data=(buffer)1190
0:00:03.900224124  2222   0x558c75ff00 INFO          GST_SCHEDULING gstpad.c:4898:gst_pad_get_range_unchecked:<source:src> getrange failed, flow: eos
0:00:03.912980034  2222   0x558c75ff00 INFO          GST_SCHEDULING gstpad.c:5113:gst_pad_pull_range:<decodebin0:sink> pullrange failed, flow: eos
0:00:03.925791647  2222   0x558c75ff00 INFO          GST_SCHEDULING gstpad.c:4898:gst_pad_get_range_unchecked:<sink:proxypad0> getrange failed, flow: eos
0:00:03.939229711  2222   0x558c75ff00 INFO          GST_SCHEDULING gstpad.c:5113:gst_pad_pull_range:<typefind:sink> pullrange failed, flow: eos
0:00:03.951896961  2222   0x558c75ff00 INFO          GST_SCHEDULING gstpad.c:4898:gst_pad_get_range_unchecked:<typefind:src> getrange failed, flow: eos
0:00:03.965136708  2222   0x558c75ff00 INFO          GST_SCHEDULING gstpad.c:5113:gst_pad_pull_range:<qtdemux0:sink> pullrange failed, flow: eos
0:00:03.978321042  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-h264, stream-format=(string)avc, alignment=(string)au, level=(string)4.1, profile=(string)constrained-baseline, codec_data=(buffer)0142c029ffe1001b6742c0299a7200f0044fcb8088000003000800000301e078c1924001000468ce32c8, width=(int)1920, height=(int)1080, framerate=(fraction)24000/1001, pixel-aspect-ratio=(fraction)1/1
0:00:04.016749759  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<qtdemux0> adding pad 'video_0'
0:00:04.028815348  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "multiqueue"
0:00:04.042220456  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad qtdemux0:sink
0:00:04.053912741  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<multiqueue0> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:04.070435520  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<multiqueue0> notifying about state-changed NULL to READY (PAUSED pending)
0:00:04.087264234  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<multiqueue0> continue state change READY to PAUSED, final PAUSED
0:00:04.102853170  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<multiqueue0> completed state change to PAUSED
0:00:04.116787903  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<multiqueue0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:04.134639994  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link qtdemux0:video_0 and decodepad1:proxypad2
0:00:04.148425697  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked qtdemux0:video_0 and decodepad1:proxypad2, successful
0:00:04.162455506  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.176836454  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking qtdemux0:video_0(0x558c7732d0) and decodepad1:proxypad2(0x558c754a50)
0:00:04.190093991  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked qtdemux0:video_0 and decodepad1:proxypad2
0:00:04.203567053  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<multiqueue0> adding pad 'src_0'
0:00:04.215143555  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<multiqueue0> adding pad 'sink_0'
0:00:04.227294304  2222   0x558c75ff00 INFO                    task gsttask.c:460:gst_task_set_lock: setting stream lock 0x558c7737e0 on task 0x7fa8005050
0:00:04.240728577  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:6159:gst_pad_start_task:<multiqueue0:src_0> created task 0x7fa8005050
0:00:04.254028694  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link qtdemux0:video_0 and multiqueue0:sink_0
0:00:04.267449551  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked qtdemux0:video_0 and multiqueue0:sink_0, successful
0:00:04.281357745  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.293682314  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link multiqueue0:src_0 and decodepad1:proxypad2
0:00:04.307537720  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked multiqueue0:src_0 and decodepad1:proxypad2, successful
0:00:04.321733474  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.333931470  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking multiqueue0:src_0(0x558c773770) and decodepad1:proxypad2(0x558c754a50)
0:00:04.349428830  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked multiqueue0:src_0 and decodepad1:proxypad2
0:00:04.362505547  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link multiqueue0:src_0 and decodepad1:proxypad2
0:00:04.376605351  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked multiqueue0:src_0 and decodepad1:proxypad2, successful
0:00:04.390800230  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.403083094  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking multiqueue0:src_0(0x558c773770) and decodepad1:proxypad2(0x558c754a50)
0:00:04.418488295  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked multiqueue0:src_0 and decodepad1:proxypad2
0:00:04.433708301  2222   0x558c75ff00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstvideoparsersbad.so" loaded
0:00:04.449598505  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "h264parse"
0:00:04.463166059  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseParse@0x7fa801d8f0> adding pad 'sink'
0:00:04.475901262  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseParse@0x7fa801d8f0> adding pad 'src'
0:00:04.488921693  2222   0x558c75ff00 INFO               baseparse gstbaseparse.c:4026:gst_base_parse_set_pts_interpolation:<GstH264Parse@0x7fa801d8f0> PTS interpolation: no
0:00:04.504298021  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link multiqueue0:src_0 and h264parse0:sink
0:00:04.517783331  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked multiqueue0:src_0 and h264parse0:sink, successful
0:00:04.531541620  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.543742823  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<h264parse0> completed state change to READY
0:00:04.557386496  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<h264parse0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:04.574900572  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad h264parse0:src
0:00:04.586755303  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link h264parse0:src and decodepad1:proxypad2
0:00:04.600538673  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked h264parse0:src and decodepad1:proxypad2, successful
0:00:04.614464657  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.626525580  2222   0x558c75ff00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<h264parse0:src> Received event on flushing pad. Discarding
0:00:04.643871961  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "capsfilter"
0:00:04.655037538  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7fb01c6f60> adding pad 'sink'
0:00:04.668085966  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7fb01c6f60> adding pad 'src'
0:00:04.681572443  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.693629574  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<capsfilter0> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:04.710245972  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<capsfilter0> notifying about state-changed NULL to READY (PAUSED pending)
0:00:04.727084314  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<capsfilter0> continue state change READY to PAUSED, final PAUSED
0:00:04.742697462  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<capsfilter0> completed state change to PAUSED
0:00:04.756611201  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<capsfilter0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:04.774269937  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking h264parse0:src(0x558c773c10) and decodepad1:proxypad2(0x558c754a50)
0:00:04.789485866  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked h264parse0:src and decodepad1:proxypad2
0:00:04.802305358  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad capsfilter0:sink
0:00:04.814507731  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link h264parse0:src and capsfilter0:sink
0:00:04.828006753  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked h264parse0:src and capsfilter0:sink, successful
0:00:04.841614267  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.853676068  2222   0x558c75ff00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<h264parse0:src> Received event on flushing pad. Discarding
0:00:04.868609394  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad capsfilter0:src
0:00:04.880719608  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link capsfilter0:src and decodepad1:proxypad2
0:00:04.894651138  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked capsfilter0:src and decodepad1:proxypad2, successful
0:00:04.908679493  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:04.920745377  2222   0x558c75ff00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<h264parse0:src> Received event on flushing pad. Discarding
0:00:04.936731829  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<h264parse0> completed state change to PAUSED
0:00:04.949532947  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<h264parse0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:04.975196721  2222   0x558c75ff00 INFO               h264parse gsth264parse.c:1938:gst_h264_parse_update_src_caps:<h264parse0> pixel aspect ratio has been changed 1/1
0:00:04.984769051  2222   0x558c75ff00 INFO               baseparse gstbaseparse.c:4068:gst_base_parse_set_latency:<h264parse0> min/max latency 0:00:00.041708333, 0:00:00.041708333
0:00:05.006094333  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-h264, stream-format=(string)avc, alignment=(string)au, level=(string)4.1, profile=(string)constrained-baseline, codec_data=(buffer)0142c029ffe1001b6742c0299a7200f0044fcb8088000003000800000301e078c1924001000468ce32c8, width=(int)1920, height=(int)1080, framerate=(fraction)24000/1001, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, chroma-format=(string)4:2:0, bit-depth-luma=(uint)8, bit-depth-chroma=(uint)8, parsed=(boolean)true
0:00:05.051732494  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<'':decodepad1> pad has no peer
0:00:05.063024939  2222   0x558c75ff00 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<capsfilter0> reuse caps
0:00:05.075649030  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-h264, stream-format=(string)avc, alignment=(string)au, level=(string)4.1, profile=(string)constrained-baseline, codec_data=(buffer)0142c029ffe1001b6742c0299a7200f0044fcb8088000003000800000301e078c1924001000468ce32c8, width=(int)1920, height=(int)1080, framerate=(fraction)24000/1001, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, chroma-format=(string)4:2:0, bit-depth-luma=(uint)8, bit-depth-chroma=(uint)8, parsed=(boolean)true
0:00:05.126426829  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking capsfilter0:src(0x7fa80202e0) and decodepad1:proxypad2(0x558c754a50)
0:00:05.141767289  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked capsfilter0:src and decodepad1:proxypad2
0:00:05.154674858  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link capsfilter0:src and decodepad1:proxypad2
0:00:05.168592388  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked capsfilter0:src and decodepad1:proxypad2, successful
0:00:05.182600037  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.196920327  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking capsfilter0:src(0x7fa80202e0) and decodepad1:proxypad2(0x558c754a50)
0:00:05.210157161  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked capsfilter0:src and decodepad1:proxypad2
0:00:05.223125975  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link capsfilter0:src and decodepad1:proxypad2
0:00:05.236974969  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked capsfilter0:src and decodepad1:proxypad2, successful
0:00:05.250984076  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.263266943  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking capsfilter0:src(0x7fa80202e0) and decodepad1:proxypad2(0x558c754a50)
0:00:05.278518453  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked capsfilter0:src and decodepad1:proxypad2
0:00:05.291410564  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link capsfilter0:src and decodepad1:proxypad2
0:00:05.305337135  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked capsfilter0:src and decodepad1:proxypad2, successful
0:00:05.319349450  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.336321074  2222   0x558c75ff00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstxvimagesink.so" loaded
0:00:05.349106444  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "xvimagesink"
0:00:05.363237749  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseSink@0x7fa8041ce0> adding pad 'sink'
0:00:05.381848411  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to READY
0:00:05.390300829  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<xvimagesink0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:05.407951400  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:05.420196353  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking capsfilter0:src(0x7fa80202e0) and decodepad1:proxypad2(0x558c754a50)
0:00:05.435487526  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked capsfilter0:src and decodepad1:proxypad2
0:00:05.467809818  2222   0x558c75ff00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstrockchipmpp.so" loaded
0:00:05.480011608  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "mppvideodec"
0:00:05.494050463  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstVideoDecoder@0x7fa8076420> adding pad 'sink'
0:00:05.506639264  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstVideoDecoder@0x7fa8076420> adding pad 'src'
0:00:05.520225488  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link capsfilter0:src and mppvideodec0:sink
0:00:05.533610768  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked capsfilter0:src and mppvideodec0:sink, successful
0:00:05.547361187  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.559608474  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<mppvideodec0> completed state change to READY
0:00:05.573388932  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<mppvideodec0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:05.591152369  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<mppvideodec0:src> pad has no peer
0:00:05.603152633  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad mppvideodec0:src
0:00:05.614985495  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link mppvideodec0:src and decodepad1:proxypad2
0:00:05.628928398  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked mppvideodec0:src and decodepad1:proxypad2, successful
0:00:05.643033747  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.655100507  2222   0x558c75ff00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<mppvideodec0:src> Received event on flushing pad. Discarding
0:00:05.670970301  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<mppvideodec0> completed state change to PAUSED
0:00:05.684248257  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<mppvideodec0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:05.702297796  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:05.718924408  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:05.727860958  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event audio/mpeg, mpegversion=(int)4, framed=(boolean)true, stream-format=(string)raw, level=(string)2, base-profile=(string)lc, profile=(string)lc, codec_data=(buffer)1190, rate=(int)48000, channels=(int)2
0:00:05.754636194  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<qtdemux0> adding pad 'audio_0'
0:00:05.766857528  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link qtdemux0:audio_0 and decodepad2:proxypad3
0:00:05.780607368  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked qtdemux0:audio_0 and decodepad2:proxypad3, successful
0:00:05.794692890  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.806972553  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:05.821186689  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking qtdemux0:audio_0(0x7fa8020c20) and decodepad2:proxypad3(0x558c7553d0)
0:00:05.834628262  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked qtdemux0:audio_0 and decodepad2:proxypad3
0:00:05.848034253  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<multiqueue0> adding pad 'src_1'
0:00:05.859631470  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<multiqueue0> adding pad 'sink_1'
0:00:05.871796517  2222   0x558c75ff00 INFO                    task gsttask.c:460:gst_task_set_lock: setting stream lock 0x7fa8021130 on task 0x7fa8005830
0:00:05.885262587  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:6159:gst_pad_start_task:<multiqueue0:src_1> created task 0x7fa8005830
0:00:05.898628624  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link qtdemux0:audio_0 and multiqueue0:sink_1
0:00:05.911980661  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked qtdemux0:audio_0 and multiqueue0:sink_1, successful
0:00:05.925885947  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.938168526  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link multiqueue0:src_1 and decodepad2:proxypad3
0:00:05.952074979  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked multiqueue0:src_1 and decodepad2:proxypad3, successful
0:00:05.966265492  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:05.978460579  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking multiqueue0:src_1(0x7fa80210c0) and decodepad2:proxypad3(0x558c7553d0)
0:00:05.993958823  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked multiqueue0:src_1 and decodepad2:proxypad3
0:00:06.007044007  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link multiqueue0:src_1 and decodepad2:proxypad3
0:00:06.021139736  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked multiqueue0:src_1 and decodepad2:proxypad3, successful
0:00:06.035339874  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:06.047624495  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking multiqueue0:src_1(0x7fa80210c0) and decodepad2:proxypad3(0x558c7553d0)
0:00:06.063033204  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked multiqueue0:src_1 and decodepad2:proxypad3
0:00:06.078113815  2222   0x558c75ff00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstaudioparsers.so" loaded
0:00:06.093867539  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "aacparse"
0:00:06.107233284  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseParse@0x7fa8097be0> adding pad 'sink'
0:00:06.119994159  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseParse@0x7fa8097be0> adding pad 'src'
0:00:06.133344739  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link multiqueue0:src_1 and aacparse0:sink
0:00:06.146629406  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked multiqueue0:src_1 and aacparse0:sink, successful
0:00:06.160305169  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:06.172511629  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aacparse0> completed state change to READY
0:00:06.186057318  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aacparse0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:06.203422083  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad aacparse0:src
0:00:06.215333983  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link aacparse0:src and decodepad2:proxypad3
0:00:06.228963082  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked aacparse0:src and decodepad2:proxypad3, successful
0:00:06.242805081  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:06.254891385  2222   0x558c75ff00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<aacparse0:src> Received event on flushing pad. Discarding
0:00:06.270039365  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aacparse0> completed state change to PAUSED
0:00:06.283466355  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aacparse0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:06.301142595  2222   0x558c75ff00 INFO                aacparse gstaacparse.c:604:gst_aac_parse_read_audio_specific_config:<aacparse0> Parsed AudioSpecificConfig: 48000 Hz, 2 channels
0:00:06.324651129  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event audio/mpeg, mpegversion=(int)4, framed=(boolean)true, stream-format=(string)raw, level=(string)2, base-profile=(string)lc, profile=(string)lc, codec_data=(buffer)1190, rate=(int)48000, channels=(int)2
0:00:06.347408096  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking aacparse0:src(0x7fa8021560) and decodepad2:proxypad3(0x558c7553d0)
0:00:06.362577658  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked aacparse0:src and decodepad2:proxypad3
0:00:06.375312286  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link aacparse0:src and decodepad2:proxypad3
0:00:06.389046668  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked aacparse0:src and decodepad2:proxypad3, successful
0:00:06.402893334  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:06.415171830  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:06.429416298  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking aacparse0:src(0x7fa8021560) and decodepad2:proxypad3(0x558c7553d0)
0:00:06.442570018  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked aacparse0:src and decodepad2:proxypad3
0:00:06.455289480  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link aacparse0:src and decodepad2:proxypad3
0:00:06.469041361  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked aacparse0:src and decodepad2:proxypad3, successful
0:00:06.482876652  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:06.495158357  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking aacparse0:src(0x7fa8021560) and decodepad2:proxypad3(0x558c7553d0)
0:00:06.510218552  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked aacparse0:src and decodepad2:proxypad3
0:00:06.522952305  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link aacparse0:src and decodepad2:proxypad3
0:00:06.536710602  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked aacparse0:src and decodepad2:proxypad3, successful
0:00:06.550560184  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:06.574562179  2222   0x558c75ff00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstpulseaudio.so" loaded
0:00:06.586648774  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "pulsesink"
0:00:06.600744211  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseSink@0x7fa80aa1b0> adding pad 'sink'
0:00:06.613309394  2222   0x558c75ff00 INFO                   pulse pulsesink.c:3240:gst_pulsesink_change_state:<pulsesink0> new pa main loop thread
0:00:06.626646849  2222   0x558c75ff00 INFO                   pulse pulsesink.c:532:gst_pulseringbuffer_open_device:<pulsesink0> new context with name gst-play-1.0, pbuf=0x7fa80ae040, pctx=0x7fa8095620
0:00:06.645363383  2222   0x558c75ff00 WARN                   pulse pulsesink.c:614:gst_pulseringbuffer_open_device:<pulsesink0> error: Failed to connect: 拒绝连接
0:00:06.658019850  2222   0x558c75ff00 INFO        GST_ERROR_SYSTEM gstelement.c:2153:gst_element_message_full_with_details:<pulsesink0> posting message: Failed to connect: 拒绝连接
0:00:06.674298825  2222   0x558c75ff00 INFO        GST_ERROR_SYSTEM gstelement.c:2180:gst_element_message_full_with_details:<pulsesink0> posted error message: Failed to connect: 拒绝连接
0:00:06.691033931  2222   0x558c75ff00 INFO                   pulse pulsesink.c:3222:gst_pulsesink_release_mainloop:<pulsesink0> terminating pa main loop thread
0:00:06.705132285  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2973:gst_element_change_state:<pulsesink0> have FAILURE change_state return
0:00:06.718540029  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2560:gst_element_abort_state:<pulsesink0> aborting state from NULL to READY
0:00:06.732432487  2222   0x558c75ff00 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<pulsesink0> 0x7fa80aa1b0 dispose
0:00:06.744437134  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<pulsesink0> removing pad 'sink'
0:00:06.756779212  2222   0x558c75ff00 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<pulsesink0> 0x7fa80aa1b0 parent class dispose
0:00:06.770119880  2222   0x558c75ff00 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<pulsesink0> 0x7fa80aa1b0 finalize
0:00:06.782468375  2222   0x558c75ff00 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<pulsesink0> 0x7fa80aa1b0 finalize parent
0:00:06.795478026  2222   0x558c75ff00 WARN                 playbin gstplaybin2.c:4723:autoplug_select_cb:<playbin> Could not activate sink pulsesink
0:00:06.812062649  2222   0x558c75ff00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstalsa.so" loaded
0:00:06.825657921  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "alsasink"
0:00:06.839060709  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseSink@0x7fa80b2b80> adding pad 'sink'
0:00:06.862137617  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to READY
0:00:06.870316479  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<alsasink0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:06.887678041  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad alsasink0:sink
0:00:06.900328095  2222   0x558c75ff00 WARN                    alsa conf.c:5044:parse_args: alsalib error: Unknown parameter AES0
0:00:06.910868981  2222   0x558c75ff00 WARN                    alsa conf.c:5204:snd_config_expand: alsalib error: Parse arguments error: 没有那个文件或目录
0:00:06.925233611  2222   0x558c75ff00 WARN                    alsa pcm.c:2642:snd_pcm_open_noupdate: alsalib error: Unknown PCM default:{AES0 0x02 AES1 0x82 AES2 0x00 AES3 0x02}
0:00:06.941054418  2222   0x558c75ff00 INFO                    alsa gstalsasink.c:332:gst_alsasink_getcaps:<alsasink0> returning caps audio/x-raw, format=(string){ S8, U8, S16LE, U16LE, S24_32LE, U24_32LE, S32LE, U32LE, S24LE, U24LE, F32LE, F64LE }, layout=(string)interleaved, rate=(int)[ 4000, 2147483647 ], channels=(int)2, channel-mask=(bitmask)0x0000000000000003; audio/x-raw, format=(string){ S8, U8, S16LE, U16LE, S24_32LE, U24_32LE, S32LE, U32LE, S24LE, U24LE, F32LE, F64LE }, layout=(string)interleaved, rate=(int)[ 4000, 2147483647 ], channels=(int)1; audio/x-raw, format=(string){ S8, U8, S16LE, U16LE, S24_32LE, U24_32LE, S32LE, U32LE, S24LE, U24LE, F32LE, F64LE }, layout=(string)interleaved, rate=(int)[ 4000, 2147483647 ], channels=(int)3, channel-mask=(bitmask)0x000000000000000b; audio/x-raw, format=(string){ S8, U8, S16LE, U16LE, S24_32LE, U24_32LE, S32LE, U32LE, S24LE, U24LE, F32LE, F64LE }, layout=(string)interleaved, rate=(int)[ 4000, 2147483647 ], channels=(int)4, channel-mask=(bitmask)0x0000000000000033; audio/x-raw, format=(string){ S8, U8, S16LE, U16LE, S24_32LE, U24_32LE, S32LE, U32LE, S24LE, U24LE, F32LE, F64LE }, layout=(string)interleaved, rate=(int)[ 4000, 2147483647 ], channels=(int)6, channel-mask=(bitmask)0x000000000000003f; audio/x-raw, format=(string){ S8, U8, S16LE, U16LE, S24_32LE, U24_32LE, S32LE, U32LE, S24LE, U24LE, F32LE, F64LE }, layout=(string)interleaved, rate=(int)[ 4000, 2147483647 ], channels=(int)8, channel-mask=(bitmask)0x0000000000000c3f
0:00:07.071172516  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking aacparse0:src(0x7fa8021560) and decodepad2:proxypad3(0x558c7553d0)
0:00:07.086329541  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked aacparse0:src and decodepad2:proxypad3
0:00:07.316841098  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_avs
0:00:07.325271357  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_bfstm
0:00:07.338820841  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_brstm
0:00:07.352321038  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_daud
0:00:07.365696702  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_dsf
0:00:07.379161902  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_ea
0:00:07.392580438  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_4xm
0:00:07.405941521  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_gxf
0:00:07.419324477  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_idcin
0:00:07.432923832  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_iff
0:00:07.446378532  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_ipmovie
0:00:07.460156082  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_mm
0:00:07.473513665  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_mmf
0:00:07.487063733  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_nsv
0:00:07.500359487  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_nut
0:00:07.513847727  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_film_cpk
0:00:07.527631109  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_smk
0:00:07.541023689  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_sol
0:00:07.554466724  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_psxstr
0:00:07.568272855  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_vmd
0:00:07.581816798  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_wc3movie
0:00:07.595484690  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_wsaud
0:00:07.609087837  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_wsvqa
0:00:07.622681068  2222   0x558c75ff00 INFO            GST_TYPEFIND gsttypefind.c:72:gst_type_find_register: registering typefind function for avtype_yuv4mpegpipe
0:00:07.638591410  2222   0x558c75ff00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstlibav.so" loaded
0:00:07.653898924  2222   0x558c75ff00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "avdec_aac"
0:00:07.667730137  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstAudioDecoder@0x7fa816e620> adding pad 'sink'
0:00:07.680512889  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstAudioDecoder@0x7fa816e620> adding pad 'src'
0:00:07.694383474  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link aacparse0:src and avdec_aac0:sink
0:00:07.707025071  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked aacparse0:src and avdec_aac0:sink, successful
0:00:07.720417362  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:07.732680409  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<avdec_aac0> completed state change to READY
0:00:07.746265478  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<avdec_aac0> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:07.763798532  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad avdec_aac0:src
0:00:07.775652110  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link avdec_aac0:src and decodepad2:proxypad3
0:00:07.789432873  2222   0x558c75ff00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked avdec_aac0:src and decodepad2:proxypad3, successful
0:00:07.803357999  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:07.815420686  2222   0x558c75ff00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<avdec_aac0:src> Received event on flushing pad. Discarding
0:00:07.835037245  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad alsasink0:sink
0:00:07.842426046  2222   0x558c75ff00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:07.854997652  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<avdec_aac0> completed state change to PAUSED
0:00:07.868545391  2222   0x558c75ff00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<avdec_aac0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:07.891755004  2222   0x558c75ff00 INFO               baseparse gstbaseparse.c:4008:gst_base_parse_set_passthrough:<aacparse0> passthrough: yes
0:00:07.899582729  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:900:gst_event_new_segment: creating segment event time segment start=0:00:00.000000000, offset=0:00:00.000000000, stop=0:00:10.000000000, rate=1.000000, applied_rate=1.000000, flags=0x00, time=0:00:00.000000000, base=0:00:00.000000000, position 0:00:00.000000000, duration 99:99:99.999999999
0:00:07.932591871  2222   0x7fb01bf8c0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:07.933494801  2222   0x558c75ff00 INFO               GST_EVENT gstevent.c:900:gst_event_new_segment: creating segment event time segment start=0:00:00.000000000, offset=0:00:00.000000000, stop=0:00:09.920000000, rate=1.000000, applied_rate=1.000000, flags=0x00, time=0:00:00.000000000, base=0:00:00.000000000, position 0:00:00.000000000, duration 99:99:99.999999999
0:00:07.945042445  2222   0x7fb01bf8c0 INFO               baseparse gstbaseparse.c:4068:gst_base_parse_set_latency:<h264parse0> min/max latency 0:00:00.041708333, 0:00:00.041708333
0:00:07.976433839  2222   0x7fb01bfb00 INFO                aacparse gstaacparse.c:604:gst_aac_parse_read_audio_specific_config:<aacparse0> Parsed AudioSpecificConfig: 48000 Hz, 2 channels
0:00:07.992235694  2222   0x7fb01bf8c0 INFO               baseparse gstbaseparse.c:4843:gst_base_parse_set_upstream_tags:<h264parse0> upstream tags: taglist, video-codec=(string)"H.264\ /\ AVC", bitrate=(uint)6633470;
0:00:08.008552593  2222   0x7fb01bfb00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad alsasink0:sink
0:00:08.028995087  2222   0x7fb01bf8c0 INFO               baseparse gstbaseparse.c:4068:gst_base_parse_set_latency:<h264parse0> min/max latency 0:00:00.041708333, 0:00:00.041708333
0:00:08.039771042  2222   0x7fb01bfb00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event audio/mpeg, mpegversion=(int)4, framed=(boolean)true, stream-format=(string)raw, level=(string)2, base-profile=(string)lc, profile=(string)lc, codec_data=(buffer)1190, rate=(int)48000, channels=(int)2
0:00:08.057535369  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ /\ AVC", bitrate=(uint)6633470;
0:00:08.083376194  2222   0x7fb01bfb00 INFO               baseparse gstbaseparse.c:4008:gst_base_parse_set_passthrough:<aacparse0> passthrough: yes
0:00:08.103249400  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470;
0:00:08.115918707  2222   0x7fb01bfb00 INFO               baseparse gstbaseparse.c:4843:gst_base_parse_set_upstream_tags:<aacparse0> upstream tags: taglist, audio-codec=(string)"MPEG-4\ AAC\ audio", maximum-bitrate=(uint)196608;
0:00:08.138435957  2222   0x7fb01bf8c0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:08.158282914  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC\ audio", maximum-bitrate=(uint)196608;
0:00:08.171165996  2222   0x7fb01bf8c0 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<capsfilter0> reuse caps
0:00:08.191367010  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608;
0:00:08.204060523  2222   0x7fb01bf8c0 INFO                    task gsttask.c:460:gst_task_set_lock: setting stream lock 0x7fa8020a40 on task 0x7fa8005290
0:00:08.225398073  2222   0x7fb01bfb00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event audio/x-raw, format=(string)F32LE, layout=(string)non-interleaved, rate=(int)48000, channels=(int)2, channel-mask=(bitmask)0x0000000000000003
0:00:08.237471551  2222   0x7fb01bf8c0 INFO                GST_PADS gstpad.c:6159:gst_pad_start_task:<mppvideodec0:src> created task 0x7fa8005290
0:00:08.260820278  2222   0x7fb01bfb00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<'':decodepad2> pad has no peer
0:00:08.284673258  2222   0x7fa8004b00 INFO                  mppdec gstmppdec.c:491:gst_mpp_dec_apply_info_change:<mppvideodec0> applying NV12(AFBC) 1920x1080 (1920x1104)
0:00:08.300819253  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-raw, format=(string)NV12, width=(int)1920, height=(int)1084, interlace-mode=(string)progressive, multiview-mode=(string)mono, multiview-flags=(GstVideoMultiviewFlagsSet)0:ffffffff:/right-view-first/left-flipped/left-flopped/right-flipped/right-flopped/half-aspect/mixed-mono, pixel-aspect-ratio=(fraction)1/1, chroma-site=(string)mpeg2, colorimetry=(string)bt709, framerate=(fraction)24000/1001, arm-afbc=(int)1
0:00:08.347171400  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<decodebin0> adding pad 'src_0'
0:00:08.359385743  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link decodebin0:src_0 and src_0:proxypad4
0:00:08.372433895  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked decodebin0:src_0 and src_0:proxypad4, successful
0:00:08.386104125  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:08.398504536  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<uridecodebin0> adding pad 'src_0'
0:00:08.410503937  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "input-selector"
0:00:08.424117879  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstInputSelector@0x7f8c00b030> adding pad 'src'
0:00:08.437325852  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<inputselector0> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:08.454187542  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector0> notifying about state-changed NULL to READY (PAUSED pending)
0:00:08.471275255  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<inputselector0> continue state change READY to PAUSED, final PAUSED
0:00:08.487141272  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector0> completed state change to PAUSED
0:00:08.501351918  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:08.519221237  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad inputselector0:src
0:00:08.531904251  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<inputselector0> adding pad 'sink_0'
0:00:08.544092929  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link uridecodebin0:src_0 and inputselector0:sink_0
0:00:08.558437148  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<inputselector0:src> pad has no peer
0:00:08.570377636  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked uridecodebin0:src_0 and inputselector0:sink_0, successful
0:00:08.584786017  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:08.597185261  2222   0x7fa8004b00 INFO               decodebin gstdecodebin2.c:4786:gst_decode_bin_expose:<decodebin0:src_0> added new decoded pad
0:00:08.610168669  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<decodebin0> adding pad 'src_1'
0:00:08.622381261  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link decodebin0:src_1 and src_1:proxypad5
0:00:08.635693935  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked decodebin0:src_1 and src_1:proxypad5, successful
0:00:08.649342583  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:08.661717329  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<uridecodebin0> adding pad 'src_1'
0:00:08.673715272  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:363:gst_element_factory_create: creating element "input-selector"
0:00:08.687157144  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstInputSelector@0x7f8c00b190> adding pad 'src'
0:00:08.700622347  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<inputselector1> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:08.717528660  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector1> notifying about state-changed NULL to READY (PAUSED pending)
0:00:08.734626294  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<inputselector1> continue state change READY to PAUSED, final PAUSED
0:00:08.750475984  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector1> completed state change to PAUSED
0:00:08.764646387  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector1> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:08.782594164  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad inputselector1:src
0:00:08.794954624  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<inputselector1> adding pad 'sink_0'
0:00:08.807290002  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link uridecodebin0:src_1 and inputselector1:sink_0
0:00:08.821739800  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<inputselector1:src> pad has no peer
0:00:08.833624880  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked uridecodebin0:src_1 and inputselector1:sink_0, successful
0:00:08.848052513  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:08.860425514  2222   0x7fa8004b00 INFO               decodebin gstdecodebin2.c:4786:gst_decode_bin_expose:<decodebin0:src_1> added new decoded pad
0:00:08.873453838  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "tee" named "audiotee"
0:00:08.887790479  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstTee@0x7fa8080690> adding pad 'sink'
0:00:08.900162312  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad audiotee:sink
0:00:08.912112721  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<audiotee> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:08.928438665  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<audiotee> notifying about state-changed NULL to READY (PAUSED pending)
0:00:08.945103792  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<audiotee> continue state change READY to PAUSED, final PAUSED
0:00:08.960357944  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<audiotee> completed state change to PAUSED
0:00:08.974049759  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<audiotee> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:08.991462661  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link audio_sink:proxypad6 and audiotee:sink
0:00:09.005024694  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked audio_sink:proxypad6 and audiotee:sink, successful
0:00:09.018852707  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:09.031020682  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<playsink> adding pad 'audio_sink'
0:00:09.043217238  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link inputselector1:src and playsink:audio_sink
0:00:09.057365476  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked inputselector1:src and playsink:audio_sink, successful
0:00:09.071494173  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:09.084059367  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<playsink> adding pad 'video_sink'
0:00:09.095874453  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link inputselector0:src and playsink:video_sink
0:00:09.109986235  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<video_sink:proxypad7> pad has no peer
0:00:09.122189207  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked inputselector0:src and playsink:video_sink, successful
0:00:09.136302448  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:09.148643367  2222   0x7fa8004b00 INFO                 playbin gstplaybin2.c:3818:no_more_pads_cb:<playbin> setting custom audio sink <alsasink0>
0:00:09.161530245  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad alsasink0:sink
0:00:09.173566396  2222   0x7fa8004b00 INFO                 playbin gstplaybin2.c:3825:no_more_pads_cb:<playbin> setting custom video sink <xvimagesink0>
0:00:09.187005939  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad xvimagesink0:sink
0:00:09.199514554  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:3421:bin_handle_async_done:<decodebin0> committing state from READY to PAUSED, old pending PAUSED
0:00:09.214578846  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:3444:bin_handle_async_done:<decodebin0> completed state change, pending VOID
0:00:09.228030930  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<decodebin0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:09.245622610  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:3421:bin_handle_async_done:<uridecodebin0> committing state from READY to PAUSED, old pending PAUSED
0:00:09.260949673  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:3444:bin_handle_async_done:<uridecodebin0> completed state change, pending VOID
0:00:09.274651404  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<uridecodebin0> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:09.293118308  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to READY
0:00:09.306425736  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "bin" named "vbin"
0:00:09.320209710  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "queue" named "vqueue"
0:00:09.334237499  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstQueue@0x7f8c00e640> adding pad 'sink'
0:00:09.346803276  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstQueue@0x7f8c00e640> adding pad 'src'
0:00:09.360150077  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstPlaySinkConvertBin@0x7fa8190930> adding pad 'sink'
0:00:09.373440589  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstPlaySinkConvertBin@0x7fa8190930> adding pad 'src'
0:00:09.387203565  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "identity" named "identity"
0:00:09.402038917  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c01c1c0> adding pad 'sink'
0:00:09.415204023  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c01c1c0> adding pad 'src'
0:00:09.431070044  2222   0x7fa8004b00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstvideofilter.so" loaded
0:00:09.446211914  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "videobalance" named "videobalance"
0:00:09.462171553  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c01fac0> adding pad 'sink'
0:00:09.475152048  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c01fac0> adding pad 'src'
0:00:09.488451602  2222   0x7fa8004b00 INFO      playsinkconvertbin gstplaysinkconvertbin.c:579:gst_play_sink_convert_bin_cache_converter_caps:<GstPlaySinkVideoConvert@0x7fa8190930> No conversion elements
0:00:09.508773654  2222   0x7fa8004b00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstvideoconvert.so" loaded
0:00:09.523883151  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "videoconvert" named "conv"
0:00:09.539382284  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c04c3a0> adding pad 'sink'
0:00:09.551837237  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c04c3a0> adding pad 'src'
0:00:09.567389449  2222   0x7fa8004b00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstvideoscale.so" loaded
0:00:09.582811880  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "videoscale" named "scale"
0:00:09.597834759  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c04d7f0> adding pad 'sink'
0:00:09.610684889  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c04d7f0> adding pad 'src'
0:00:09.624289503  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element conv:src to element scale:sink
0:00:09.638547399  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:src
0:00:09.650041384  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad scale:sink
0:00:09.661714439  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: conv and scale in same bin, no need for ghost pads
0:00:09.676145280  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link conv:src and scale:sink
0:00:09.688721556  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked conv:src and scale:sink, successful
0:00:09.701070642  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:09.713170955  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<conv:src> Received event on flushing pad. Discarding
0:00:09.727643214  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:sink
0:00:09.739231112  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<scale:src> pad has no peer
0:00:09.776373165  2222   0x7fa8004b00 INFO      playsinkconvertbin gstplaysinkconvertbin.c:591:gst_play_sink_convert_bin_cache_converter_caps:<vconv> Converter caps: video/x-raw, format=(string){ I420, YV12, YUY2, UYVY, AYUV, VUYA, RGBx, BGRx, xRGB, xBGR, RGBA, BGRA, ARGB, ABGR, RGB, BGR, Y41B, Y42B, YVYU, Y444, v210, v216, Y210, Y410, NV12, NV21, GRAY8, GRAY16_BE, GRAY16_LE, v308, RGB16, BGR16, RGB15, BGR15, UYVP, A420, RGB8P, YUV9, YVU9, IYU1, ARGB64, AYUV64, r210, I420_10BE, I420_10LE, I422_10BE, I422_10LE, Y444_10BE, Y444_10LE, GBR, GBR_10BE, GBR_10LE, NV16, NV24, NV12_64Z32, A420_10BE, A420_10LE, A422_10BE, A422_10LE, A444_10BE, A444_10LE, NV61, P010_10BE, P010_10LE, IYU2, VYUY, GBRA, GBRA_10BE, GBRA_10LE, BGR10A2_LE, GBR_12BE, GBR_12LE, GBRA_12BE, GBRA_12LE, I420_12BE, I420_12LE, I422_12BE, I422_12LE, Y444_12BE, Y444_12LE, GRAY10_LE32, NV12_10LE32, NV16_10LE32, NV12_10LE40 }, width=(int)[ 1, 32767 ], height=(int)[ 1, 32767 ], framerate=(fraction)[ 0/1, 2147483647/1 ]; video/x-raw(ANY), format=(string){ I420, YV12, YUY2, UYVY, AYUV, VUYA, RGBx, BGRx, xRGB, xBGR, RGBA, BGRA, ARGB, ABGR, RGB, BGR, Y41B, Y42B, YVYU, Y444, v210, v216, Y210, Y410, NV12, NV21, GRAY8, GRAY16_BE, GRAY16_LE, v308, RGB16, BGR16, RGB15, BGR15, UYVP, A420, RGB8P, YUV9, YVU9, IYU1, ARGB64, AYUV64, r210, I420_10BE, I420_10LE, I422_10BE, I422_10LE, Y444_10BE, Y444_10LE, GBR, GBR_10BE, GBR_10LE, NV16, NV24, NV12_64Z32, A420_10BE, A420_10LE, A422_10BE, A422_10LE, A444_10BE, A444_10LE, NV61, P010_10BE, P010_10LE, IYU2, VYUY, GBRA, GBRA_10BE, GBRA_10LE, BGR10A2_LE, GBR_12BE, GBR_12LE, GBRA_12BE, GBRA_12LE, I420_12BE, I420_12LE, I422_12BE, I422_12LE, Y444_12BE, Y444_12LE, GRAY10_LE32, NV12_10LE32, NV16_10LE32, NV12_10LE40 }, width=(int)[ 1, 32767 ], height=(int)[ 1, 32767 ], framerate=(fraction)[ 0/1, 2147483647/1 ]
0:00:09.928592759  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element vqueue:src to element vconv:sink
0:00:09.943066477  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad vqueue:src
0:00:09.954758200  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad vconv:sink
0:00:09.966483754  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: vqueue and vconv in same bin, no need for ghost pads
0:00:09.981039423  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link vqueue:src and vconv:sink
0:00:09.993657992  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked vqueue:src and vconv:sink, successful
0:00:10.006324098  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:10.018454163  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<vqueue:src> Received event on flushing pad. Discarding
0:00:10.033162654  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element vconv:src to element xvimagesink0:(any)
0:00:10.048264864  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad vconv:src
0:00:10.059844596  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1034:gst_pad_check_link: trying to link vconv:src and xvimagesink0:sink
0:00:10.073041787  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<vqueue:sink> pad has no peer
0:00:10.084529943  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: vconv and xvimagesink0 in same bin, no need for ghost pads
0:00:10.099470874  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link vconv:src and xvimagesink0:sink
0:00:10.112601861  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked vconv:src and xvimagesink0:sink, successful
0:00:10.125821508  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:10.137910451  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<vconv:src> Received event on flushing pad. Discarding
0:00:10.152535240  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad vqueue:sink
0:00:10.164415657  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad10 and vqueue:sink
0:00:10.177387990  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad10 and vqueue:sink, successful
0:00:10.190563891  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:10.202764242  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<vbin> adding pad 'sink'
0:00:10.214482213  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<streamsynchronizer0> adding pad 'src_0'
0:00:10.226755766  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<streamsynchronizer0> adding pad 'sink_0'
0:00:10.239625149  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link video_sink:proxypad7 and streamsynchronizer0:sink_0
0:00:10.254471879  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked video_sink:proxypad7 and streamsynchronizer0:sink_0, successful
0:00:10.269423601  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:10.281790772  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "bin" named "vdbin"
0:00:10.295366225  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "videoconvert" named "vdconv"
0:00:10.309883106  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c058dd0> adding pad 'sink'
0:00:10.323429395  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c058dd0> adding pad 'src'
0:00:10.342981512  2222   0x7fa8004b00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstdeinterlace.so" loaded
0:00:10.355313103  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "deinterlace" named "deinterlace"
0:00:10.371171546  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstDeinterlace@0x7f8c06ab50> adding pad 'sink'
0:00:10.383609587  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstDeinterlace@0x7f8c06ab50> adding pad 'src'
0:00:10.397087631  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element vdconv:src to element deinterlace:sink
0:00:10.411867866  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad vdconv:src
0:00:10.423553174  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad deinterlace:sink
0:00:10.435779772  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: vdconv and deinterlace in same bin, no need for ghost pads
0:00:10.450851360  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link vdconv:src and deinterlace:sink
0:00:10.463996346  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked vdconv:src and deinterlace:sink, successful
0:00:10.477150957  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:10.489368806  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<vdconv:src> Received event on flushing pad. Discarding
0:00:10.503882479  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad vdconv:sink
0:00:10.515825016  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad11 and vdconv:sink
0:00:10.528752728  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad11 and vdconv:sink, successful
0:00:10.541962167  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:10.554078525  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad deinterlace:src
0:00:10.566439863  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link deinterlace:src and src:proxypad12
0:00:10.579595640  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked deinterlace:src and src:proxypad12, successful
0:00:10.593082142  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:10.605160585  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<deinterlace:src> Received event on flushing pad. Discarding
0:00:10.620284961  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<vdbin> adding pad 'sink'
0:00:10.631624670  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<vdbin> adding pad 'src'
0:00:10.643216651  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<deinterlace> current NULL pending VOID_PENDING, desired next READY
0:00:10.658340443  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<deinterlace> completed state change to READY
0:00:10.672216289  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<deinterlace> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:10.689734480  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'deinterlace' changed state to 2(READY) successfully
0:00:10.704812192  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdconv> current NULL pending VOID_PENDING, desired next READY
0:00:10.719676715  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdconv> completed state change to READY
0:00:10.733070186  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdconv> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:10.750072755  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'vdconv' changed state to 2(READY) successfully
0:00:10.764835205  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<vdbin> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:10.780987630  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdbin> notifying about state-changed NULL to READY (PAUSED pending)
0:00:10.797356748  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<vdbin> continue state change READY to PAUSED, final PAUSED
0:00:10.812511751  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<deinterlace> current READY pending VOID_PENDING, desired next PAUSED
0:00:10.827936232  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<deinterlace> completed state change to PAUSED
0:00:10.841862829  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<deinterlace> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:10.859488642  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'deinterlace' changed state to 3(PAUSED) successfully
0:00:10.874741929  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdconv> current READY pending VOID_PENDING, desired next PAUSED
0:00:10.889851726  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdconv> completed state change to PAUSED
0:00:10.903289819  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdconv> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:10.920447251  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'vdconv' changed state to 3(PAUSED) successfully
0:00:10.935314401  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdbin> completed state change to PAUSED
0:00:10.948669375  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdbin> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:10.965759146  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking streamsynchronizer0:src_0(0x7f8c009140) and vbin:sink(0x558c779980)
0:00:10.981075719  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link streamsynchronizer0:src_0 and vdbin:sink
0:00:10.995018940  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked streamsynchronizer0:src_0 and vdbin:sink, successful
0:00:11.008980825  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:11.021820464  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<xvimagesink0> current READY pending VOID_PENDING, desired next READY
0:00:11.036589038  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<xvimagesink0> skipping transition from READY to  READY
0:00:11.050883982  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'xvimagesink0' changed state to 2(READY) successfully
0:00:11.066153309  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vconv> current NULL pending VOID_PENDING, desired next READY
0:00:11.080999168  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<scale> current NULL pending VOID_PENDING, desired next READY
0:00:11.095736245  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to READY
0:00:11.109097343  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<scale> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:11.107674411  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:11.126001336  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'scale' changed state to 2(READY) successfully
0:00:11.152296858  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current NULL pending VOID_PENDING, desired next READY
0:00:11.166977939  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to READY
0:00:11.180287125  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:11.197161079  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'conv' changed state to 2(READY) successfully
0:00:11.208572827  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:11.211782664  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current NULL pending VOID_PENDING, desired next READY
0:00:11.238398119  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to READY
0:00:11.251911456  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:11.269208586  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'identity' changed state to 2(READY) successfully
0:00:11.284033447  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vconv> completed state change to READY
0:00:11.297320760  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vconv> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:11.308702760  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:11.314217170  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vconv' changed state to 2(READY) successfully
0:00:11.340515317  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vqueue> current NULL pending VOID_PENDING, desired next READY
0:00:11.355321513  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vqueue> completed state change to READY
0:00:11.368715567  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vqueue> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:11.385742926  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vqueue' changed state to 2(READY) successfully
0:00:11.400391051  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<vbin> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:11.416469691  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vbin> notifying about state-changed NULL to READY (PAUSED pending)
0:00:11.409163710  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:11.432770855  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<vbin> continue state change READY to PAUSED, final PAUSED
0:00:11.459431224  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<xvimagesink0> current READY pending VOID_PENDING, desired next PAUSED
0:00:11.475055482  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2959:gst_bin_change_state_func:<vbin> child 'xvimagesink0' is changing state asynchronously to PAUSED
0:00:11.490554333  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vconv> current READY pending VOID_PENDING, desired next PAUSED
0:00:11.505513642  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:sink
0:00:11.509822103  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:11.517504888  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad8 and identity:sink
0:00:11.542344230  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad8 and identity:sink, successful
0:00:11.555645541  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:11.567758111  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:src
0:00:11.579628033  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link identity:src and src:proxypad9
0:00:11.592648491  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked identity:src and src:proxypad9, successful
0:00:11.605810688  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:11.617871928  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<identity:src> Received event on flushing pad. Discarding
0:00:11.610871591  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<vbin:sink> pad has no peer
0:00:11.632835904  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<scale> current READY pending VOID_PENDING, desired next PAUSED
0:00:11.658990853  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to PAUSED
0:00:11.672305288  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<scale> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:11.689415766  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'scale' changed state to 3(PAUSED) successfully
0:00:11.704147009  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current READY pending VOID_PENDING, desired next PAUSED
0:00:11.711960159  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<vbin:sink> pad has no peer
0:00:11.719047992  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PAUSED
0:00:11.743676774  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:11.760689264  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'conv' changed state to 3(PAUSED) successfully
0:00:11.775314353  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current READY pending VOID_PENDING, desired next PAUSED
0:00:11.790569394  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to PAUSED
0:00:11.804175478  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:11.812175574  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<vbin:sink> pad has no peer
0:00:11.821565648  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'identity' changed state to 3(PAUSED) successfully
0:00:11.847900841  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vconv> completed state change to PAUSED
0:00:11.861214405  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vconv> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:11.878315555  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vconv' changed state to 3(PAUSED) successfully
0:00:11.892966601  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vqueue> current READY pending VOID_PENDING, desired next PAUSED
0:00:11.908263639  2222   0x7fa8004b00 INFO                    task gsttask.c:460:gst_task_set_lock: setting stream lock 0x7fa8170fb0 on task 0x7fac010ef0
0:00:11.921534623  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:6159:gst_pad_start_task:<vqueue:src> created task 0x7fac010ef0
0:00:11.933870013  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<vbin:sink> pad has no peer
0:00:11.934287064  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vqueue> completed state change to PAUSED
0:00:11.958632660  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vqueue> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:11.975804971  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vqueue' changed state to 3(PAUSED) successfully
0:00:11.990584340  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking streamsynchronizer0:src_0(0x7f8c009140) and vbin:sink(0x558c779980)
0:00:12.005993369  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking vdbin:src(0x7f8c070090) and vbin:sink(0x558c779980)
0:00:12.013250064  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<vbin:sink> pad has no peer
0:00:12.039288363  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link vdbin:src and vbin:sink
0:00:12.046286661  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked vdbin:src and vbin:sink, successful
0:00:12.058817452  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:12.071380616  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to READY
0:00:12.084612520  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "bin" named "abin"
0:00:12.098488083  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "queue" named "aqueue"
0:00:12.112333899  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstQueue@0x7f8c00e940> adding pad 'sink'
0:00:12.125122212  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstQueue@0x7f8c00e940> adding pad 'src'
0:00:12.138235417  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstPlaySinkConvertBin@0x7fa8190b30> adding pad 'sink'
0:00:12.151889331  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstPlaySinkConvertBin@0x7fa8190b30> adding pad 'src'
0:00:12.165519038  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "identity" named "identity"
0:00:12.179984014  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c01c580> adding pad 'sink'
0:00:12.193479565  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c01c580> adding pad 'src'
0:00:12.208793227  2222   0x7fa8004b00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstvolume.so" loaded
0:00:12.224091723  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "volume" named "volume"
0:00:12.239005831  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c07d300> adding pad 'sink'
0:00:12.251778687  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c07d300> adding pad 'src'
0:00:12.265133082  2222   0x7fa8004b00 INFO      playsinkconvertbin gstplaysinkconvertbin.c:579:gst_play_sink_convert_bin_cache_converter_caps:<GstPlaySinkAudioConvert@0x7fa8190b30> No conversion elements
0:00:12.285464777  2222   0x7fa8004b00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstaudioconvert.so" loaded
0:00:12.300709902  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "audioconvert" named "conv"
0:00:12.315688464  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c0807b0> adding pad 'sink'
0:00:12.328859706  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c0807b0> adding pad 'src'
0:00:12.344395892  2222   0x7fa8004b00 INFO      GST_PLUGIN_LOADING gstplugin.c:902:_priv_gst_plugin_load_file_for_registry: plugin "/usr/lib/aarch64-linux-gnu/gstreamer-1.0/libgstaudioresample.so" loaded
0:00:12.359904372  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "audioresample" named "resample"
0:00:12.375335567  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c084690> adding pad 'sink'
0:00:12.388386651  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c084690> adding pad 'src'
0:00:12.401946072  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element conv:src to element resample:sink
0:00:12.416393258  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:src
0:00:12.427910586  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad resample:sink
0:00:12.439879961  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: conv and resample in same bin, no need for ghost pads
0:00:12.454487552  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link conv:src and resample:sink
0:00:12.467231243  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked conv:src and resample:sink, successful
0:00:12.479979310  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:12.492047845  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<conv:src> Received event on flushing pad. Discarding
0:00:12.506521279  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:sink
0:00:12.518070687  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<resample:src> pad has no peer
0:00:12.530294376  2222   0x7fa8004b00 INFO               structure gststructure.c:2633:gst_structure_get_valist: Expected field 'channel-mask' in structure: audio/x-raw, rate=(int)[ 1, 2147483647 ], channels=(int)[ 1, 2147483647 ];
0:00:12.550244017  2222   0x7fa8004b00 INFO      playsinkconvertbin gstplaysinkconvertbin.c:591:gst_play_sink_convert_bin_cache_converter_caps:<aconv> Converter caps: audio/x-raw, format=(string){ S8, U8, S16LE, S16BE, U16LE, U16BE, S24_32LE, S24_32BE, U24_32LE, U24_32BE, S32LE, S32BE, U32LE, U32BE, S24LE, S24BE, U24LE, U24BE, S20LE, S20BE, U20LE, U20BE, S18LE, S18BE, U18LE, U18BE, F32LE, F32BE, F64LE, F64BE }, rate=(int)[ 1, 2147483647 ], channels=(int)[ 1, 2147483647 ], layout=(string){ interleaved, non-interleaved }
0:00:12.595498762  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to NULL
0:00:12.608700919  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking conv:src(0x7f8c0821d0) and resample:sink(0x7f8c082420)
0:00:12.622877459  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked conv:src and resample:sink
0:00:12.634575314  2222   0x7fa8004b00 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<aconv> removed child "conv"
0:00:12.646034020  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<conv> 0x7f8c0807b0 dispose
0:00:12.657663922  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<conv> removing pad 'sink'
0:00:12.669493600  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<conv> removing pad 'src'
0:00:12.681185039  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<conv> 0x7f8c0807b0 parent class dispose
0:00:12.693978310  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<conv> 0x7f8c0807b0 finalize
0:00:12.705846486  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<conv> 0x7f8c0807b0 finalize parent
0:00:12.718307867  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to NULL
0:00:12.731840753  2222   0x7fa8004b00 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<aconv> removed child "resample"
0:00:12.743638645  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<resample> 0x7f8c084690 dispose
0:00:12.755621440  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<resample> removing pad 'sink'
0:00:12.767789138  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<resample> removing pad 'src'
0:00:12.779823554  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<resample> 0x7f8c084690 parent class dispose
0:00:12.792975843  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<resample> 0x7f8c084690 finalize
0:00:12.805189912  2222   0x7fa8004b00 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<resample> 0x7f8c084690 finalize parent
0:00:12.818068347  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "audioconvert" named "conv"
0:00:12.832591657  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c0807b0> adding pad 'sink'
0:00:12.845998260  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c0807b0> adding pad 'src'
0:00:12.859483316  2222   0x7fa8004b00 INFO     GST_ELEMENT_FACTORY gstelementfactory.c:360:gst_element_factory_create: creating element "audioresample" named "resample"
0:00:12.874238774  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c084670> adding pad 'sink'
0:00:12.887753286  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<GstBaseTransform@0x7f8c084670> adding pad 'src'
0:00:12.901239216  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element conv:src to element resample:sink
0:00:12.915866935  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:src
0:00:12.927403222  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad resample:sink
0:00:12.939345770  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: conv and resample in same bin, no need for ghost pads
0:00:12.953944907  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link conv:src and resample:sink
0:00:12.966690353  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked conv:src and resample:sink, successful
0:00:12.979462046  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:12.991539917  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<conv:src> Received event on flushing pad. Discarding
0:00:13.006036979  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element resample:src to element volume:sink
0:00:13.020804395  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad resample:src
0:00:13.032699697  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad volume:sink
0:00:13.044462592  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: resample and volume in same bin, no need for ghost pads
0:00:13.059229133  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link resample:src and volume:sink
0:00:13.072144023  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked resample:src and volume:sink, successful
0:00:13.085104119  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:13.097158367  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<resample:src> Received event on flushing pad. Discarding
0:00:13.111934532  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:sink
0:00:13.123547814  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<volume:src> pad has no peer
0:00:13.135242464  2222   0x7fa8004b00 INFO               structure gststructure.c:2633:gst_structure_get_valist: Expected field 'channel-mask' in structure: audio/x-raw, rate=(int)[ 1, 2147483647 ], channels=(int)[ 1, 2147483647 ];
0:00:13.155416093  2222   0x7fa8004b00 INFO      playsinkconvertbin gstplaysinkconvertbin.c:591:gst_play_sink_convert_bin_cache_converter_caps:<aconv> Converter caps: audio/x-raw, format=(string){ F32LE, F64LE, S8, S16LE, S24LE, S32LE }, rate=(int)[ 1, 2147483647 ], channels=(int)[ 1, 2147483647 ], layout=(string)interleaved; audio/x-raw, rate=(int)[ 1, 2147483647 ], format=(string){ S8, U8, S16LE, S16BE, U16LE, U16BE, S24_32LE, S24_32BE, U24_32LE, U24_32BE, S32LE, S32BE, U32LE, U32BE, S24LE, S24BE, U24LE, U24BE, S20LE, S20BE, U20LE, U20BE, S18LE, S18BE, U18LE, U18BE, F32LE, F32BE, F64LE, F64BE }, channels=(int)[ 1, 2147483647 ], layout=(string){ interleaved, non-interleaved }
0:00:13.214906892  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element aqueue:src to element aconv:sink
0:00:13.229338042  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad aqueue:src
0:00:13.241009361  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad aconv:sink
0:00:13.252711886  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: aqueue and aconv in same bin, no need for ghost pads
0:00:13.267225571  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link aqueue:src and aconv:sink
0:00:13.279867774  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked aqueue:src and aconv:sink, successful
0:00:13.292563640  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:13.304633345  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<aqueue:src> Received event on flushing pad. Discarding
0:00:13.319456757  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstutils.c:1771:gst_element_link_pads_full: trying to link element aconv:src to element alsasink0:(any)
0:00:13.334207258  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad aconv:src
0:00:13.345812956  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1034:gst_pad_check_link: trying to link aconv:src and alsasink0:sink
0:00:13.358739513  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<aqueue:sink> pad has no peer
0:00:13.370202598  2222   0x7fa8004b00 INFO                GST_PADS gstutils.c:1587:prepare_link_maybe_ghosting: aconv and alsasink0 in same bin, no need for ghost pads
0:00:13.384918684  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link aconv:src and alsasink0:sink
0:00:13.397787495  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked aconv:src and alsasink0:sink, successful
0:00:13.410763631  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:13.422828378  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<aconv:src> Received event on flushing pad. Discarding
0:00:13.437362479  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad aqueue:sink
0:00:13.449244948  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad15 and aqueue:sink
0:00:13.462253165  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad15 and aqueue:sink, successful
0:00:13.475496447  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:13.487597942  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<abin> adding pad 'sink'
0:00:13.499120813  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<streamsynchronizer0> adding pad 'src_1'
0:00:13.511671440  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<streamsynchronizer0> adding pad 'sink_1'
0:00:13.524646701  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:671:gst_element_add_pad:<audiotee> adding pad 'src_0'
0:00:13.536577000  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<alsasink0> current READY pending VOID_PENDING, desired next READY
0:00:13.551532818  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<alsasink0> skipping transition from READY to  READY
0:00:13.565549542  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'alsasink0' changed state to 2(READY) successfully
0:00:13.580557565  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aconv> current NULL pending VOID_PENDING, desired next READY
0:00:13.595419765  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<volume> current NULL pending VOID_PENDING, desired next READY
0:00:13.610279049  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to READY
0:00:13.623693527  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<volume> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:13.625947647  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:13.640720021  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'volume' changed state to 2(READY) successfully
0:00:13.667200461  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<resample> current NULL pending VOID_PENDING, desired next READY
0:00:13.682215191  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to READY
0:00:13.695806989  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<resample> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:13.712987471  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'resample' changed state to 2(READY) successfully
0:00:13.727898089  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current NULL pending VOID_PENDING, desired next READY
0:00:13.742607472  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to READY
0:00:13.755866508  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:13.726436367  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:13.772663482  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'conv' changed state to 2(READY) successfully
0:00:13.799019981  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current NULL pending VOID_PENDING, desired next READY
0:00:13.814018676  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to READY
0:00:13.827627684  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:13.827141221  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:13.844788923  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'identity' changed state to 2(READY) successfully
0:00:13.871469731  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aconv> completed state change to READY
0:00:13.884733432  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aconv> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:13.901672146  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aconv' changed state to 2(READY) successfully
0:00:13.916218792  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aqueue> current NULL pending VOID_PENDING, desired next READY
0:00:13.931106953  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aqueue> completed state change to READY
0:00:13.944522893  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aqueue> notifying about state-changed NULL to READY (VOID_PENDING pending)
0:00:13.928122554  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:13.961500395  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aqueue' changed state to 2(READY) successfully
0:00:13.987944096  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<abin> committing state from NULL to READY, pending PAUSED, next PAUSED
0:00:14.003968796  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<abin> notifying about state-changed NULL to READY (PAUSED pending)
0:00:14.020271433  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<abin> continue state change READY to PAUSED, final PAUSED
0:00:14.028740499  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:14.035247671  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<alsasink0> current READY pending VOID_PENDING, desired next PAUSED
0:00:14.062403276  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2959:gst_bin_change_state_func:<abin> child 'alsasink0' is changing state asynchronously to PAUSED
0:00:14.077579874  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aconv> current READY pending VOID_PENDING, desired next PAUSED
0:00:14.092571861  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:sink
0:00:14.104514121  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad13 and identity:sink
0:00:14.117860941  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad13 and identity:sink, successful
0:00:14.131276589  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:14.129660878  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:14.143370796  2222   0x7fa8004b00 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:src
0:00:14.166998960  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link identity:src and src:proxypad14
0:00:14.180092633  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked identity:src and src:proxypad14, successful
0:00:14.193306171  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:14.205376755  2222   0x7fa8004b00 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<identity:src> Received event on flushing pad. Discarding
0:00:14.220340744  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<volume> current READY pending VOID_PENDING, desired next PAUSED
0:00:14.229922725  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<abin:sink> pad has no peer
0:00:14.235244362  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to PAUSED
0:00:14.260001774  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<volume> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:14.277181387  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'volume' changed state to 3(PAUSED) successfully
0:00:14.291997220  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<resample> current READY pending VOID_PENDING, desired next PAUSED
0:00:14.307237396  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to PAUSED
0:00:14.320889860  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<resample> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:14.330677742  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<abin:sink> pad has no peer
0:00:14.338257291  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'resample' changed state to 3(PAUSED) successfully
0:00:14.364555753  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current READY pending VOID_PENDING, desired next PAUSED
0:00:14.379423208  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PAUSED
0:00:14.392727156  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:14.409753363  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'conv' changed state to 3(PAUSED) successfully
0:00:14.424402376  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current READY pending VOID_PENDING, desired next PAUSED
0:00:14.431230941  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<abin:sink> pad has no peer
0:00:14.439674342  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to PAUSED
0:00:14.464601491  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:14.481949965  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'identity' changed state to 3(PAUSED) successfully
0:00:14.496966742  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aconv> completed state change to PAUSED
0:00:14.510328727  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aconv> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:14.527398681  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aconv' changed state to 3(PAUSED) successfully
0:00:14.531771599  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<abin:sink> pad has no peer
0:00:14.542079483  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aqueue> current READY pending VOID_PENDING, desired next PAUSED
0:00:14.568548557  2222   0x7fa8004b00 INFO                    task gsttask.c:460:gst_task_set_lock: setting stream lock 0x7f8c0231f0 on task 0x7f8c075050
0:00:14.581902668  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:6159:gst_pad_start_task:<aqueue:src> created task 0x7f8c075050
0:00:14.594671157  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aqueue> completed state change to PAUSED
0:00:14.607675878  2222   0x7fa8004b00 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aqueue> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:14.624903029  2222   0x7fa8004b00 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aqueue' changed state to 3(PAUSED) successfully
0:00:14.632382544  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<abin:sink> pad has no peer
0:00:14.650998797  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link audiotee:src_0 and streamsynchronizer0:sink_1
0:00:14.665220259  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked audiotee:src_0 and streamsynchronizer0:sink_1, successful
0:00:14.679640623  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:14.691962896  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link streamsynchronizer0:src_1 and abin:sink
0:00:14.705572487  2222   0x7fa8004b00 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked streamsynchronizer0:src_1 and abin:sink, successful
0:00:14.719504640  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:14.731840332  2222   0x7fa8004b00 INFO                playsink gstplaysink.c:1451:do_async_done:<playsink> Sending async_done message
0:00:14.745218362  2222   0x7f8c010ea0 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad13(0x7f8c009870) and identity:sink(0x7f8c0233d0)
0:00:14.758217254  2222   0x7fa8004b00 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<vdconv> reuse caps
0:00:14.758603100  2222   0x7f8c010ea0 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad13 and identity:sink
0:00:14.771438962  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-raw, format=(string)NV12, width=(int)1920, height=(int)1084, interlace-mode=(string)progressive, multiview-mode=(string)mono, multiview-flags=(GstVideoMultiviewFlagsSet)0:ffffffff:/right-view-first/left-flipped/left-flopped/right-flipped/right-flopped/half-aspect/mixed-mono, pixel-aspect-ratio=(fraction)1/1, chroma-site=(string)mpeg2, colorimetry=(string)bt709, framerate=(fraction)24000/1001, arm-afbc=(int)1
0:00:14.783023670  2222   0x7f8c010ea0 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking identity:src(0x7f8c023620) and src:proxypad14(0x7f8c009ad0)
0:00:14.832502928  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-raw, format=(string)NV12, width=(int)1920, height=(int)1084, interlace-mode=(string)progressive, multiview-mode=(string)mono, multiview-flags=(GstVideoMultiviewFlagsSet)0:ffffffff:/right-view-first/left-flipped/left-flopped/right-flipped/right-flopped/half-aspect/mixed-mono, pixel-aspect-ratio=(fraction)1/1, chroma-site=(string)mpeg2, colorimetry=(string)bt709, framerate=(fraction)24000/1001, arm-afbc=(int)1
0:00:14.832883524  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<identity:sink> pad has no peer
0:00:14.844833078  2222   0x7f8c010ea0 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked identity:src and src:proxypad14
0:00:14.892544970  2222   0x7f8c010cc0 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad8(0x7f8c0087d0) and identity:sink(0x7fa8171190)
0:00:14.915872456  2222   0x7f8c010ea0 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PAUSED
0:00:14.930402191  2222   0x7f8c010cc0 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad8 and identity:sink
0:00:14.933367050  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:14.943754847  2222   0x7f8c010ea0 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to PAUSED
0:00:14.955999255  2222   0x7f8c010cc0 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking identity:src(0x7fa81713e0) and src:proxypad9(0x7f8c008a30)
0:00:14.967731826  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<identity:sink> pad has no peer
0:00:14.981353379  2222   0x7f8c010ea0 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to PAUSED
0:00:14.995960108  2222   0x7f8c010cc0 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked identity:src and src:proxypad9
0:00:15.021056418  2222   0x7f8c010ea0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:sink
0:00:15.033231997  2222   0x7f8c010cc0 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PAUSED
0:00:15.033897530  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:15.044709379  2222   0x7f8c010ea0 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad13 and conv:sink
0:00:15.082747128  2222   0x7f8c010ea0 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad13 and conv:sink, successful
0:00:15.095786850  2222   0x7f8c010ea0 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:15.058047745  2222   0x7f8c010cc0 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to PAUSED
0:00:15.069805981  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:15.108128083  2222   0x7f8c010ea0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad volume:src
0:00:15.121310128  2222   0x7f8c010cc0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad conv:sink
0:00:15.134239317  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad14> pad has no peer
0:00:15.156283275  2222   0x7f8c010cc0 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad8 and conv:sink
0:00:15.168008846  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:15.168056676  2222   0x7f8c010ea0 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link volume:src and src:proxypad14
0:00:15.180836543  2222   0x7f8c010cc0 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad8 and conv:sink, successful
0:00:15.205471763  2222   0x7f8c010ea0 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked volume:src and src:proxypad14, successful
0:00:15.218469197  2222   0x7f8c010cc0 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:15.231527293  2222   0x7f8c010ea0 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:15.235349004  2222   0x558c507200 INFO                GST_PADS gstpad.c:4237:gst_pad_peer_query:<src:proxypad9> pad has no peer
0:00:15.243972643  2222   0x7f8c010cc0 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad scale:src
0:00:15.265466559  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:1357:gst_audio_converter_new: unitsizes: 8 -> 8
0:00:15.278941707  2222   0x7f8c010cc0 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link scale:src and src:proxypad9
0:00:15.290546246  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:726:chain_unpack: unpack format F32LE to F32LE
0:00:15.303389400  2222   0x7f8c010cc0 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked scale:src and src:proxypad9, successful
0:00:15.327877339  2222   0x7f8c010cc0 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:15.315100389  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:868:chain_mix: mix format F32LE, passthrough 1, in_channels 2, out_channels 2
0:00:15.347091178  2222   0x7f8c010cc0 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<conv> reuse caps
0:00:15.354310257  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:962:chain_quantize: depth in 32, out 32
0:00:15.377187735  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:974:chain_quantize: using no dither and noise shaping
0:00:15.389415227  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:1031:chain_pack: pack format F32LE to F32LE
0:00:15.366653823  2222   0x7f8c010cc0 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-raw, format=(string)NV12, width=(int)1920, height=(int)1084, interlace-mode=(string)progressive, multiview-mode=(string)mono, multiview-flags=(GstVideoMultiviewFlagsSet)0:ffffffff:/right-view-first/left-flipped/left-flopped/right-flipped/right-flopped/half-aspect/mixed-mono, pixel-aspect-ratio=(fraction)1/1, chroma-site=(string)mpeg2, colorimetry=(string)bt709, framerate=(fraction)24000/1001, arm-afbc=(int)1
0:00:15.400830489  2222   0x7f8c010ea0 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event audio/x-raw, rate=(int)48000, format=(string)F32LE, channels=(int)2, layout=(string)interleaved, channel-mask=(bitmask)0x0000000000000003
0:00:15.448619958  2222   0x7f8c010cc0 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<scale> reuse caps
0:00:15.471361821  2222   0x7f8c010ea0 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<resample> reuse caps
0:00:15.482880909  2222   0x7f8c010cc0 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event video/x-raw, format=(string)NV12, width=(int)1920, height=(int)1084, interlace-mode=(string)progressive, multiview-mode=(string)mono, multiview-flags=(GstVideoMultiviewFlagsSet)0:ffffffff:/right-view-first/left-flipped/left-flopped/right-flipped/right-flopped/half-aspect/mixed-mono, pixel-aspect-ratio=(fraction)1/1, chroma-site=(string)mpeg2, colorimetry=(string)bt709, framerate=(fraction)24000/1001, arm-afbc=(int)1
0:00:15.495146898  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:1357:gst_audio_converter_new: unitsizes: 8 -> 8
0:00:15.553895788  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:726:chain_unpack: unpack format F32LE to F32LE
0:00:15.565558364  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:868:chain_mix: mix format F32LE, passthrough 1, in_channels 2, out_channels 2
0:00:15.580014604  2222   0x7f8c010ea0 INFO         audio-resampler audio-resampler.c:1554:gst_audio_resampler_update: phase 0 out_rate 48000, in_rate 48000, gcd 48000
0:00:15.594414265  2222   0x7f8c010ea0 INFO         audio-resampler audio-resampler.c:1561:gst_audio_resampler_update: new phase 0/1
0:00:15.606047094  2222   0x7f8c010ea0 INFO         audio-resampler audio-resampler.c:1567:gst_audio_resampler_update: have new options, reconfigure filter
0:00:15.619822636  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:962:chain_quantize: depth in 32, out 32
0:00:15.628506354  2222   0x7fa8004b00 INFO                  mppdec gstmppdec.c:913:gst_mpp_dec_loop:<mppvideodec0> video info changed
0:00:15.630593946  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:974:chain_quantize: using no dither and noise shaping
0:00:15.642622828  2222   0x7fa8004b00 WARN                  mppdec gstmppdec.c:562:gst_mpp_dec_get_frame:<mppvideodec0>  is not able to generate pts
0:00:15.654645294  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:1031:chain_pack: pack format F32LE to F32LE
0:00:15.679297138  2222   0x7f8c010ea0 INFO         audio-converter audio-converter.c:1393:gst_audio_converter_new: same formats, and passthrough mixing -> only resampling
0:00:15.682601763  2222   0x7fa8004b00 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<vdconv> reuse caps
0:00:15.694422119  2222   0x7f8c010ea0 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event audio/x-raw, rate=(int)48000, format=(string)F32LE, channels=(int)2, layout=(string)interleaved, channel-mask=(bitmask)0x0000000000000003
0:00:15.710475988  2222   0x7fa8004b00 INFO               GST_EVENT gstevent.c:900:gst_event_new_segment: creating segment event time segment start=0:00:00.000000000, offset=0:00:00.000000000, stop=0:00:10.000000000, rate=1.000000, applied_rate=1.000000, flags=0x00, time=0:00:00.000000000, base=0:00:00.000000000, position 0:00:00.000000000, duration 99:99:99.999999999
0:00:15.729668250  2222   0x7f8c010ea0 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<volume> reuse caps
0:00:15.762412950  2222   0x7fa8004b00 INFO            videodecoder gstvideodecoder.c:3184:gst_video_decoder_clip_and_push_buf:<mppvideodec0> First buffer since flush took 0:00:10.092097973 to produce
0:00:15.773814508  2222   0x7f8c010ea0 INFO               GST_EVENT gstevent.c:820:gst_event_new_caps: creating caps event audio/x-raw, rate=(int)48000, format=(string)F32LE, channels=(int)2, layout=(string)interleaved, channel-mask=(bitmask)0x0000000000000003
0:00:15.818856407  2222   0x7fb01bf8c0 INFO           basetransform gstbasetransform.c:1317:gst_base_transform_setcaps:<capsfilter0> reuse caps
0:00:15.820850381  2222   0x7f8c010ea0 WARN                    alsa pcm_hw.c:1359:snd_pcm_hw_get_chmap: alsalib error: Cannot read Channel Map ctl
: 没有那个文件或目录
0:00:15.842227938  2222   0x7f8c010ea0 INFO              ringbuffer gstaudioringbuffer.c:634:gst_audio_ring_buffer_acquire:<audiosinkringbuffer0> Allocating an array for 20 timestamps
0:00:15.859340773  2222   0x558c507200 INFO               GST_EVENT gstevent.c:1449:gst_event_new_latency: creating latency event 0:00:00.000000000
0:00:15.860163795  2222   0x7fb01bfb00 INFO               GST_EVENT gstevent.c:900:gst_event_new_segment: creating segment event time segment start=0:00:00.000000000, offset=0:00:00.000000000, stop=0:00:09.920000000, rate=1.000000, applied_rate=1.000000, flags=0x00, time=0:00:00.000000000, base=0:00:00.000000000, position 0:00:00.000000000, duration 99:99:99.999999999
0:00:15.870986146  2222   0x558c507200 INFO                     bin gstbin.c:2783:gst_bin_do_latency_func:<playbin> configured latency of 0:00:00.000000000
0:00:15.890799612  2222   0x7f8c010cc0 INFO              GST_STATES gstbin.c:3421:bin_handle_async_done:<vbin> committing state from READY to PAUSED, old pending PAUSED
0:00:15.904736145  2222   0x7f8c010ea0 INFO            audioconvert gstaudioconvert.c:294:gst_audio_convert_get_unit_size:<conv> unit_size = 8
0:00:15.907361239  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)131250, bitrate=(uint)127050;
0:00:15.931406761  2222   0x7f8c010cc0 INFO              GST_STATES gstbin.c:3444:bin_handle_async_done:<vbin> completed state change, pending VOID
0:00:15.943956816  2222   0x7f8c010ea0 INFO            audioconvert gstaudioconvert.c:294:gst_audio_convert_get_unit_size:<conv> unit_size = 8
0:00:15.969491184  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)130875, bitrate=(uint)127397;
0:00:15.981533777  2222   0x7f8c010cc0 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vbin> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:15.994376351  2222   0x7f8c010ea0 INFO              GST_STATES gstbin.c:3421:bin_handle_async_done:<abin> committing state from READY to PAUSED, old pending PAUSED
0:00:16.019557829  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)126749, bitrate=(uint)127343;
0:00:16.050426087  2222   0x7f8c010ea0 INFO              GST_STATES gstbin.c:3444:bin_handle_async_done:<abin> completed state change, pending VOID
0:00:16.076299346  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)126000, bitrate=(uint)127240;
0:00:16.088142454  2222   0x7f8c010ea0 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<abin> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:16.114061210  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)126428;
0:00:16.129961095  2222   0x7f8c010ea0 INFO              GST_STATES gstbin.c:3421:bin_handle_async_done:<playsink> committing state from READY to PAUSED, old pending PAUSED
0:00:16.156634628  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)130855;
0:00:16.169669104  2222   0x7f8c010ea0 INFO              GST_STATES gstbin.c:3444:bin_handle_async_done:<playsink> completed state change, pending VOID
0:00:16.195838091  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)133732;
0:00:16.207742444  2222   0x7f8c010ea0 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playsink> notifying about state-changed READY to PAUSED (VOID_PENDING pending)
0:00:16.234297569  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)136793;
0:00:16.249891228  2222   0x7f8c010ea0 INFO              GST_STATES gstbin.c:3421:bin_handle_async_done:<playbin> committing state from READY to PAUSED, old pending PLAYING
0:00:16.289605069  2222   0x7f8c010ea0 INFO              GST_STATES gstbin.c:3452:bin_handle_async_done:<playbin> continue state change, pending PLAYING
0:00:16.302913983  2222   0x7f8c010ea0 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playbin> notifying about state-changed READY to PAUSED (PLAYING pending)
0:00:16.305281555  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)140030;
0:00:16.320356086  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:3248:gst_bin_continue_func:<playbin> continue state change PAUSED to PLAYING, final PLAYING
0:00:16.347294432  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)143045;
0:00:16.360581764  2222   0x7f8c011520 INFO               GST_EVENT gstevent.c:1449:gst_event_new_latency: creating latency event 0:00:00.000000000
0:00:16.386488271  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)146097;
0:00:16.397472777  2222   0x7f8c011520 INFO                     bin gstbin.c:2783:gst_bin_do_latency_func:<playbin> configured latency of 0:00:00.000000000
0:00:16.424688185  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)149187;
0:00:16.435402919  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<playsink> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.463561215  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)152372;
0:00:16.475617515  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<abin> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.515466971  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<alsasink0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.530850062  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to PLAYING
0:00:16.544686270  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<alsasink0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:16.550681318  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)155758;
0:00:16.562366355  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'alsasink0' changed state to 4(PLAYING) successfully
0:00:16.591795930  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)159208;
0:00:16.602263349  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aconv> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.642274669  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<volume> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.657461774  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to PLAYING
0:00:16.671011295  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<volume> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:16.688515518  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'volume' changed state to 4(PLAYING) successfully
0:00:16.703280323  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<resample> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.718677123  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to PLAYING
0:00:16.732441882  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<resample> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:16.750006481  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'resample' changed state to 4(PLAYING) successfully
0:00:16.765053602  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.780114430  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PLAYING
0:00:16.793549630  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:16.810735090  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'conv' changed state to 4(PLAYING) successfully
0:00:16.825464027  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.840868413  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to PLAYING
0:00:16.854601090  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:16.872189021  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'identity' changed state to 4(PLAYING) successfully
0:00:16.887304386  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aconv> completed state change to PLAYING
0:00:16.898282479  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)162705;
0:00:16.900711005  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aconv> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:16.942852510  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aconv' changed state to 4(PLAYING) successfully
0:00:16.957518451  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aqueue> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:16.972753099  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aqueue> completed state change to PLAYING
0:00:16.986322748  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aqueue> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.003740066  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aqueue' changed state to 4(PLAYING) successfully
0:00:17.018534039  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<abin> completed state change to PLAYING
0:00:17.031945033  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<abin> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.049155866  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'abin' changed state to 4(PLAYING) successfully
0:00:17.064109078  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vbin> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:17.079267898  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<xvimagesink0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:17.094983469  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to PLAYING
0:00:17.109089744  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<xvimagesink0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.110671917  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)1521600;
0:00:17.127452283  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'xvimagesink0' changed state to 4(PLAYING) successfully
0:00:17.137987076  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)166031;
0:00:17.155547883  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)1648560;
0:00:17.169907014  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vconv> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:17.224095781  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)2373120;
0:00:17.237502983  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<scale> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:17.266871613  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)2543280;
0:00:17.280084871  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to PLAYING
0:00:17.309602823  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)3161520;
0:00:17.321142915  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<scale> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.351602296  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)3539040;
0:00:17.366028214  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'scale' changed state to 4(PLAYING) successfully
0:00:17.387824286  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)169548;
0:00:17.394958501  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)3611040;
0:00:17.408399242  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:17.462017552  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)3897600;
0:00:17.475775312  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PLAYING
0:00:17.504620439  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)3947520;
0:00:17.516755195  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.545619571  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)4218000;
0:00:17.561532293  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'conv' changed state to 4(PLAYING) successfully
0:00:17.590415626  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)4464480;
0:00:17.603813787  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:17.632739117  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)4526640;
0:00:17.646755565  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to PLAYING
0:00:17.675591068  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)4651200;
0:00:17.688115461  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.717268859  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)4842240;
0:00:17.733204334  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'identity' changed state to 4(PLAYING) successfully
0:00:17.762039262  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)5029200;
0:00:17.775809275  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vconv> completed state change to PLAYING
0:00:17.804592581  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)5388720;
0:00:17.816863831  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vconv> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.846200971  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)1521600, maximum-bitrate=(uint)9935760;
0:00:17.861740977  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vconv' changed state to 4(PLAYING) successfully
0:00:17.890215723  2222   0x7f8c010cc0 WARN                basesink gstbasesink.c:3003:gst_base_sink_is_too_late:<xvimagesink0> warning: 许多缓冲被丢弃。
0:00:17.904058355  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vqueue> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:17.918463278  2222   0x7f8c010cc0 WARN                basesink gstbasesink.c:3003:gst_base_sink_is_too_late:<xvimagesink0> warning: There may be a timestamping problem, or this computer is too slow.
0:00:17.933361956  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vqueue> completed state change to PLAYING
0:00:17.951174458  2222   0x7f8c010cc0 INFO        GST_ERROR_SYSTEM gstelement.c:2153:gst_element_message_full_with_details:<xvimagesink0> posting message: 许多缓冲被丢弃。
0:00:17.964677907  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vqueue> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:17.980600550  2222   0x7f8c010cc0 INFO        GST_ERROR_SYSTEM gstelement.c:2180:gst_element_message_full_with_details:<xvimagesink0> posted warning message: 许多缓冲被丢弃。
WARNING 许多缓冲被丢弃。
0:00:17.997844637  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vqueue' changed state to 4(PLAYING) successfully
WARNING debug information: gstbasesink.c(3003): gst_base_sink_is_too_late (): /GstPlayBin:playbin/GstPlaySink:playsink/GstBin:vbin/GstXvImageSink:xvimagesink0:
There may be a timestamping problem, or this computer is too slow.
0:00:18.031971169  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vbin> completed state change to PLAYING
0:00:18.065224808  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vbin> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.082498934  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'vbin' changed state to 4(PLAYING) successfully
0:00:18.097429985  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdbin> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.101311486  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)506400, maximum-bitrate=(uint)9935760;
0:00:18.112571603  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<deinterlace> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.155688672  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<deinterlace> completed state change to PLAYING
0:00:18.169705416  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<deinterlace> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.187668115  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'deinterlace' changed state to 4(PLAYING) successfully
0:00:18.202898684  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdconv> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.218401651  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdconv> completed state change to PLAYING
0:00:18.231874477  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdconv> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.239888878  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)506400, maximum-bitrate=(uint)70740480;
0:00:18.249087357  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'vdconv' changed state to 4(PLAYING) successfully
0:00:18.291711546  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdbin> completed state change to PLAYING
0:00:18.305069464  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdbin> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.322303343  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'vdbin' changed state to 4(PLAYING) successfully
0:00:18.337343177  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<streamsynchronizer0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.353680831  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<streamsynchronizer0> completed state change to PLAYING
0:00:18.368434853  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<streamsynchronizer0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.386886932  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'streamsynchronizer0' changed state to 4(PLAYING) successfully
0:00:18.403205337  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<audiotee> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.418708303  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<audiotee> completed state change to PLAYING
0:00:18.432354075  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<audiotee> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.449853059  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'audiotee' changed state to 4(PLAYING) successfully
0:00:18.465187746  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playsink> completed state change to PLAYING
0:00:18.478975257  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playsink> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.496531986  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'playsink' changed state to 4(PLAYING) successfully
0:00:18.511803387  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<inputselector1> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.527704448  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector1> completed state change to PLAYING
0:00:18.542044626  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector1> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.560017533  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'inputselector1' changed state to 4(PLAYING) successfully
0:00:18.567983521  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)166217;
0:00:18.575867265  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<inputselector0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.616536850  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector0> completed state change to PLAYING
0:00:18.630800617  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.648858100  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'inputselector0' changed state to 4(PLAYING) successfully
0:00:18.664646587  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<uridecodebin0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.680543857  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<decodebin0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.696174564  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<avdec_aac0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.711705820  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<avdec_aac0> completed state change to PLAYING
0:00:18.725618743  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<avdec_aac0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.743295343  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'avdec_aac0' changed state to 4(PLAYING) successfully
0:00:18.758984967  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aacparse0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.774499312  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aacparse0> completed state change to PLAYING
0:00:18.788531225  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aacparse0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.805990842  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'aacparse0' changed state to 4(PLAYING) successfully
0:00:18.821700297  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<mppvideodec0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.837345007  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<mppvideodec0> completed state change to PLAYING
0:00:18.851457998  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<mppvideodec0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.869372873  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'mppvideodec0' changed state to 4(PLAYING) successfully
0:00:18.885190820  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<capsfilter0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.900869653  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<capsfilter0> completed state change to PLAYING
0:00:18.914977394  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<capsfilter0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.932672951  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'capsfilter0' changed state to 4(PLAYING) successfully
0:00:18.948436653  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<h264parse0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:18.964044324  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<h264parse0> completed state change to PLAYING
0:00:18.977971245  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<h264parse0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:18.995689551  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'h264parse0' changed state to 4(PLAYING) successfully
0:00:19.011372467  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<multiqueue0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:19.027070548  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<multiqueue0> completed state change to PLAYING
0:00:19.041066298  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<multiqueue0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:19.059102788  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'multiqueue0' changed state to 4(PLAYING) successfully
0:00:19.074645131  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<qtdemux0> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:19.090066149  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<qtdemux0> completed state change to PLAYING
0:00:19.103813126  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<qtdemux0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:19.121315906  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'qtdemux0' changed state to 4(PLAYING) successfully
0:00:19.136859998  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:19.152250686  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<typefind> completed state change to PLAYING
0:00:19.166032660  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<typefind> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:19.183563729  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 4(PLAYING) successfully
0:00:19.199075158  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<decodebin0> completed state change to PLAYING
0:00:19.212985455  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<decodebin0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:19.230677805  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<uridecodebin0> child 'decodebin0' changed state to 4(PLAYING) successfully
0:00:19.246623201  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<source> current PAUSED pending VOID_PENDING, desired next PLAYING
0:00:19.261872149  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<source> completed state change to PLAYING
0:00:19.275488760  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<source> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:19.292915129  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<uridecodebin0> child 'source' changed state to 4(PLAYING) successfully
0:00:19.308537383  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<uridecodebin0> completed state change to PLAYING
0:00:19.308582296  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)162901;
0:00:19.322633458  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<uridecodebin0> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:19.365590135  2222   0x7f8c011520 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'uridecodebin0' changed state to 4(PLAYING) successfully
0:00:19.381051400  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playbin> completed state change to PLAYING
0:00:19.394718466  2222   0x7f8c011520 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playbin> notifying about state-changed PAUSED to PLAYING (VOID_PENDING pending)
0:00:20.807741521  2222   0x7fb01bfb00 INFO            audiodecoder gstaudiodecoder.c:2454:gst_audio_decoder_sink_eventfunc:<avdec_aac0> upstream stream tags: taglist, audio-codec=(string)"MPEG-4\ AAC", maximum-bitrate=(uint)196608, minimum-bitrate=(uint)115875, bitrate=(uint)166273;
0:00:22.062659662  2222   0x7fb01bf8c0 INFO            videodecoder gstvideodecoder.c:1312:gst_video_decoder_sink_event_default:<mppvideodec0> upstream tags: taglist, video-codec=(string)"H.264\ \(Constrained\ Baseline\ Profile\)", bitrate=(uint)6633470, minimum-bitrate=(uint)469920, maximum-bitrate=(uint)70740480;
0:00:24.817822360  2222   0x558c75ff00 INFO                    task gsttask.c:312:gst_task_func:<qtdemux0:sink> Task going to paused
0:00:25.027942993  2222   0x7fb01bfb00 WARN                   libav gstavauddec.c:628:gst_ffmpegauddec_drain:<avdec_aac0> send packet failed, could not drain decoder
0:00:25.036953963  2222   0x7fb01bfb00 WARN            audiodecoder gstaudiodecoder.c:1753:gst_audio_decoder_drain:<avdec_aac0> still 1 frames left after draining
0:00:26.391862816  2222   0x7fa8004b00 INFO                  mppdec gstmppdec.c:897:gst_mpp_dec_loop:<mppvideodec0> got eos
0:00:26.397167849  2222   0x7fa8004b00 INFO                    task gsttask.c:312:gst_task_func:<mppvideodec0:src> Task going to paused
0:00:26.409120649  2222   0x7fa8004b00 INFO                    task gsttask.c:314:gst_task_func:<mppvideodec0:src> Task resume from paused
0:00:26.446126385  2222   0x7f8c010ea0 INFO                    task gsttask.c:312:gst_task_func:<aqueue:src> Task going to paused
0:00:26.562329633  2222   0x7f8c010cc0 INFO                    task gsttask.c:312:gst_task_func:<vqueue:src> Task going to paused
0:00:26.563154406  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<playsink> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.583669337  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<abin> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.598684415  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<alsasink0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.617529092  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to PAUSED
0:00:26.627922172  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<alsasink0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:26.645514231  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'alsasink0' changed state to 3(PAUSED) successfully
0:00:26.660533393  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aconv> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.675719376  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<volume> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.690933065  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to PAUSED
0:00:26.704437712  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<volume> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:26.721754753  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'volume' changed state to 3(PAUSED) successfully
0:00:26.736627221  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<resample> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.752015610  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to PAUSED
0:00:26.765708372  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<resample> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:26.783186694  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'resample' changed state to 3(PAUSED) successfully
0:00:26.798229484  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.813296188  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PAUSED
0:00:26.826635767  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:26.843747199  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'conv' changed state to 3(PAUSED) successfully
0:00:26.858466845  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.873878274  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to PAUSED
0:00:26.887556454  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:26.905025151  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'identity' changed state to 3(PAUSED) successfully
0:00:26.920080190  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aconv> completed state change to PAUSED
0:00:26.933509304  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aconv> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:26.950714062  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aconv' changed state to 3(PAUSED) successfully
0:00:26.965406002  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aqueue> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:26.980630195  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aqueue> completed state change to PAUSED
0:00:26.994140678  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aqueue> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.011444013  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aqueue' changed state to 3(PAUSED) successfully
0:00:27.026240070  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<abin> completed state change to PAUSED
0:00:27.039556901  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<abin> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.056680582  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'abin' changed state to 3(PAUSED) successfully
0:00:27.071667958  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vbin> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.086763244  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<xvimagesink0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.102497817  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to PAUSED
0:00:27.116527137  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<xvimagesink0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.134336186  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'xvimagesink0' changed state to 3(PAUSED) successfully
0:00:27.149653997  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vconv> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.164835318  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<scale> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.179948102  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to PAUSED
0:00:27.193380716  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<scale> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.210603265  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'scale' changed state to 3(PAUSED) successfully
0:00:27.225440444  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.240447944  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to PAUSED
0:00:27.253785190  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.270918787  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'conv' changed state to 3(PAUSED) successfully
0:00:27.285627934  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.301028864  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to PAUSED
0:00:27.314709085  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.332188865  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'identity' changed state to 3(PAUSED) successfully
0:00:27.347221447  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vconv> completed state change to PAUSED
0:00:27.360630729  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vconv> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.377847445  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vconv' changed state to 3(PAUSED) successfully
0:00:27.392564175  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vqueue> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.407783118  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vqueue> completed state change to PAUSED
0:00:27.421304100  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vqueue> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.438595478  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vqueue' changed state to 3(PAUSED) successfully
0:00:27.453387743  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vbin> completed state change to PAUSED
0:00:27.466700783  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vbin> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.483823297  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'vbin' changed state to 3(PAUSED) successfully
0:00:27.498807465  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdbin> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.513990245  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<deinterlace> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.529635574  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<deinterlace> completed state change to PAUSED
0:00:27.543575360  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<deinterlace> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.561295456  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'deinterlace' changed state to 3(PAUSED) successfully
0:00:27.576612684  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdconv> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.591849709  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdconv> completed state change to PAUSED
0:00:27.605360192  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdconv> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.622660319  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'vdconv' changed state to 3(PAUSED) successfully
0:00:27.637531621  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdbin> completed state change to PAUSED
0:00:27.650941486  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdbin> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.668143911  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'vdbin' changed state to 3(PAUSED) successfully
0:00:27.683222573  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<streamsynchronizer0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.699579809  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<streamsynchronizer0> completed state change to PAUSED
0:00:27.714207296  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<streamsynchronizer0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.732620347  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'streamsynchronizer0' changed state to 3(PAUSED) successfully
0:00:27.748893011  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<audiotee> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.764302986  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<audiotee> completed state change to PAUSED
0:00:27.777990794  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<audiotee> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.795446956  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'audiotee' changed state to 3(PAUSED) successfully
0:00:27.810774687  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playsink> completed state change to PAUSED
0:00:27.824442955  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playsink> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.841891534  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'playsink' changed state to 3(PAUSED) successfully
0:00:27.857138479  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<inputselector1> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.873068167  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector1> completed state change to PAUSED
0:00:27.887264897  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector1> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.905251270  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'inputselector1' changed state to 3(PAUSED) successfully
0:00:27.921008596  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<inputselector0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:27.936932160  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector0> completed state change to PAUSED
0:00:27.951131805  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:27.969107388  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'inputselector0' changed state to 3(PAUSED) successfully
0:00:27.984874630  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<uridecodebin0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.000753863  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<decodebin0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.016392781  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<avdec_aac0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.031918831  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<avdec_aac0> completed state change to PAUSED
0:00:28.045766169  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<avdec_aac0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.063410151  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'avdec_aac0' changed state to 3(PAUSED) successfully
0:00:28.079075608  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aacparse0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.094565203  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aacparse0> completed state change to PAUSED
0:00:28.108343129  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aacparse0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.125903408  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'aacparse0' changed state to 3(PAUSED) successfully
0:00:28.141472914  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<mppvideodec0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.157222948  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<mppvideodec0> completed state change to PAUSED
0:00:28.171251690  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<mppvideodec0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.189201899  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'mppvideodec0' changed state to 3(PAUSED) successfully
0:00:28.204928602  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<capsfilter0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.220620308  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<capsfilter0> completed state change to PAUSED
0:00:28.234540849  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<capsfilter0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.252269991  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'capsfilter0' changed state to 3(PAUSED) successfully
0:00:28.268014775  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<h264parse0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.283573199  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<h264parse0> completed state change to PAUSED
0:00:28.297431911  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<h264parse0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.315089016  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'h264parse0' changed state to 3(PAUSED) successfully
0:00:28.330755349  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<multiqueue0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.346406515  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<multiqueue0> completed state change to PAUSED
0:00:28.360351263  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<multiqueue0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.378085946  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'multiqueue0' changed state to 3(PAUSED) successfully
0:00:28.393835980  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<qtdemux0> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.409234873  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<qtdemux0> completed state change to PAUSED
0:00:28.422934930  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<qtdemux0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.440396633  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'qtdemux0' changed state to 3(PAUSED) successfully
0:00:28.455883312  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.471285413  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<typefind> completed state change to PAUSED
0:00:28.484980220  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<typefind> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.502432590  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 3(PAUSED) successfully
0:00:28.517941725  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<decodebin0> completed state change to PAUSED
0:00:28.531773023  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<decodebin0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.549415838  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<uridecodebin0> child 'decodebin0' changed state to 3(PAUSED) successfully
0:00:28.565320736  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<source> current PLAYING pending VOID_PENDING, desired next PAUSED
0:00:28.580563890  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<source> completed state change to PAUSED
0:00:28.594070586  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<source> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.611370134  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<uridecodebin0> child 'source' changed state to 3(PAUSED) successfully
0:00:28.626951014  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<uridecodebin0> completed state change to PAUSED
0:00:28.641042751  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<uridecodebin0> notifying about state-changed PLAYING to PAUSED (VOID_PENDING pending)
0:00:28.658929382  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'uridecodebin0' changed state to 3(PAUSED) successfully
0:00:28.674664542  2222   0x558c507200 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<playbin> committing state from PLAYING to PAUSED, pending NULL, next READY
0:00:28.691045115  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playbin> notifying about state-changed PLAYING to PAUSED (NULL pending)
0:00:28.707713833  2222   0x558c507200 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<playbin> continue state change PAUSED to READY, final NULL
0:00:28.722848207  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<playsink> current PAUSED pending VOID_PENDING, desired next READY
0:00:28.738125488  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<abin> current PAUSED pending VOID_PENDING, desired next READY
0:00:28.752962968  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<alsasink0> current PAUSED pending VOID_PENDING, desired next READY
0:00:28.769417914  2222   0x558c507200 INFO              ringbuffer gstaudioringbuffer.c:728:gst_audio_ring_buffer_release:<audiosinkringbuffer0> Freeing timestamp buffer, 20 entries
0:00:28.785927982  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to READY
0:00:28.797919582  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<alsasink0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:28.815323252  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'alsasink0' changed state to 2(READY) successfully
0:00:28.830267182  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aconv> current PAUSED pending VOID_PENDING, desired next READY
0:00:28.845394557  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<volume> current PAUSED pending VOID_PENDING, desired next READY
0:00:28.860388942  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to READY
0:00:28.873734944  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<volume> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:28.890864759  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'volume' changed state to 2(READY) successfully
0:00:28.905657908  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<resample> current PAUSED pending VOID_PENDING, desired next READY
0:00:28.921001101  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to READY
0:00:28.934480969  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<resample> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:28.951774398  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'resample' changed state to 2(READY) successfully
0:00:28.966746034  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current PAUSED pending VOID_PENDING, desired next READY
0:00:28.981731961  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to READY
0:00:28.994889852  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.011826014  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'conv' changed state to 2(READY) successfully
0:00:29.026458758  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.041747997  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to READY
0:00:29.055278319  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.072580789  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'identity' changed state to 2(READY) successfully
0:00:29.087621253  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:sink
0:00:29.099486279  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad13(0x7f8c009870) and conv:sink(0x7f8c0828c0)
0:00:29.113952493  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad13 and conv:sink
0:00:29.125918136  2222   0x558c507200 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad13 and identity:sink
0:00:29.139258014  2222   0x558c507200 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad13 and identity:sink, successful
0:00:29.152667304  2222   0x558c507200 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:29.164735315  2222   0x558c507200 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<sink:proxypad13> Received event on flushing pad. Discarding
0:00:29.179730283  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:src
0:00:29.191604349  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking volume:src(0x7f8c023ac0) and src:proxypad14(0x7f8c009ad0)
0:00:29.206111685  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked volume:src and src:proxypad14
0:00:29.218149657  2222   0x558c507200 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link identity:src and src:proxypad14
0:00:29.231216263  2222   0x558c507200 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked identity:src and src:proxypad14, successful
0:00:29.244447648  2222   0x558c507200 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:29.256510118  2222   0x558c507200 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<identity:src> Received event on flushing pad. Discarding
0:00:29.271291018  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aconv> completed state change to READY
0:00:29.284592107  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aconv> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.301647552  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aconv' changed state to 2(READY) successfully
0:00:29.316247924  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aqueue> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.331393381  2222   0x7f8c010ea0 INFO                    task gsttask.c:314:gst_task_func:<aqueue:src> Task resume from paused
0:00:29.343190744  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aqueue> completed state change to READY
0:00:29.356341928  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aqueue> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.373466785  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aqueue' changed state to 2(READY) successfully
0:00:29.388272183  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<abin> completed state change to READY
0:00:29.401398868  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<abin> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.418359528  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'abin' changed state to 2(READY) successfully
0:00:29.433237838  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vbin> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.448172727  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<xvimagesink0> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.464149958  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to READY
0:00:29.477689905  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<xvimagesink0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.495335058  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'xvimagesink0' changed state to 2(READY) successfully
0:00:29.510558968  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vconv> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.525660678  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<scale> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.540596150  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to READY
0:00:29.553835410  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<scale> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.570883273  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'scale' changed state to 2(READY) successfully
0:00:29.585590095  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.600552982  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to READY
0:00:29.613723997  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.630662201  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'conv' changed state to 2(READY) successfully
0:00:29.645306319  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.660571642  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to READY
0:00:29.674119464  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.691414934  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'identity' changed state to 2(READY) successfully
0:00:29.706457731  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:sink
0:00:29.718335300  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad8(0x7f8c0087d0) and conv:sink(0x7fa8171ad0)
0:00:29.732759813  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad8 and conv:sink
0:00:29.744583720  2222   0x558c507200 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link sink:proxypad8 and identity:sink
0:00:29.757838732  2222   0x558c507200 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked sink:proxypad8 and identity:sink, successful
0:00:29.771167240  2222   0x558c507200 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:29.783236421  2222   0x558c507200 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<sink:proxypad8> Received event on flushing pad. Discarding
0:00:29.798138650  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:928:gst_element_get_static_pad: found pad identity:src
0:00:29.810008053  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking scale:src(0x7f8c0223a0) and src:proxypad9(0x7f8c008a30)
0:00:29.824352071  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked scale:src and src:proxypad9
0:00:29.836154105  2222   0x558c507200 INFO                GST_PADS gstpad.c:2377:gst_pad_link_prepare: trying to link identity:src and src:proxypad9
0:00:29.849191841  2222   0x558c507200 INFO                GST_PADS gstpad.c:2585:gst_pad_link_full: linked identity:src and src:proxypad9, successful
0:00:29.862333112  2222   0x558c507200 INFO               GST_EVENT gstevent.c:1579:gst_event_new_reconfigure: creating reconfigure event
0:00:29.874398502  2222   0x558c507200 INFO               GST_EVENT gstpad.c:5812:gst_pad_send_event_unchecked:<identity:src> Received event on flushing pad. Discarding
0:00:29.889184072  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vconv> completed state change to READY
0:00:29.902474957  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vconv> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.919512325  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vconv' changed state to 2(READY) successfully
0:00:29.934142157  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vqueue> current PAUSED pending VOID_PENDING, desired next READY
0:00:29.949269828  2222   0x7f8c010cc0 INFO                    task gsttask.c:314:gst_task_func:<vqueue:src> Task resume from paused
0:00:29.961056695  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vqueue> completed state change to READY
0:00:29.974230922  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vqueue> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:29.991356659  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vqueue' changed state to 2(READY) successfully
0:00:30.006137563  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vbin> completed state change to READY
0:00:30.019292833  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vbin> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:30.036251748  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'vbin' changed state to 2(READY) successfully
0:00:30.051133854  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdbin> current PAUSED pending VOID_PENDING, desired next READY
0:00:30.066211070  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<deinterlace> current PAUSED pending VOID_PENDING, desired next READY
0:00:30.081702423  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<deinterlace> completed state change to READY
0:00:30.095473649  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<deinterlace> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:30.113023147  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'deinterlace' changed state to 2(READY) successfully
0:00:30.128251145  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdconv> current PAUSED pending VOID_PENDING, desired next READY
0:00:30.143401272  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdconv> completed state change to READY
0:00:30.156735613  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdconv> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:30.173848225  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'vdconv' changed state to 2(READY) successfully
0:00:30.188711082  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdbin> completed state change to READY
0:00:30.201967553  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdbin> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:30.219083957  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'vdbin' changed state to 2(READY) successfully
0:00:30.234001643  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<streamsynchronizer0> current PAUSED pending VOID_PENDING, desired next READY
0:00:30.250313105  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<streamsynchronizer0> completed state change to READY
0:00:30.264714286  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<streamsynchronizer0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:30.282975691  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'streamsynchronizer0' changed state to 2(READY) successfully
0:00:30.299150663  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<audiotee> current PAUSED pending VOID_PENDING, desired next READY
0:00:30.314447488  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<audiotee> completed state change to READY
0:00:30.327977523  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<audiotee> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:30.345276498  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'audiotee' changed state to 2(READY) successfully
0:00:30.360678316  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<streamsynchronizer0> removing pad 'src_0'
0:00:30.373709928  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking streamsynchronizer0:src_0(0x7f8c009140) and vdbin:sink(0x558c779c00)
0:00:30.389126328  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked streamsynchronizer0:src_0 and vdbin:sink
0:00:30.402035157  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<streamsynchronizer0> removing pad 'sink_0'
0:00:30.415251381  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking video_sink:proxypad7(0x7f8c008570) and streamsynchronizer0:sink_0(0x7f8c008ee0)
0:00:30.431647420  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked video_sink:proxypad7 and streamsynchronizer0:sink_0
0:00:30.445575260  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<streamsynchronizer0> removing pad 'src_1'
0:00:30.458656744  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking streamsynchronizer0:src_1(0x7f8c07a310) and abin:sink(0x7f8c070810)
0:00:30.474061186  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked streamsynchronizer0:src_1 and abin:sink
0:00:30.486879022  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<streamsynchronizer0> removing pad 'sink_1'
0:00:30.500095538  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking audiotee:src_0(0x7f8c07a570) and streamsynchronizer0:sink_1(0x7f8c07a0b0)
0:00:30.515977988  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked audiotee:src_0 and streamsynchronizer0:sink_1
0:00:30.529471859  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<deinterlace> current READY pending VOID_PENDING, desired next NULL
0:00:30.544676525  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<deinterlace> completed state change to NULL
0:00:30.558419169  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<deinterlace> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:30.575800388  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'deinterlace' changed state to 1(NULL) successfully
0:00:30.590939725  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vdconv> current READY pending VOID_PENDING, desired next NULL
0:00:30.605834079  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdconv> completed state change to NULL
0:00:30.619164045  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdconv> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:30.636112461  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vdbin> child 'vdconv' changed state to 1(NULL) successfully
0:00:30.650831244  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vdbin> completed state change to NULL
0:00:30.664041927  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vdbin> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:30.680935805  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking vdbin:src(0x7f8c070090) and vbin:sink(0x558c779980)
0:00:30.694839439  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked vdbin:src and vbin:sink
0:00:30.706266707  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playsink> removed child "vdbin"
0:00:30.718207566  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<xvimagesink0> current READY pending VOID_PENDING, desired next NULL
0:00:30.788129098  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to NULL
0:00:30.796601704  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<xvimagesink0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:30.814171623  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'xvimagesink0' changed state to 1(NULL) successfully
0:00:30.829470494  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vconv> current READY pending VOID_PENDING, desired next NULL
0:00:30.844112287  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<scale> current READY pending VOID_PENDING, desired next NULL
0:00:30.858822617  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to NULL
0:00:30.872095132  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<scale> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:30.889012930  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'scale' changed state to 1(NULL) successfully
0:00:30.903603977  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current READY pending VOID_PENDING, desired next NULL
0:00:30.918275517  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to NULL
0:00:30.931402793  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:30.948196933  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'conv' changed state to 1(NULL) successfully
0:00:30.962698736  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current READY pending VOID_PENDING, desired next NULL
0:00:30.977766041  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to NULL
0:00:30.991262540  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.008393531  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vconv> child 'identity' changed state to 1(NULL) successfully
0:00:31.023284681  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vconv> completed state change to NULL
0:00:31.036502367  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vconv> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.053395084  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vconv' changed state to 1(NULL) successfully
0:00:31.067915260  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<vqueue> current READY pending VOID_PENDING, desired next NULL
0:00:31.082923944  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vqueue> completed state change to NULL
0:00:31.096310201  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vqueue> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.113159171  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<vbin> child 'vqueue' changed state to 1(NULL) successfully
0:00:31.127759550  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<vbin> completed state change to NULL
0:00:31.140851245  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<vbin> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.157703131  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playsink> removed child "vbin"
0:00:31.169476003  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<alsasink0> current READY pending VOID_PENDING, desired next NULL
0:00:31.184780415  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to NULL
0:00:31.198059055  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<alsasink0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.215331494  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'alsasink0' changed state to 1(NULL) successfully
0:00:31.230148275  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aconv> current READY pending VOID_PENDING, desired next NULL
0:00:31.245020177  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<volume> current READY pending VOID_PENDING, desired next NULL
0:00:31.259864664  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to NULL
0:00:31.273190258  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<volume> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.290167844  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'volume' changed state to 1(NULL) successfully
0:00:31.304912588  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<resample> current READY pending VOID_PENDING, desired next NULL
0:00:31.319936145  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to NULL
0:00:31.333415146  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<resample> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.350545846  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'resample' changed state to 1(NULL) successfully
0:00:31.365402290  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<conv> current READY pending VOID_PENDING, desired next NULL
0:00:31.380131577  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to NULL
0:00:31.393284226  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<conv> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.410065825  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'conv' changed state to 1(NULL) successfully
0:00:31.424614875  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<identity> current READY pending VOID_PENDING, desired next NULL
0:00:31.439687137  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<identity> completed state change to NULL
0:00:31.453164096  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<identity> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.470374707  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<aconv> child 'identity' changed state to 1(NULL) successfully
0:00:31.485213652  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aconv> completed state change to NULL
0:00:31.498406257  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aconv> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.515276808  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aconv' changed state to 1(NULL) successfully
0:00:31.529802526  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aqueue> current READY pending VOID_PENDING, desired next NULL
0:00:31.544702425  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aqueue> completed state change to NULL
0:00:31.558039978  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aqueue> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.574984899  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<abin> child 'aqueue' changed state to 1(NULL) successfully
0:00:31.589616776  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<abin> completed state change to NULL
0:00:31.602748135  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<abin> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:31.619579314  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playsink> removed child "abin"
0:00:31.631310188  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playsink> completed state change to READY
0:00:31.644785398  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playsink> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:31.662080294  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'playsink' changed state to 2(READY) successfully
0:00:31.677222551  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<inputselector1> current PAUSED pending VOID_PENDING, desired next READY
0:00:31.693083716  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector1> completed state change to READY
0:00:31.707089429  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector1> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:31.724970538  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'inputselector1' changed state to 2(READY) successfully
0:00:31.740572726  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<inputselector0> current PAUSED pending VOID_PENDING, desired next READY
0:00:31.756411438  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector0> completed state change to READY
0:00:31.770437279  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:31.788280183  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'inputselector0' changed state to 2(READY) successfully
0:00:31.803908618  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<uridecodebin0> current PAUSED pending VOID_PENDING, desired next READY
0:00:31.819751997  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<decodebin0> current PAUSED pending VOID_PENDING, desired next READY
0:00:31.835182988  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<avdec_aac0> current PAUSED pending VOID_PENDING, desired next READY
0:00:31.850967454  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<avdec_aac0> completed state change to READY
0:00:31.864204101  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<avdec_aac0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:31.881694404  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'avdec_aac0' changed state to 2(READY) successfully
0:00:31.897248470  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aacparse0> current PAUSED pending VOID_PENDING, desired next READY
0:00:31.912692294  2222   0x558c507200 INFO               baseparse gstbaseparse.c:4843:gst_base_parse_set_upstream_tags:<aacparse0> upstream tags: (NULL)
0:00:31.926096929  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aacparse0> completed state change to READY
0:00:31.939766378  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aacparse0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:31.957155480  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'aacparse0' changed state to 2(READY) successfully
0:00:31.972644217  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<mppvideodec0> current PAUSED pending VOID_PENDING, desired next READY
0:00:32.023231970  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<mppvideodec0> completed state change to READY
0:00:32.031799364  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<mppvideodec0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:32.049421200  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'mppvideodec0' changed state to 2(READY) successfully
0:00:32.065140921  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<capsfilter0> current PAUSED pending VOID_PENDING, desired next READY
0:00:32.080736984  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<capsfilter0> completed state change to READY
0:00:32.094463596  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<capsfilter0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:32.112037894  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'capsfilter0' changed state to 2(READY) successfully
0:00:32.127700452  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<h264parse0> current PAUSED pending VOID_PENDING, desired next READY
0:00:32.143548205  2222   0x558c507200 INFO               baseparse gstbaseparse.c:4843:gst_base_parse_set_upstream_tags:<h264parse0> upstream tags: (NULL)
0:00:32.156726814  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<h264parse0> completed state change to READY
0:00:32.170486090  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<h264parse0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:32.187948396  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'h264parse0' changed state to 2(READY) successfully
0:00:32.203531335  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<multiqueue0> current PAUSED pending VOID_PENDING, desired next READY
0:00:32.219682983  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<multiqueue0> completed state change to READY
0:00:32.232891923  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<multiqueue0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:32.250438515  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'multiqueue0' changed state to 2(READY) successfully
0:00:32.266101948  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<qtdemux0> current PAUSED pending VOID_PENDING, desired next READY
0:00:32.281651056  2222   0x558c75faa0 INFO                    task gsttask.c:314:gst_task_func:<typefind:sink> Task resume from paused
0:00:32.293413432  2222   0x558c75ff00 INFO                    task gsttask.c:314:gst_task_func:<qtdemux0:sink> Task resume from paused
0:00:32.305296257  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<qtdemux0> removing pad 'video_0'
0:00:32.317469562  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking qtdemux0:video_0(0x558c7732d0) and multiqueue0:sink_0(0x558c773520)
0:00:32.332832892  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked qtdemux0:video_0 and multiqueue0:sink_0
0:00:32.345767393  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<qtdemux0> removing pad 'audio_0'
0:00:32.358015068  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking qtdemux0:audio_0(0x7fa8020c20) and multiqueue0:sink_1(0x7fa8020e70)
0:00:32.373368190  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked qtdemux0:audio_0 and multiqueue0:sink_1
0:00:32.386239404  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<qtdemux0> completed state change to READY
0:00:32.399772071  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<qtdemux0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:32.417072513  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'qtdemux0' changed state to 2(READY) successfully
0:00:32.432511379  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<avdec_aac0> current READY pending VOID_PENDING, desired next READY
0:00:32.447780215  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<avdec_aac0> skipping transition from READY to  READY
0:00:32.461903173  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'avdec_aac0' changed state to 2(READY) successfully
0:00:32.477539192  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<aacparse0> current READY pending VOID_PENDING, desired next READY
0:00:32.492752032  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<aacparse0> skipping transition from READY to  READY
0:00:32.506802662  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'aacparse0' changed state to 2(READY) successfully
0:00:32.522335146  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<mppvideodec0> current READY pending VOID_PENDING, desired next READY
0:00:32.537816009  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<mppvideodec0> skipping transition from READY to  READY
0:00:32.552127371  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'mppvideodec0' changed state to 2(READY) successfully
0:00:32.567920878  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<capsfilter0> current READY pending VOID_PENDING, desired next READY
0:00:32.583324746  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<capsfilter0> skipping transition from READY to  READY
0:00:32.597535491  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'capsfilter0' changed state to 2(READY) successfully
0:00:32.613241504  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<h264parse0> current READY pending VOID_PENDING, desired next READY
0:00:32.628563128  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<h264parse0> skipping transition from READY to  READY
0:00:32.642678504  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'h264parse0' changed state to 2(READY) successfully
0:00:32.658306648  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<multiqueue0> current READY pending VOID_PENDING, desired next READY
0:00:32.673697684  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<multiqueue0> skipping transition from READY to  READY
0:00:32.687921552  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'multiqueue0' changed state to 2(READY) successfully
0:00:32.703628732  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<qtdemux0> current READY pending VOID_PENDING, desired next READY
0:00:32.718770121  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<qtdemux0> skipping transition from READY to  READY
0:00:32.732761843  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'qtdemux0' changed state to 2(READY) successfully
0:00:32.748215004  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current PAUSED pending VOID_PENDING, desired next READY
0:00:32.763459346  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<typefind> completed state change to READY
0:00:32.777015932  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<typefind> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:32.794347585  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 2(READY) successfully
0:00:32.809821452  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<avdec_aac0> completed state change to NULL
0:00:32.823383288  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<avdec_aac0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:32.840697734  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aacparse0> completed state change to NULL
0:00:32.854232738  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<aacparse0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:32.871448024  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<mppvideodec0> completed state change to NULL
0:00:32.885253384  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<mppvideodec0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:32.902724736  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<capsfilter0> completed state change to NULL
0:00:32.916443185  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<capsfilter0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:32.933829668  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<h264parse0> completed state change to NULL
0:00:32.947465873  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<h264parse0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:32.964776528  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<multiqueue0> completed state change to NULL
0:00:32.978494977  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<multiqueue0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:32.996076863  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<qtdemux0> completed state change to NULL
0:00:33.009345011  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<qtdemux0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:33.026522091  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking aacparse0:src(0x7fa8021560) and avdec_aac0:sink(0x7fa8021a00)
0:00:33.041289300  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked aacparse0:src and avdec_aac0:sink
0:00:33.053598808  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking avdec_aac0:src(0x7fa8021c50) and src_1:proxypad3(0x558c7553d0)
0:00:33.068486175  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked avdec_aac0:src and src_1:proxypad3
0:00:33.080861302  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "avdec_aac0"
0:00:33.093330340  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking multiqueue0:src_1(0x7fa80210c0) and aacparse0:sink(0x7fa8021310)
0:00:33.108356239  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked multiqueue0:src_1 and aacparse0:sink
0:00:33.120911312  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "aacparse0"
0:00:33.133243568  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<decodebin0> removing pad 'src_1'
0:00:33.145588072  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking decodebin0:src_1(0x7fb0032b10) and src_1:proxypad5(0x7f8c0080b0)
0:00:33.160686883  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked decodebin0:src_1 and src_1:proxypad5
0:00:33.173294161  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<uridecodebin0> removing pad 'src_1'
0:00:33.185885398  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking uridecodebin0:src_1(0x558c778d00) and inputselector1:sink_0(0x7f8c00e380)
0:00:33.201771070  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked uridecodebin0:src_1 and inputselector1:sink_0
0:00:33.215276034  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking uridecodebin0:src_1(0x558c778d00) and inputselector1:sink_0(0x7f8c00e380)
0:00:33.231040381  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking inputselector1:src(0x7fa8170850) and playsink:audio_sink(0x558c778f80)
0:00:33.246560912  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked inputselector1:src and playsink:audio_sink
0:00:33.259682945  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking audio_sink:proxypad6(0x7f8c008310) and audiotee:sink(0x7fa8170aa0)
0:00:33.274895498  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked audio_sink:proxypad6 and audiotee:sink
0:00:33.287626142  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<playsink> removing pad 'audio_sink'
0:00:33.300364369  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector1> completed state change to NULL
0:00:33.314318177  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector1> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:33.331974141  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playbin> removed child "inputselector1"
0:00:33.344439678  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<inputselector1> removing pad 'sink_0'
0:00:33.357361642  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking capsfilter0:src(0x7fa80202e0) and mppvideodec0:sink(0x7fa8020780)
0:00:33.372421664  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked capsfilter0:src and mppvideodec0:sink
0:00:33.385072689  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking mppvideodec0:src(0x7fa80209d0) and src_0:proxypad2(0x558c754a50)
0:00:33.400126877  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked mppvideodec0:src and src_0:proxypad2
0:00:33.412686909  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "mppvideodec0"
0:00:33.425325101  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking h264parse0:src(0x558c773c10) and capsfilter0:sink(0x7fa8020090)
0:00:33.440264673  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked h264parse0:src and capsfilter0:sink
0:00:33.452743918  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "capsfilter0"
0:00:33.465248828  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking multiqueue0:src_0(0x558c773770) and h264parse0:sink(0x558c7739c0)
0:00:33.480364846  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked multiqueue0:src_0 and h264parse0:sink
0:00:33.493025495  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "h264parse0"
0:00:33.505431828  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<decodebin0> removing pad 'src_0'
0:00:33.517789457  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking decodebin0:src_0(0x7fb0032090) and src_0:proxypad4(0x558c755d50)
0:00:33.532890309  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked decodebin0:src_0 and src_0:proxypad4
0:00:33.545490879  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<uridecodebin0> removing pad 'src_0'
0:00:33.558080367  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking uridecodebin0:src_0(0x558c778a80) and inputselector0:sink_0(0x7f8c00e080)
0:00:33.573967788  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked uridecodebin0:src_0 and inputselector0:sink_0
0:00:33.587358719  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking uridecodebin0:src_0(0x558c778a80) and inputselector0:sink_0(0x7f8c00e080)
0:00:33.603240016  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking inputselector0:src(0x7fa8170600) and playsink:video_sink(0x558c779200)
0:00:33.618775421  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked inputselector0:src and playsink:video_sink
0:00:33.631882580  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<playsink> removing pad 'video_sink'
0:00:33.644550229  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<inputselector0> completed state change to NULL
0:00:33.658520369  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<inputselector0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:33.676167292  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playbin> removed child "inputselector0"
0:00:33.688633413  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<inputselector0> removing pad 'sink_0'
0:00:33.701567918  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "multiqueue0"
0:00:33.714011000  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking typefind:src(0x558c7724f0) and qtdemux0:sink(0x558c772990)
0:00:33.728506399  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked typefind:src and qtdemux0:sink
0:00:33.740541470  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "qtdemux0"
0:00:33.752872271  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<avdec_aac0> completed state change to NULL
0:00:33.766424778  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<aacparse0> completed state change to NULL
0:00:33.780073236  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<mppvideodec0> completed state change to NULL
0:00:33.793892890  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<capsfilter0> completed state change to NULL
0:00:33.807666173  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<h264parse0> completed state change to NULL
0:00:33.821376752  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<multiqueue0> removing pad 'src_1'
0:00:33.833856001  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<multiqueue0> removing pad 'sink_1'
0:00:33.846459199  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<multiqueue0> removing pad 'src_0'
0:00:33.858879243  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<multiqueue0> removing pad 'sink_0'
0:00:33.871484483  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<multiqueue0> completed state change to NULL
0:00:33.885256016  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<qtdemux0> completed state change to NULL
0:00:33.898774983  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<decodebin0> completed state change to READY
0:00:33.912534559  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<decodebin0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:33.930003290  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<uridecodebin0> child 'decodebin0' changed state to 2(READY) successfully
0:00:33.945860968  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<decodebin0> current READY pending VOID_PENDING, desired next READY
0:00:33.961210307  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current READY pending VOID_PENDING, desired next READY
0:00:33.976302414  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<typefind> skipping transition from READY to  READY
0:00:33.990255934  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 2(READY) successfully
0:00:34.005703266  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<decodebin0> completed state change to READY
0:00:34.019475674  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<uridecodebin0> child 'decodebin0' changed state to 2(READY) successfully
0:00:34.035343851  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<source> current PAUSED pending VOID_PENDING, desired next READY
0:00:34.050434208  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<source> completed state change to READY
0:00:34.063838558  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<source> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:34.080951773  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<uridecodebin0> child 'source' changed state to 2(READY) successfully
0:00:34.096497098  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current READY pending VOID_PENDING, desired next READY
0:00:34.111590955  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<typefind> skipping transition from READY to  READY
0:00:34.125535726  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 2(READY) successfully
0:00:34.140978975  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<decodebin0> completed state change to READY
0:00:34.154791921  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking source:src(0x558c772050) and decodebin0:sink(0x558c778080)
0:00:34.169351774  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked source:src and decodebin0:sink
0:00:34.181392678  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<uridecodebin0> removed child "decodebin0"
0:00:34.194189238  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<source> completed state change to NULL
0:00:34.207339564  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<source> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:34.224388325  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<uridecodebin0> removed child "source"
0:00:34.236631632  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<uridecodebin0> completed state change to READY
0:00:34.250593610  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<uridecodebin0> notifying about state-changed PAUSED to READY (VOID_PENDING pending)
0:00:34.268327156  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'uridecodebin0' changed state to 2(READY) successfully
0:00:34.283899021  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<playsink> current READY pending VOID_PENDING, desired next READY
0:00:34.299086496  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<audiotee> current READY pending VOID_PENDING, desired next READY
0:00:34.314195227  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<audiotee> skipping transition from READY to  READY
0:00:34.328150497  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'audiotee' changed state to 2(READY) successfully
0:00:34.343418466  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<streamsynchronizer0> current READY pending VOID_PENDING, desired next READY
0:00:34.359518211  2222   0x558c507200 INFO              GST_STATES gstbin.c:2621:gst_bin_element_set_state:<streamsynchronizer0> skipping transition from READY to  READY
0:00:34.374421623  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'streamsynchronizer0' changed state to 2(READY) successfully
0:00:34.390647650  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playsink> completed state change to READY
0:00:34.404243320  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'playsink' changed state to 2(READY) successfully
0:00:34.419420879  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<uridecodebin0> current READY pending VOID_PENDING, desired next READY
0:00:34.435040574  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<uridecodebin0> completed state change to READY
0:00:34.449040174  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'uridecodebin0' changed state to 2(READY) successfully
0:00:34.464677659  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to NULL
0:00:34.478264580  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to NULL
0:00:34.492177270  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playbin> removed child "uridecodebin0"
0:00:34.504552984  2222   0x558c507200 INFO              GST_STATES gstelement.c:2660:gst_element_continue_state:<playbin> committing state from PAUSED to READY, pending NULL, next NULL
0:00:34.520705516  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playbin> notifying about state-changed PAUSED to READY (NULL pending)
0:00:34.537199858  2222   0x558c507200 INFO              GST_STATES gstelement.c:2668:gst_element_continue_state:<playbin> continue state change READY to NULL, final NULL
0:00:34.552130685  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<playsink> current READY pending VOID_PENDING, desired next NULL
0:00:34.567196835  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<audiotee> current READY pending VOID_PENDING, desired next NULL
0:00:34.582258027  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<audiotee> completed state change to NULL
0:00:34.595762996  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<audiotee> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:34.612881168  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'audiotee' changed state to 1(NULL) successfully
0:00:34.628021980  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<streamsynchronizer0> current READY pending VOID_PENDING, desired next NULL
0:00:34.644049980  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<streamsynchronizer0> completed state change to NULL
0:00:34.658497840  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<streamsynchronizer0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:34.676566196  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playsink> child 'streamsynchronizer0' changed state to 1(NULL) successfully
0:00:34.692709104  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking vconv:src(0x558c779700) and xvimagesink0:sink(0x7fa8020530)
0:00:34.707323203  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked vconv:src and xvimagesink0:sink
0:00:34.719463853  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vbin> removed child "xvimagesink0"
0:00:34.731546758  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking aconv:src(0x7f8c070590) and alsasink0:sink(0x7fa80217b0)
0:00:34.745878547  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked aconv:src and alsasink0:sink
0:00:34.757757300  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<abin> removed child "alsasink0"
0:00:34.769549433  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to NULL
0:00:34.783121192  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to NULL
0:00:34.796973515  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playsink> completed state change to NULL
0:00:34.810497152  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playsink> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:34.827608330  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<playbin> child 'playsink' changed state to 1(NULL) successfully
0:00:34.843367728  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<qtdemux0> 0x7fb01c6190 dispose
0:00:34.854707518  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<qtdemux0> removing pad 'sink'
0:00:34.866861293  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<qtdemux0> 0x7fb01c6190 parent class dispose
0:00:34.879996457  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<qtdemux0> 0x7fb01c6190 finalize
0:00:34.892214686  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<qtdemux0> 0x7fb01c6190 finalize parent
0:00:34.905055287  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<multiqueue0> 0x7fa8017040 dispose
0:00:34.917368010  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<multiqueue0> 0x7fa8017040 parent class dispose
0:00:34.930798320  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<multiqueue0> 0x7fa8017040 finalize
0:00:34.943261823  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<multiqueue0> 0x7fa8017040 finalize parent
0:00:34.956371614  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<h264parse0> 0x7fa801d8f0 dispose
0:00:34.968565928  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<h264parse0> removing pad 'sink'
0:00:34.980905190  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<h264parse0> removing pad 'src'
0:00:34.993110295  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<h264parse0> 0x7fa801d8f0 parent class dispose
0:00:35.006973991  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<h264parse0> 0x7fa801d8f0 finalize
0:00:35.018835828  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<h264parse0> 0x7fa801d8f0 finalize parent
0:00:35.031875916  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<capsfilter0> 0x7fb01c6f60 dispose
0:00:35.044130309  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<capsfilter0> removing pad 'sink'
0:00:35.056555023  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<capsfilter0> removing pad 'src'
0:00:35.068862204  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<capsfilter0> 0x7fb01c6f60 parent class dispose
0:00:35.082263058  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<capsfilter0> 0x7fb01c6f60 finalize
0:00:35.094735311  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<capsfilter0> 0x7fb01c6f60 finalize parent
0:00:35.107842477  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<mppvideodec0> 0x7fa8076420 dispose
0:00:35.120225778  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<mppvideodec0> removing pad 'sink'
0:00:35.132725153  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<mppvideodec0> removing pad 'src'
0:00:35.145117203  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<mppvideodec0> 0x7fa8076420 parent class dispose
0:00:35.158660089  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<mppvideodec0> 0x7fa8076420 finalize
0:00:35.171178713  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<mppvideodec0> 0x7fa8076420 finalize parent
0:00:35.184363749  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<aacparse0> 0x7fa8097be0 dispose
0:00:35.196473486  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<aacparse0> removing pad 'sink'
0:00:35.208721754  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<aacparse0> removing pad 'src'
0:00:35.220930650  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<aacparse0> 0x7fa8097be0 parent class dispose
0:00:35.234154475  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<aacparse0> 0x7fa8097be0 finalize
0:00:35.246398660  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<aacparse0> 0x7fa8097be0 finalize parent
0:00:35.259334630  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<avdec_aac0> 0x7fa816e620 dispose
0:00:35.271552275  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<avdec_aac0> removing pad 'sink'
0:00:35.283876663  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<avdec_aac0> removing pad 'src'
0:00:35.296070977  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<avdec_aac0> 0x7fa816e620 parent class dispose
0:00:35.309506245  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<avdec_aac0> 0x7fa816e620 finalize
0:00:35.321798552  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<avdec_aac0> 0x7fa816e620 finalize parent
0:00:35.334815600  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<inputselector0> 0x7f8c00b030 dispose
0:00:35.347360764  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<inputselector0> removing pad 'src'
0:00:35.359959008  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<inputselector0> 0x7f8c00b030 parent class dispose
0:00:35.373640717  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<inputselector0> 0x7f8c00b030 finalize
0:00:35.386363202  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<inputselector0> 0x7f8c00b030 finalize parent
0:00:35.399715643  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<inputselector1> 0x7f8c00b190 dispose
0:00:35.412257599  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<inputselector1> removing pad 'src'
0:00:35.424880050  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<inputselector1> 0x7f8c00b190 parent class dispose
0:00:35.438538136  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<inputselector1> 0x7f8c00b190 finalize
0:00:35.451256538  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<inputselector1> 0x7f8c00b190 finalize parent
0:00:35.464700847  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking vdconv:src(0x7f8c022840) and deinterlace:sink(0x7f8c022a90)
0:00:35.479315825  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked vdconv:src and deinterlace:sink
0:00:35.491439560  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking deinterlace:src(0x7f8c022ce0) and src:proxypad12(0x7f8c009610)
0:00:35.506319061  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked deinterlace:src and src:proxypad12
0:00:35.518705570  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vdbin> removed child "deinterlace"
0:00:35.530831930  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad11(0x7f8c0093b0) and vdconv:sink(0x7f8c0225f0)
0:00:35.545387703  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad11 and vdconv:sink
0:00:35.557516105  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vdbin> removed child "vdconv"
0:00:35.569151916  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<vdbin> 0x7f8c0131e0 dispose
0:00:35.580903802  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vdbin> removing pad 'sink'
0:00:35.592822510  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vdbin> removing pad 'src'
0:00:35.604609977  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<vdbin> 0x7f8c0131e0 parent class dispose
0:00:35.617484702  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<vdbin> 0x7f8c0131e0 finalize
0:00:35.629434032  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<vdbin> 0x7f8c0131e0 finalize parent
0:00:35.642016527  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<vdconv> 0x7f8c058dd0 dispose
0:00:35.653877781  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vdconv> removing pad 'sink'
0:00:35.665869984  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vdconv> removing pad 'src'
0:00:35.677723946  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<vdconv> 0x7f8c058dd0 parent class dispose
0:00:35.690782699  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<vdconv> 0x7f8c058dd0 finalize
0:00:35.702749820  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<vdconv> 0x7f8c058dd0 finalize parent
0:00:35.715417186  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<deinterlace> 0x7f8c06ab50 dispose
0:00:35.727712413  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<deinterlace> removing pad 'sink'
0:00:35.740135964  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<deinterlace> removing pad 'src'
0:00:35.752432940  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<deinterlace> 0x7f8c06ab50 parent class dispose
0:00:35.765864129  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<deinterlace> 0x7f8c06ab50 finalize
0:00:35.778325303  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<deinterlace> 0x7f8c06ab50 finalize parent
0:00:35.791501301  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking vqueue:src(0x7fa8170f40) and vconv:sink(0x558c779480)
0:00:35.805589570  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked vqueue:src and vconv:sink
0:00:35.817183970  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vbin> removed child "vconv"
0:00:35.828796744  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad10(0x7f8c008c90) and vqueue:sink(0x7fa8170cf0)
0:00:35.843241113  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad10 and vqueue:sink
0:00:35.855371559  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vbin> removed child "vqueue"
0:00:35.866919296  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<vbin> 0x7f8c013040 dispose
0:00:35.878587483  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vbin> removing pad 'sink'
0:00:35.890419575  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<vbin> 0x7f8c013040 parent class dispose
0:00:35.903203310  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<vbin> 0x7f8c013040 finalize
0:00:35.915061942  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<vbin> 0x7f8c013040 finalize parent
0:00:35.927564821  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<vqueue> 0x7f8c00e640 dispose
0:00:35.939417328  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vqueue> removing pad 'sink'
0:00:35.951413325  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vqueue> removing pad 'src'
0:00:35.963264083  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<vqueue> 0x7f8c00e640 parent class dispose
0:00:35.976254595  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<vqueue> 0x7f8c00e640 finalize
0:00:35.988301047  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<vqueue> 0x7f8c00e640 finalize parent
0:00:36.000978330  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to NULL
0:00:36.014174744  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking conv:src(0x7fa8171d20) and scale:sink(0x7f8c022150)
0:00:36.028117481  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked conv:src and scale:sink
0:00:36.039538060  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vconv> removed child "conv"
0:00:36.051002094  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<scale> completed state change to NULL
0:00:36.064325374  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vconv> removed child "scale"
0:00:36.076014852  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad8(0x7f8c0087d0) and identity:sink(0x7fa8171190)
0:00:36.090491593  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad8 and identity:sink
0:00:36.102703992  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking identity:src(0x7fa81713e0) and src:proxypad9(0x7f8c008a30)
0:00:36.117301183  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked identity:src and src:proxypad9
0:00:36.129324595  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<vconv> removed child "identity"
0:00:36.141128981  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<vconv> 0x7fa8190930 dispose
0:00:36.152863955  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vconv> removing pad 'sink'
0:00:36.164772750  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<vconv> removing pad 'src'
0:00:36.176558471  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<vconv> 0x7fa8190930 parent class dispose
0:00:36.189439323  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<videobalance> 0x7f8c01fac0 dispose
0:00:36.201825252  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<videobalance> removing pad 'sink'
0:00:36.214374502  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<videobalance> removing pad 'src'
0:00:36.226755473  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<videobalance> 0x7f8c01fac0 parent class dispose
0:00:36.240484433  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<videobalance> 0x7f8c01fac0 finalize
0:00:36.252795409  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<videobalance> 0x7f8c01fac0 finalize parent
0:00:36.265999697  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<vconv> 0x7fa8190930 finalize
0:00:36.277947864  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<vconv> 0x7fa8190930 finalize parent
0:00:36.290503531  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<identity> 0x7f8c01c1c0 dispose
0:00:36.302533359  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<identity> removing pad 'sink'
0:00:36.314692971  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<identity> removing pad 'src'
0:00:36.326739131  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<identity> 0x7f8c01c1c0 parent class dispose
0:00:36.339890048  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<identity> 0x7f8c01c1c0 finalize
0:00:36.352098072  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<identity> 0x7f8c01c1c0 finalize parent
0:00:36.364941886  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<conv> 0x7f8c04c3a0 dispose
0:00:36.376626697  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<conv> removing pad 'sink'
0:00:36.388426416  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<conv> removing pad 'src'
0:00:36.400159057  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<conv> 0x7f8c04c3a0 parent class dispose
0:00:36.412986830  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<conv> 0x7f8c04c3a0 finalize
0:00:36.424809589  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<conv> 0x7f8c04c3a0 finalize parent
0:00:36.437344258  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<scale> 0x7f8c04d7f0 dispose
0:00:36.449069607  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<scale> removing pad 'sink'
0:00:36.460973444  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<scale> removing pad 'src'
0:00:36.472768206  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<scale> 0x7f8c04d7f0 parent class dispose
0:00:36.485643517  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<scale> 0x7f8c04d7f0 finalize
0:00:36.497598976  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<scale> 0x7f8c04d7f0 finalize parent
0:00:36.510275092  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking aqueue:src(0x7f8c023180) and aconv:sink(0x7f8c070310)
0:00:36.524344112  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked aqueue:src and aconv:sink
0:00:36.535942887  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<abin> removed child "aconv"
0:00:36.547470792  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad15(0x7f8c009d30) and aqueue:sink(0x7f8c022f30)
0:00:36.561996822  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad15 and aqueue:sink
0:00:36.574123185  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<abin> removed child "aqueue"
0:00:36.585679672  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<abin> 0x7f8c013380 dispose
0:00:36.597342901  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<abin> removing pad 'sink'
0:00:36.609179076  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<abin> 0x7f8c013380 parent class dispose
0:00:36.621973601  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<abin> 0x7f8c013380 finalize
0:00:36.633823775  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<abin> 0x7f8c013380 finalize parent
0:00:36.646329862  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<aqueue> 0x7f8c00e940 dispose
0:00:36.658194910  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<aqueue> removing pad 'sink'
0:00:36.670169326  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<aqueue> removing pad 'src'
0:00:36.682035832  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<aqueue> 0x7f8c00e940 parent class dispose
0:00:36.695027802  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<aqueue> 0x7f8c00e940 finalize
0:00:36.707061130  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<aqueue> 0x7f8c00e940 finalize parent
0:00:36.719748624  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<conv> completed state change to NULL
0:00:36.732937167  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking conv:src(0x7f8c082670) and resample:sink(0x7f8c082420)
0:00:36.747147348  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked conv:src and resample:sink
0:00:36.758819329  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<aconv> removed child "conv"
0:00:36.770292991  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<resample> completed state change to NULL
0:00:36.783794471  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking resample:src(0x7f8c0821d0) and volume:sink(0x7f8c023870)
0:00:36.798191305  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked resample:src and volume:sink
0:00:36.810043232  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<aconv> removed child "resample"
0:00:36.821839455  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<volume> completed state change to NULL
0:00:36.835167405  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<aconv> removed child "volume"
0:00:36.846848719  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad13(0x7f8c009870) and identity:sink(0x7f8c0233d0)
0:00:36.861595821  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad13 and identity:sink
0:00:36.873891342  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking identity:src(0x7f8c023620) and src:proxypad14(0x7f8c009ad0)
0:00:36.888559116  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked identity:src and src:proxypad14
0:00:36.900680233  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<aconv> removed child "identity"
0:00:36.912477331  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<aconv> 0x7fa8190b30 dispose
0:00:36.924235931  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<aconv> removing pad 'sink'
0:00:36.936142396  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<aconv> removing pad 'src'
0:00:36.947922287  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<aconv> 0x7fa8190b30 parent class dispose
0:00:36.960819475  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<aconv> 0x7fa8190b30 finalize
0:00:36.972758605  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<aconv> 0x7fa8190b30 finalize parent
0:00:36.985345773  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<identity> 0x7f8c01c580 dispose
0:00:36.997372397  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<identity> removing pad 'sink'
0:00:37.009524428  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<identity> removing pad 'src'
0:00:37.021574675  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<identity> 0x7f8c01c580 parent class dispose
0:00:37.034723554  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<identity> 0x7f8c01c580 finalize
0:00:37.046949372  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<identity> 0x7f8c01c580 finalize parent
0:00:37.059801938  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<conv> 0x7f8c0807b0 dispose
0:00:37.071471295  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<conv> removing pad 'sink'
0:00:37.083274518  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<conv> removing pad 'src'
0:00:37.094979455  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<conv> 0x7f8c0807b0 parent class dispose
0:00:37.107781858  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<conv> 0x7f8c0807b0 finalize
0:00:37.119656242  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<conv> 0x7f8c0807b0 finalize parent
0:00:37.132157375  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<resample> 0x7f8c084670 dispose
0:00:37.144181373  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<resample> removing pad 'sink'
0:00:37.156338946  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<resample> removing pad 'src'
0:00:37.168380444  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<resample> 0x7f8c084670 parent class dispose
0:00:37.181541864  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<resample> 0x7f8c084670 finalize
0:00:37.193744642  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<resample> 0x7f8c084670 finalize parent
0:00:37.206584667  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<volume> 0x7f8c07d300 dispose
0:00:37.218489382  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<volume> removing pad 'sink'
0:00:37.230464676  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<volume> removing pad 'src'
0:00:37.242308729  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<volume> 0x7f8c07d300 parent class dispose
0:00:37.255306535  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<volume> 0x7f8c07d300 finalize
0:00:37.267321785  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<volume> 0x7f8c07d300 finalize parent
0:00:37.280147228  2222   0x558c507200 INFO              GST_STATES gstbin.c:2503:gst_bin_element_set_state:<typefind> current READY pending VOID_PENDING, desired next NULL
0:00:37.295091482  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<typefind> completed state change to NULL
0:00:37.308576630  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<typefind> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:37.325726023  2222   0x558c507200 INFO              GST_STATES gstbin.c:2952:gst_bin_change_state_func:<decodebin0> child 'typefind' changed state to 1(NULL) successfully
0:00:37.341023752  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<decodebin0> completed state change to NULL
0:00:37.354679805  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<decodebin0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:37.372030434  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2132:gst_pad_unlink: unlinking sink:proxypad0(0x558c754330) and typefind:sink(0x558c7722a0)
0:00:37.386676625  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstpad.c:2187:gst_pad_unlink: unlinked sink:proxypad0 and typefind:sink
0:00:37.398882320  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<decodebin0> removed child "typefind"
0:00:37.411171717  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<typefind> 0x558c76f070 dispose
0:00:37.423140011  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<typefind> removing pad 'sink'
0:00:37.435313041  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<typefind> removing pad 'src'
0:00:37.447343748  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<typefind> 0x558c76f070 parent class dispose
0:00:37.460492919  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<typefind> 0x558c76f070 finalize
0:00:37.472703279  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<typefind> 0x558c76f070 finalize parent
0:00:37.485531639  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<decodebin0> 0x558c774020 dispose
0:00:37.497750166  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<decodebin0> removing pad 'sink'
0:00:37.510132015  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<decodebin0> 0x558c774020 parent class dispose
0:00:37.523443633  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<decodebin0> 0x558c774020 finalize
0:00:37.535796609  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<decodebin0> 0x558c774020 finalize parent
0:00:37.548808414  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<uridecodebin0> completed state change to NULL
0:00:37.562741530  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<uridecodebin0> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:37.580308561  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<uridecodebin0> 0x558c7540a0 dispose
0:00:37.592732990  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<uridecodebin0> 0x558c7540a0 parent class dispose
0:00:37.606345587  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<uridecodebin0> 0x558c7540a0 finalize
0:00:37.618995167  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<uridecodebin0> 0x558c7540a0 finalize parent
0:00:37.632262163  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<source> 0x558c76c120 dispose
0:00:37.644125173  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<source> removing pad 'src'
0:00:37.656022306  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<source> 0x558c76c120 parent class dispose
0:00:37.668996780  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<source> 0x558c76c120 finalize
0:00:37.681037403  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<source> 0x558c76c120 finalize parent
0:00:37.693695441  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<playbin> completed state change to NULL
0:00:37.707128092  2222   0x558c507200 INFO              GST_STATES gstelement.c:2588:_priv_gst_element_state_changed:<playbin> notifying about state-changed READY to NULL (VOID_PENDING pending)
0:00:37.724211285  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playbin> removed child "playsink"
0:00:37.736152751  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<alsasink0> completed state change to NULL
0:00:37.749680483  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<alsasink0> 0x7fa80b2b80 dispose
0:00:37.761804519  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<alsasink0> removing pad 'sink'
0:00:37.774054839  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<alsasink0> 0x7fa80b2b80 parent class dispose
0:00:37.787293840  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<alsasink0> 0x7fa80b2b80 finalize
0:00:37.799580033  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<alsasink0> 0x7fa80b2b80 finalize parent
0:00:37.812511347  2222   0x558c507200 INFO              GST_STATES gstelement.c:2688:gst_element_continue_state:<xvimagesink0> completed state change to NULL
0:00:37.826368639  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<xvimagesink0> 0x7fa8041ce0 dispose
0:00:37.838758074  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<xvimagesink0> removing pad 'sink'
0:00:37.851267376  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<xvimagesink0> 0x7fa8041ce0 parent class dispose
0:00:37.864775858  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<xvimagesink0> 0x7fa8041ce0 finalize
0:00:37.877315200  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<xvimagesink0> 0x7fa8041ce0 finalize parent
0:00:37.890517745  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<audiotee> removing pad 'src_0'
0:00:37.902780606  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playsink> removed child "audiotee"
0:00:37.914807524  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<audiotee> 0x7fa8080690 dispose
0:00:37.926805278  2222   0x558c507200 INFO        GST_ELEMENT_PADS gstelement.c:787:gst_element_remove_pad:<audiotee> removing pad 'sink'
0:00:37.938975103  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<audiotee> 0x7fa8080690 parent class dispose
0:00:37.952113487  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<audiotee> 0x7fa8080690 finalize
0:00:37.964328226  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<audiotee> 0x7fa8080690 finalize parent
0:00:37.977190420  2222   0x558c507200 INFO           GST_PARENTAGE gstbin.c:1801:gst_bin_remove_func:<playsink> removed child "streamsynchronizer0"
0:00:37.990185896  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<streamsynchronizer0> 0x558c75e0b0 dispose
0:00:38.003150458  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3309:gst_element_dispose:<streamsynchronizer0> 0x558c75e0b0 parent class dispose
0:00:38.017282773  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3341:gst_element_finalize:<streamsynchronizer0> 0x558c75e0b0 finalize
0:00:38.030454404  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3346:gst_element_finalize:<streamsynchronizer0> 0x558c75e0b0 finalize parent
0:00:38.044239076  2222   0x558c507200 INFO         GST_REFCOUNTING gstelement.c:3264:gst_element_dispose:<playsink> 0x558c75c110 dispose
~~~





~~~shell

            if [[ -c /dev/mpp_service ]]; then
                chmod 0666 /dev/mpp_service

                if [[ $DISTRIBUTION_CODENAME =~ bullseye|bookworm|jammy ]]; then
                    {
                        echo "type=dec"
                        echo "codecs=VP8:VP9:H.264:H.265:AV1"
                        echo "max-width=7680"
                        echo "max-height=4320"
                    } > /dev/video-dec0
                else
                    echo dec > /dev/video-dec0
                fi

                # Create dummy video node for chromium V4L2 VDA/VEA with rkmpp plugin
                echo enc > /dev/video-enc0
                chmod 0660 /dev/video-*
                chown root:video /dev/video-*
            fi
~~~

