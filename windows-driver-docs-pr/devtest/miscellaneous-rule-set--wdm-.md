---
title: 其他规则集 (WDM)
description: 使用这些规则来验证驱动程序是否正确遵循了对注册表项、字符串和设备对象指针的正确处理的一组一般要求。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 87a0d1b19e51a377f6e598124b93afc41c3d09c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838629"
---
# <a name="miscellaneous-rule-set-wdm"></a>其他规则集 (WDM)


使用这些规则来验证驱动程序是否正确遵循了对注册表项、字符串和设备对象指针的正确处理的一组一般要求。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"><strong>AddDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"><strong>AddDevice</strong></a>规则指定驱动程序的<a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><strong>AddDevice</strong></a>例程仅在调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a>后才调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>IoAttachDeviceToDeviceStack</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"><strong>DanglingDeviceObjectReference</strong></a></p></td>
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"><strong>DanglingDeviceObjectReference</strong></a>规则指定驱动程序将<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)"><strong>ObDereferenceObject</strong></a>与<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference" data-raw-source="[&lt;strong&gt;IoGetAttachedDeviceReference&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)"><strong>IoGetAttachedDeviceReference</strong></a>返回的设备对象指针一起调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"><strong>PnpSameDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"><strong>PnpSameDeviceObject</strong></a>规则指定驱动程序使用指向有效目标设备对象的指针调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>IoAttachDeviceToDeviceStack</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"><strong>TargetRelationNeedsRef</strong></a></p></td>
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"><strong>TargetRelationNeedsRef</strong></a>规则指定在处理<em>TargetDeviceRelation</em>查询时，驱动程序的<a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchPnP&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><strong>DispatchPnP</strong></a>例程调用以下函数之一来引用子设备的 PDO：</p>
<ul>
<li><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>ObReferenceObject</strong></a></p></li>
<li><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a></p></li>
<li><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer" data-raw-source="[&lt;strong&gt;ObReferenceObjectByPointer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)"><strong>ObReferenceObjectByPointer</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a>规则指定在调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)"><strong>ZwCreateKey</strong></a>之后，驱动程序只能调用以下注册表函数，同时将打开的句柄保存到注册表项 (也就是说，在对<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>ZwClose</strong></a>或<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)"><strong>ZwDeleteKey</strong></a>的任何调用都关闭或删除注册表项) 的句柄之前：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](wdm-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a>规则指定在调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)"><strong>ZwOpenKey</strong></a>之后，驱动程序只会在将打开的句柄保存到注册表项 (的情况下，在调用<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>ZwClose</strong></a>或<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)"><strong>ZwDeleteKey</strong></a>) 之前调用以下注册表函数：</p></td>
</tr>
</tbody>
</table>

 

**选择杂项规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **杂项**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

