---
title: 提供的 WDTF 简单 I/O 插件
description: 简单 i/o 插件是 Windows 驱动程序测试框架的扩展 (WDTF) ，用于实现特定于设备的特定 i/o 功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8198da11fd4347d049bd94e9129a62471aaf0f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785371"
---
# <a name="provided-wdtf-simple-io-plug-ins"></a>提供的 WDTF 简单 I/O 插件

简单 i/o 插件是 Windows 驱动程序测试框架的扩展 (WDTF) ，用于实现特定于设备的特定 i/o 功能。 如果为要测试的设备类型提供了插件，则 [设备基本测试](/windows-hardware/drivers) 将使用 WDTF 简单 i/o 接口测试 i/o。

本主题列出了具有简单 i/o 插件的设备类型，并指示是否存在测试设备的特定要求。 使用 [Windows 硬件实验室工具包 (WINDOWS HLK) ](/windows-hardware/test/hlk/)时，需要遵循这些要求。 本主题还介绍了如何对测试失败进行故障排除和会审。

如果未列出你的设备类型，则可以创建一个，请参阅 [如何使用 WDTF Simple I/o 操作插件为设备自定义 i/o](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)

有关具有特定要求的设备基础测试的列表，请参阅 [具有特定设备配置要求的设备基础测试](#device-fundamental-tests-that-have-specific-device-configuration-requirements)

## <a name="audio"></a>音频

### <a name="requirements"></a>要求

- 设备必须至少连接一个呈现类型终结点 (扬声器、耳机或类似) 。

- 如果目标音频设备具有 HDMI 视频和音频输出功能，若要执行音频测试，设备必须连接到 HDMI 音频功能设备，如 HDMI 监视器或 A/V 接收器。

### <a name="type-of-io-plug-in-performs-audio"></a>I/o 插件的类型执行 (音频) 

- 在呈现类型终结点上播放正弦微调。 捕获捕获类型终结点上的音频。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

- 查看失败的 HRESULT 以执行初始会审。
- 如果测试未响应，请使用目标计算机上的内核调试器来缩小根本原因。
- 运行跟踪：
  - 启动内核跟踪：

```syntax
xperf.exe -on LOADER+PROC_THREAD+CSWITCH+DISK_IO+HARD_FAULTS+PROFILE+INTERRUPT+NETWORKTRACE+DPC+Latency+POWER -stackwalk ProcessCreate+ProcessDelete+ImageLoad+ImageUnload+ThreadCreate+ThreadDelete+CSwitch+ReadyThread+Profile+DiskFlushInit+FileFlush+RegFlush+HardFault+VirtualAlloc+VirtualFree -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo_Kernel.etl
```

- 启动音频跟踪：

```syntax
xperf.exe -start AudioSimpleIo -on Microsoft-Windows-Audio+a6a00efd-21f2-4a99-807e-9b3bf1d90285:0xffff:0x3 -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo.etl
```

- 运行测试。
- 停止跟踪：

```syntax
xperf.exe -stop "NT Kernel Logger" Audio_SimpleIo
```

- 合并跟踪：

```syntax
xperf.exe -merge Audio_SimpleIo_Kernel.etl Audio_SimpleIo.etl Audio_SimpleIo _Merged.etl
```

- 查看合并的跟踪文件，其中包含 Xperf (**xperfview**) 。

## <a name="bluetooth"></a>蓝牙

### <a name="bluetooth-requirements"></a>蓝牙要求

- 无特殊要求。

#### <a name="type-of-io-plug-in-performs-bluetooth"></a>I/o 插件的类型 (蓝牙) 

- 使用 [**BluetoothFindFirstDevice 函数**](/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothfindfirstdevice) 查找蓝牙设备。

## <a name="cdrom"></a>CDROM

### <a name="cdrom-requirements"></a>CDROM 要求

- 已分配驱动器号。
- 媒体存在于设备中。
- 文件存在于插入的介质上。

### <a name="type-of-io-plug-in-performs-cdrom"></a>I/o 插件的类型会执行 (CDROM) 

- 在 cd-rom 上查找文件，并使用 Win32 [**ReadFile**](/windows/win32/api/fileapi/nf-fileapi-readfile) API 执行读取操作。

### <a name="how-to-triage-test-failures-cdrom"></a>如何诊断 (CDROM) 的测试失败

- 在测试计算机上，导航到相关的 CD/DVD 驱动器并确认你可以访问驱动器的内容。
- CD-Rom 简单的 i/o 插件在 CD/DVD 上搜索要用于执行读取的文件。 确保 CD/DVD 中的文件在磁盘上进行了编码。
- 这个简单的 i/o 插件使用 Win32 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)， [**WriteFile**](/windows/win32/api/fileapi/nf-fileapi-writefile)， [**ReadFile**](/windows/win32/api/fileapi/nf-fileapi-readfile) 函数。 返回的错误很可能是这些 Api 中的 Win32 错误代码。

## <a name="disk"></a>磁盘

### <a name="disk-requirements"></a>磁盘要求

- 磁盘至少分配有一个关联的卷驱动器号。

