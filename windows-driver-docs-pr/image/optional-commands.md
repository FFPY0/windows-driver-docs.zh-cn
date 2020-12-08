---
title: 可选命令
description: 可选命令
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f819cb9dce2ca7bb5fa4229c0cb26e42a9381ab1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785191"
---
# <a name="optional-commands"></a>可选命令


## <span id="ddk_optional_commands_si"></span><span id="DDK_OPTIONAL_COMMANDS_SI"></span>


Microdriver 可以实现以下命令，但这不是必需的。

<span id="CMD_GETSUPPORTEDFILEFORMATS"></span><span id="cmd_getsupportedfileformats"></span>CMD \_ GETSUPPORTEDFILEFORMATS  
由 WIA 平板驱动程序调用以获取其他文件格式的数目。 应填写传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val) 结构的两个成员： **lVal** 应设置为其他文件格式的数量; **pGuid** 应指向图像格式 guid 的数组。 为此数组分配的内存由 microdriver 所有，只应由它释放。

图像格式在 *wiadef* 中列出，或可以定义为自定义格式。 请注意，由于 BMP (文件) 和 MEMORYBMP (内存) 格式是所需的格式，WIA 平板驱动程序会自动添加它们。 Microdriver 不应将其添加到其扩展列表。

此命令是可选的，除非设备可以支持其他文件格式。

<span id="CMD_GETSUPPORTEDMEMORYFORMATS"></span><span id="cmd_getsupportedmemoryformats"></span>CMD \_ GETSUPPORTEDMEMORYFORMATS  
由 WIA 平板驱动程序调用以获取额外内存格式的数目。 应填写传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val) 结构的两个成员： **lVal** 应设置为额外的内存格式数; **pGuid** 应指向图像格式 guid 的数组。 为此数组分配的内存由 microdriver 所有，只应由它释放。

图像格式在 *wiadef* 中列出，或可以定义为自定义格式。 请注意，由于 BMP (文件) 和 MEMORYBMP (内存) 格式是所需的格式，WIA 平板驱动程序会自动添加它们。 Microdriver 不应将其添加到其扩展列表。

此命令是可选的，除非设备可以支持额外的内存格式。

<span id="CMD_SETFORMAT"></span><span id="cmd_setformat"></span>CMD \_ SETFORMAT  
类驱动程序发送此命令，以设置应用程序请求的当前格式。 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **pGuid** 成员包含图像格式 GUID。 为了跟踪当前的图像格式设置，microdriver 应将此图像格式 ID 保存在其专用上下文中。

仅当 Microdrivers 报告扩展格式时，才需要支持此命令。 由于类驱动程序无法验证扩展格式的数据，因此 microdriver 负责生成正确的数据。 传输扩展格式的数据时，应传输所有数据，包括图像标头。 例如，如果您的驱动程序报告它支持 JPEG 格式，则必须传输所有 JPEG，而不只是图像位。

类驱动程序拥有由 VAL 结构的 **pGuid** 成员指向的内存，因此 microdriver 不能释放它。

请注意，此命令不会影响 microdriver 响应其 [**Scan**](/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-scan) 函数调用的方式。 与往常一样，microdriver 必须检查此函数的 *lPhase*、 *pScanInfo* 和 *lLength* 参数的值，并根据需要将数据放置在 *pBuffer* 和 *pReceived* 参数所指向的缓冲区中。

仅支持 WiaImgFmt \_ BMP 和 WiaImgFmt \_ MEMORYBMP 格式的文件 (microdrivers) 的默认格式的驱动程序可以接收 CMD \_ SETFORMAT 命令。 这些驱动程序可以忽略此命令，因为该类驱动程序使用默认格式处理所有数据传输。

<span id="CMD_SETSCANMODE"></span><span id="cmd_setscanmode"></span>CMD \_ SETSCANMODE  
由 WIA 平板驱动程序调用，用于设置扫描模式-预览或 microdriver 设备的最终状态。 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **lVal** 成员将包含以下值之一，这两个值都是在 *wiamicro* 中定义的：

SCANMODE \_ PREVIEWSCAN − Preview 扫描模式

SCANMODE \_ FINALSCAN −最终扫描模式

<span id="CMD_SETSTIDEVICEHKEY"></span><span id="cmd_setstidevicehkey"></span>CMD \_ SETSTIDEVICEHKEY  
由 WIA 平板驱动程序调用，以允许 microdriver 读取已安装注册表部分中的注册表项。 此命令向 microdriver 提供 STI 设备的已安装注册表 HKEY，以便它可以访问其设备的专用注册表值。 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **pHandle** 成员将包含一个指针，指向在 STI 的 [**IStiUSD：： INITIALIZE**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)方法期间提供给 WIA 平板驱动程序的 HKEY。 这是已安装设备部分的顶级 HKEY。 可以使用此 HKEY 直接打开 **DeviceData** 键。 有关详细信息，请参阅 [WIA 设备的 INF 文件](./inf-files-for-wia-devices.md) 。

注意：此密钥 *仅* 由 WIA 平板驱动程序打开并关闭。 它在此命令和 CMD \_ INITIALIZE (查看 [所需命令](required-commands.md)) 中也是有效的。 这些命令返回后，该密钥将不再有效。 *不* 能缓存 HKEY 值。

 

