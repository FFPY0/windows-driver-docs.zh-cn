---
title: ScsiReadCapacity 函数
description: ScsiReadCapacity WMI 方法可向所指示的设备发送 SCSI 读取容量命令。
keywords:
- ScsiReadCapacity 函数存储设备
topic_type:
- apiref
api_name:
- ScsiReadCapacity
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 78233544a561b4702de4b8b4131dfa27b56da261
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839397"
---
# <a name="scsireadcapacity-function"></a>ScsiReadCapacity 函数


**ScsiReadCapacity** WMI 方法可向所指示的设备发送 SCSI 读取容量命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void ScsiReadCapacity(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [in] uint8                                   Cdb[10],
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[10],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[10],
   [in] uint64                                  FcLun,
   [out] uint32                                 ResponseBufferSize,
   [out] uint32                                 SenseBufferSize,
   [out] uint8                                  ScsiStatus,
   [out, WmiSizeIs("ResponseBufferSize")] uint8 ResponseBuffer[],
   [out, WmiSizeIs("SenseBufferSize")] uint8    SenseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)结构的 **HBAStatus** 成员中返回此信息。

*Cdb*   
包含要发送到目标设备的 SCSI 读取容量命令的命令描述符块。 此信息将传送到结构中 [**ScsiReadCapacity \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)的 **Cdb** 成员的微型端口驱动程序。

*HbaPortWWN*   
用于访问目标的 HBA 的全球名称。 此信息将传送到结构 [**\_ 中 ScsiReadCapacity**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)的 **HbaPortWWN** 成员中的微型端口驱动程序。

*DiscoveredPortWWN*   
用于访问目标设备的端口的全球名称。 此信息将传送到结构 [**\_ 中 ScsiReadCapacity**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)的 **DiscoveredPortWWN** 成员中的微型端口驱动程序。

*FcLun*   
将接收 SCSI 读取容量命令的逻辑单元的逻辑单元号。 此信息将传送到结构 [**\_ 中 ScsiReadCapacity**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)的 **FcLun** 成员中的微型端口驱动程序。

*ResponseBufferSize*   
将保存读取容量命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序在 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)结构的 **ResponseBufferSize** 成员中返回此信息。

*SenseBufferSize*   
缓冲区的大小（以字节为单位），该缓冲区将保存 SCSI 查询命令生成的 SCSI 感知数据。 微型端口驱动程序在 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)结构的 **SenseBufferSize** 成员中返回此信息。

*ScsiStatus*   
SCSI 读取容量命令的状态。 微型端口驱动程序在 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)结构的 **ScsiStatus** 成员中返回此信息。

*ResponseBuffer*   
SCSI 读取容量命令的结果。 微型端口驱动程序在 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)结构的 **ResponseBuffer** 成员中返回此信息。

*SenseBuffer*   
Scsi 读取容量命令生成的 SCSI 探测数据。 微型端口驱动程序在 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)结构的 **SenseBuffer** 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 [MSFC \_ HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**ScsiReadCapacity \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)

[**ScsiReadCapacity \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)

 

