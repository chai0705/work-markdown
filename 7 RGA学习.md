## RGA库版本号的查询

~~~
    strings /usr/lib/aarch64-linux-gnu/librga.so |grep rga_api |grep version
~~~

![image-20231127102821791](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311271028831.png)

RGA驱动版本号查询

## **版本号格式**

```
<driver_name>: v major.minor.revision
```

例如：

> RGA2 Device Driver: v2.1.0
>
> RGA multicore Device Driver: v1.2.23



## **递增规则**

| 名称     | 规则                                                   |
| -------- | ------------------------------------------------------ |
| major    | 主版本号，当提交不向下兼容的版本。                     |
| minor    | 次版本号，当向下兼容的功能性API新增。                  |
| revision | 修订版本号，当提交向下兼容的功能补充或致命的问题修正。 |

~~~shell
 dmesg |grep rga
~~~

![image-20231127103055998](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311271030046.png)

上面的打印说明RGA驱动的版本号为3.2.6618，也可以在命令行输入以下命令查看驱动的版本号，

~~~
cat /sys/kernel/debug/rkrga/driver_version
~~~

![image-20231127103453089](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202311271034106.png)

这里 “RGA2 Device Driver” 是指驱动名称为RGA2 Device Driver，“v2.1.0” 是指版本号为2.1.0，即说明当前驱动为2.1.0版本的RGA2 Device Driver（通常简称rga2 driver）驱动。

## 版本对应关系

使用RGA时需要确认保证当前的运行环境是可以正常工作的，下表为常用的librga与驱动版本对应关系。

| librga版本    | 对应驱动                                                     | 硬件支持         |
| ------------- | ------------------------------------------------------------ | ---------------- |
| 无版本号      | 对应SDK内驱动                                                | RGA1、RGA2       |
| 1.0.0 ~ 1.3.2 | RGA Device Driver（kernel - 4.4及以上）<br/>RGA2 Device Driver（无版本号或v2.1.0） | RGA1、RGA2       |
| > 1.4.0       | RGA multicore Device Driver（v1.2.0及以上）                  | RGA2、RGA3       |
| > 1.9.0       | RGA Device Driver（kernel-4.4及以上）<br/>RGA2 Device Driver（无版本号和v2.1.0）<br/>RGA multicore Device Driver（v1.2.0及以上） | RGA1、RGA2、RGA3 |

## 应用接口

RGA模块支持库为librga.so，通过对图像缓冲区结构体struct rga_info进行配置，实现相应的2D图形操作。为了获得更友好的开发体验，在此基础上进一步封装常用的2D图像操作接口。新的接口主要包含以下特点：

- 接口定义参考opencv/matlab中常用的2D图形接口定义，以减少二次开发的学习成本。
- 为消除RGA硬件版本差异带来的兼容问题，加入RGA query查询功能。查询内容主要包括版本信息，输入输出大分辨率及图像格式的支持。
- 执行图像操作之前，需要对输入输出图像缓冲区进行处理。调用wrapbuffer_T接口将输入输出图像信息填充到结构体struct rga_buffer_t，结构体中包含分辨率及图像格式等信息。
- 对于2D图像复合操作，增加improcess接口。通过传入一系列预定义的usage执行复合操作。
- 支持对单次无法完成的图像复合操作进行绑定为一个RGA图像任务，统一提交到驱动内逐个执行。

## API概述

该软件支持库提供以下API，异步模式仅支持C++实现。