#### <a name="type-of-io-plug-in-performs-disk"></a>I/o 插件的类型执行 (磁盘) 

- 使用简单的 [卷](#volume)i/o 插件。

## <a name="display"></a>显示

### <a name="display-requirements"></a>显示要求

- 没有特殊的测试要求。

### <a name="type-of-io-plug-in-performs-display"></a>I/o 插件的类型执行 (显示) 

- 使用 D3DX Api 来运动图形适配器。

### <a name="how-to-triage-test-failures-display"></a>如何对测试失败进行会审 (显示) 

- 查看测试日志，该日志报告所使用的 Api 失败。

## <a name="gps-devices-and-gps-devices-in-systems"></a>GPS 设备在系统中 (和 GPS 设备) 

### <a name="requirements-gps"></a>要求 (GPS) 

- 设备必须在具有适当 GPS 信号的位置进行测试。

### <a name="type-of-io-plug-in-performs-gps"></a>I/o 插件的类型会执行 (GPS) 

- 对 [传感器](#sensors)使用 i/o 插件。

## <a name="lan"></a>LAN

### <a name="requirements-lan"></a> (LAN) 的要求

- 设备有一个 IPv6 地址。

- 设备具有 IPv6 网关地址 (否则，应将 WDTFREMOTESYSTEM 参数传递给测试，其中包含一个测试 NIC 可对其执行 ping 操作的 IPv6 地址) 。

- 设备的网络操作状态为 "IfOperStatusUp"。

- 网络设备不是 WWAN 或 WLAN 设备。

### <a name="type-of-io-plug-in-performs-lan"></a>I/o 插件的类型 (LAN) 执行

- Ping IPv6 网络网关地址。

### <a name="how-to-triage-test-failures-lan"></a>如何诊断 (LAN) 的测试失败

- 确认有一个现有的 IP 地址。
- 确认存在网关 IPv6 IP 地址。
-  (使用 ping.exe) ，请手动确认 IP 网关地址。

## <a name="mobile-broadband"></a>移动宽带

### <a name="requirements-mobile-broadband"></a>移动宽带 (要求) 

- 没有特殊的测试要求。

### <a name="type-of-io-plug-in-performs-mobile-broadband"></a>I/o 插件的类型 (移动宽带执行) 

- 使用 [**IMbnInterface 接口**](/windows/win32/api/mbnapi/nn-mbnapi-imbninterface) 并调用 GetHomeProvider、 [**IMbnInterface：： GetInterfaceCapability 方法**](/windows/win32/api/mbnapi/nf-mbnapi-imbninterface-getinterfacecapability)和 [**IMbnInterface：： GetReadyState 方法**](/windows/win32/api/mbnapi/nf-mbnapi-imbninterface-getreadystate) api 来试验设备。

### <a name="how-to-triage-test-failures-mobile-broadband"></a>如何诊断移动宽带 (的测试失败) 

- MobileBroadbandPlugin 的区域可能会失败。

  - "MobileBroadbandPlugin：获取所有移动宽带接口时返回故障。"
  - "MobileBroadbandPlugin：获取接口时返回了失败。"
  - "MobileBroadbandPlugin：获取 DeviceId 返回的。"
  - "MobileBroadbandPlugin：获取接口功能返回失败"
  - "MobileBroadbandPlugin：获取 ReadyState 返回的失败。"

- 调查故障的最佳位置是从设备开始，并确定它是否无法指示就绪信息或设备功能。 若要调试更进一步的操作系统跟踪文件，需要收集。

  - 运行命令： **netsh trace start wwan \_ dbg**
  - 重现此问题。
  - 运行命令： **netsh trace stop**

## <a name="portable-devices"></a>便携设备

### <a name="requirements-portable-devices"></a>便携设备 (需求) 

- 设备具有可在其中创建文件夹和文件的存储组件。

### <a name="type-of-io-plug-in-performs-portable-devices"></a>I/o 插件的类型 (便携设备执行) 

- 使用 WPD Api 读取文件并将其写入 WPD 设备上的存储组件。

## <a name="smart-card-readers"></a>智能卡读卡器

### <a name="requirements-smart-card-readers"></a>智能卡读卡器 (要求) 

- 设备已插入 Athena T0 测试卡。

### <a name="type-of-io-plug-in-performs-smart-card-readers"></a>I/o 插件的类型会执行 (智能卡读卡器) 

- 读取数据并将数据写入读卡器中插入的 Athena T0 卡。

## <a name="sensors"></a>Sensors

### <a name="requirements-sensors"></a>传感器 (要求) 

- GPS 设备必须在具有适当 GPS 信号的位置进行测试。

## <a name="volume"></a>数据量(Volume)

### <a name="requirements-volume"></a> (卷) 的要求

- 已为卷分配驱动器号。
- 卷的可用空间为5MB。
- 卷不是写保护的。
- 媒体存在于设备中。

### <a name="type-of-io-plug-in-performs-volume"></a>I/o 插件的类型执行 (卷) 

- 创建名为 WDTF 的 \_ 目录 \_ ，并创建一个名为 SimpleIO 的文件。 I/o 是通过调用 [**ReadFile**](/windows/win32/api/fileapi/nf-fileapi-readfile) 和 [**WriteFile**](/windows/win32/api/fileapi/nf-fileapi-writefile) api 来执行的。

### <a name="how-to-triage-test-failures-volume"></a>如何诊断 (卷) 的测试失败

- 在测试计算机上，导航到相关驱动器并确认你可以访问驱动器的内容。
- 尝试将文件保存到驱动器。 确保可以轻松保存和访问。
- 这个简单的 i/o 插件使用 Win32 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)， [**WriteFile**](/windows/win32/api/fileapi/nf-fileapi-writefile)， [**ReadFile**](/windows/win32/api/fileapi/nf-fileapi-readfile) 函数。 返回的错误很可能是这些 Api 中的 Win32 错误代码。

## <a name="webcam"></a>摄像头

### <a name="requirements-webcam"></a>要求 (网络摄像机) 

- 没有特殊的测试要求。

    > [!NOTE]
    > 用于网络摄像机设备的简单 i/o 插件依赖于 MFPlat.dll 文件，该文件在不包括 Media Player 和相关技术的 Windows 版本（例如，Windows 7 N 或 Windows 7 KN）上不可用。 在这些版本的 Windows 上，必须安装媒体功能包。 媒体功能包可供下载。 有关详细信息，请参阅 [知识库文章 968211](/troubleshoot/windows-client/shell-experience/windows-media-feature-pack-for-windows-7)。

### <a name="type-of-io-plug-in-performs-webcam"></a>I/o 插件的类型 (网络摄像机) 

- 使用媒体基础接口来捕获视频。

## <a name="wlan"></a>WLAN

### <a name="requirements-wlan"></a> (WLAN) 的要求

- 请参阅 HCK 文档中 [由设备基础测试记录的 WLAN SimpleIO 插件故障疑难解答](/previous-versions/windows/hardware/hck/dn260302(v=vs.85)) 。

### <a name="type-of-io-plug-in-performs-wlan"></a>I/o 插件的类型 (WLAN) 

- 请参阅 HCK 文档中 [由设备基础测试记录的 WLAN SimpleIO 插件故障疑难解答](/previous-versions/windows/hardware/hck/dn260302(v=vs.85)) 。

### <a name="how-to-triage-test-failures-wlan"></a>如何诊断 (WLAN) 的测试失败

- 请参阅 HCK 文档中 [由设备基础测试记录的 WLAN SimpleIO 插件故障疑难解答](/previous-versions/windows/hardware/hck/dn260302(v=vs.85)) 。

## <a name="usb-controller-and-hub-with-mutt"></a>USB 控制器和集线器与 Mutt

### <a name="requirements-usb"></a> (USB) 的要求

- 没有特殊的测试要求。

    设备具有符号链接。

### <a name="type-of-io-plug-in-performs-usb"></a>I/o 插件的类型执行 (USB) 

- 使用 Microsoft USB 测试工具 (MUTT) 设备的 USB 传输测试。 仅当 SuperMUTT 插入到 USB 3.0 控制器时，所涵盖的传输类型包括控制、大容量、同步、中断和流式处理 () 

### <a name="how-to-triage-test-failures-usb"></a>如何诊断 (USB) 的测试失败

- 首先检查测试日志文件中的消息。
- 通过在 USB 2.0 和 USB 3.0 堆栈上启用 Windows (ETW) 的事件跟踪，进一步进行调查。
  - 对于 USB 2.0，请参阅[windows 7 usb 核心堆栈中](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/etw-in-the-windows-7-usb-core-stack/ba-p/270689)的 MICROSOFT Windows USB 核心团队博客-ETW
  - 对于 USB 3.0，请参阅 Microsoft Windows USB 核心团队博客- [如何在 Windows 8 中捕获和读取 USB ETW 跟踪](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/how-to-capture-and-read-usb-etw-traces-in-windows-8/ba-p/270762)

## <a name="device-fundamental-tests-that-have-specific-device-configuration-requirements"></a>具有特定设备配置要求的设备基础测试

在运行以下 [设备基础测试](/windows-hardware/drivers)之前，必须根据本主题中所述的针对特定设备类型的要求配置测试计算机上的设备。

- PCI 根端口惊喜删除测试 (PCI 设备仅) 
- 设备路径试验测试 (认证) 
- 睡眠和 PNP (在 (证书前后使用 IO 来禁用和启用) ) 
- 即插即用的驱动程序测试 (认证) 
- 并发硬件和操作系统 (混乱) 测试 (认证) 
- 在 (认证) 之前和之后，重新安装 IO
- 设备安装检查以确保文件系统一致性 (认证) 
- 设备安装检查以了解其他设备稳定性 (认证) 

## <a name="related-topics"></a>相关主题

[设备基础功能测试](../devtest/device-fundamentals-tests.md)  

[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)  

[如何在运行时从命令提示符测试驱动程序](/windows-hardware/drivers)  

[如何选择和配置设备基础功能测试](/windows-hardware/drivers)  

[设备基础测试疑难解答](/windows-hardware/drivers)