- **querystring**： 查询获取当前芯片平台RGA硬件版本与功能支持信息，以字符串的形式返回。
- **imcheckHeader**:  校验当前使用头文件版本与librga版本差异。
- **importbuffer_T**： 将外部内存（dma_fd、虚拟地址、物理地址）导入RGA驱动内部，实现硬件快速访问物理连续/非物理连续的内存。
- **releasebuffer_handle**： 将外部buffer从RGA驱动内部解除引用与映射。
- **wrapbuffer_handle**： 快速封装图像缓冲区结构（rga_buffer_t）。
- **imbeginJob**：创建RGA图像处理任务。
- **imendJob**： 提交并执行RGA图像处理任务。
- **imcancelJob**： 取消并删除RGA图像处理任务。
- **imcopy**： 调用RGA实现快速图像拷贝操作。
- **imcopyTask**： 向RGA图像任务中添加快速图像拷贝操作。
- **imresize**： 调用RGA实现快速图像缩放操作。
- **imresizeTask**： 向RGA图像任务中添加快速图像缩放操作。
- **impyramind**： 调用RGA实现快速图像金字塔操作。
- **imcrop**： 调用RGA实现快速图像裁剪操作。
- **imcropTask**： 向RGA图像任务中添加快速图像裁剪操作。
- **imtranslate**： 调用RGA实现快速图像平移操作。
- **imtranslateTask**： 向RGA图像任务中添加快速图像平移操作。
- **imcvtcolor**： 调用RGA实现快速图像格式转换。
- **imcvtcolorTask**： 向RGA图像任务中添加快速图像格式转换。
- **imrotate**： 调用RGA实现快速图像旋转操作。
- **imrotateTask**： 向RGA图像任务中添加快速图像旋转操作。
- **imflip**： 调用RGA实现快速图像翻转操作。
- **imflipTask**： 向RGA图像任务中添加快速图像翻转操作。
- **imblend**： 调用RGA实现双通道快速图像合成操作。
- **imblendTask**： 向RGA图像任务中添加双通道快速图像合成操作。
- **imcomposite**： 调用RGA实现三通道快速图像合成操作。
- **imcompositeTask**： 向RGA图像任务中添加三通道快速图像合成操作。
- **imcolorkey**： 调用RGA实现快速图像颜色键操作。
- **imcolorkeyTask**： 向RGA图像任务中添加快速图像颜色键操作。
- **imosd**：调用RGA实现快速图像OSD字幕叠加。
- **imosdTask**：向RGA图像任务中添加快速图像OSD字幕叠加。
- **imquantize**： 调用RGA实现快速图像运算点前处理（量化）操作。
- **imquantizeTask**： 向RGA图像任务中添加快速图像运算点前处理（量化）操作。
- **imrop**： 调用RGA实现快速图像光栅操作。
- **imropTask**： 向RGA图像任务中添加快速图像光栅操作。
- **imfill**： 调用RGA实现快速图像填充操作。
- **imfillArray**： 调用RGA实现多组快速图像填充操作。
- **imfillTask**： 向RGA图像任务中添加快速图像填充操作。
- **imfillTaskArray**： 向RGA图像任务中添加多组快速图像填充操作。
- **imrectangle**： 调用RGA实现等距矩形边框快速绘制操作。
- **imrectangleArray**： 调用RGA实现多组等距矩形边框快速绘制操作。
- **imrectangleTask**： 向RGA图像任务中添加等距矩形边框快速绘制操作。
- **imrectangleTaskArray**： 向RGA图像任务中添加多组等距矩形边框快速绘制操作。
- **immakeBorder**： 调用RGA实现矩形边框快速绘制操作。
- **immosaic**：调用RGA实现快速图像马赛克遮盖。
- **immosaicArray**：调用RGA实现快速图像马赛克遮盖。
- **immosaicTask**：向RGA图像任务中添加快速图像马赛克遮盖。
- **immosaicTaskArray**：向RGA图像任务中添加快速图像马赛克遮盖。
- **improcess**： 调用RGA实现快速图像复合处理操作。
- **improcessTask**： 向RGA图像任务中添加快速图像复合处理操作。
- **imcheck**： 校验参数是否合法，以及当前硬件是否支持该操作。
- **imsync**： 用于异步模式时，同步任务完成状态。
- **imconfig**： 向当前线程上下文添加默认配置。

## 例程运行