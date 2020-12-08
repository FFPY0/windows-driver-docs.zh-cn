---
title: PortCls 专用 PEP 上下文共享
description: 从 Windows 8 开始，微型端口驱动程序可以使用 IPortClsRuntimePower （一个新接口）来与 Windows Power Engine 插件共享 (PEP) 的专用上下文共享。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e1102ee751cd384165eb9aedcedc06e36ede3fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800811"
---
# <a name="portcls-private-pep-context-sharing"></a>PortCls 专用 PEP 上下文共享


从 Windows 8 开始，微型端口驱动程序可以使用 IPortClsRuntimePower （一个新接口）来与 Windows Power Engine 插件共享 (PEP) 的专用上下文共享。

已更新 (PortCls) 的音频端口类驱动程序，以在 WaveRT 端口公开新的 IPortClsRuntimePower 接口。 为了使微型端口驱动程序能够将专用电源控制发送给操作系统的 PEP，小型端口驱动程序首先必须获取对其关联端口的 IPortClsRuntimePower 接口的访问权限。 然后，小型端口驱动程序将注册在适当的时间调用的回调，以允许微型端口驱动程序发送专用电源控件。

## <a name="span-idaccessing_iportclsruntimepowerspanspan-idaccessing_iportclsruntimepowerspanspan-idaccessing_iportclsruntimepowerspanaccessing-iportclsruntimepower"></a><span id="Accessing_IPortClsRuntimePower"></span><span id="accessing_iportclsruntimepower"></span><span id="ACCESSING_IPORTCLSRUNTIMEPOWER"></span>访问 IPortClsRuntimePower


微型端口驱动程序通过以下事件序列获得对其端口的 IPortClsRuntimePower 的访问权限：

1. 微型端口驱动程序调用 [**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport) ，并 \_ 将 IID IPortWaveRT 作为 REFID 提供。

2. **PcNewPort** 创建 (Pport) 类型为 [IPortWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)的端口接口。

3. 然后，微型端口驱动程序会在新创建的 **IPortWaveRT** 端口接口中调用 QueryInterface，并将 IID \_ IPortClsRuntimePower 指定为接口 GUID。

4. **IPortWaveRT** 端口接口为微型端口驱动程序提供指向其 [**IPortClsRuntimePower**](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsruntimepower)接口的指针。

*Portcls* 头文件定义 IPORTCLSRUNTIMEPOWER 的 GUID，如下所示：

``` syntax
// {E057C351-0430-4DBC-B172-C711D40A2373}
DEFINE_GUID(IID_IPortClsRuntimePower,
0xe057c351, 0x430, 0x4dbc, 0xb1, 0x72, 0xc7, 0x11, 0xd4, 0xa, 0x23, 0x73);
```

## <a name="span-idregistering_a_callbackspanspan-idregistering_a_callbackspanspan-idregistering_a_callbackspanregistering-a-callback"></a><span id="Registering_a_callback"></span><span id="registering_a_callback"></span><span id="REGISTERING_A_CALLBACK"></span>注册回调


微型端口驱动程序使用 [**IPortClsRuntimePower：： RegisterPowerControlCallback**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsruntimepower-registerpowercontrolcallback) 方法注册回调。 当 PEP 启动专用请求或响应由微型端口驱动程序本身启动的专用请求时，将调用此方法。 通常应在驱动程序处理 IRP \_ MN \_ 启动 \_ 设备 PNP IRP 时执行回调注册操作。

除了回调中提供的上下文指针，其他参数的定义与运行时 power framework 的 PowerControlCallback 的定义相同。 此外，微型端口的回调必须是 PCPFNRUNTIME \_ 电源 \_ 控制回调类型 \_ ，如以下代码片段中的 *Portcls* 头文件所定义。

```ManagedCPlusPlus
typedef
NTSTATUS
_IRQL_requires_max_(DISPATCH_LEVEL)
(*PCPFNRUNTIME_POWER_CONTROL_CALLBACK)
(
    _In_        LPCGUID PowerControlCode,
    _In_opt_    PVOID   InBuffer,
    _In_        SIZE_T  InBufferSize,
    _Out_opt_   PVOID   OutBuffer,
    _In_        SIZE_T  OutBufferSize,
    _Out_opt_   PSIZE_T BytesReturned,
    _In_opt_    PVOID   Context
);
```

当停止或删除驱动程序时，它必须使用 [**IPortClsRuntimePower：： UnregisterPowerControlCallback**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsruntimepower-unregisterpowercontrolcallback) 方法注销任何已注册的回调。

## <a name="span-idsending_private_power_controlsspanspan-idsending_private_power_controlsspanspan-idsending_private_power_controlsspansending-private-power-controls"></a><span id="Sending_private_power_controls"></span><span id="sending_private_power_controls"></span><span id="SENDING_PRIVATE_POWER_CONTROLS"></span>发送专用电源控制


当微型端口建立对 **IPortClsRuntimePower** 接口的访问权限，并使用该接口的 **RegisterPowerControlCallback** 方法注册回调时，它现在已准备好发送专用电源控制。 调用回调方法时，微型端口驱动程序使用 [**IPortClsRuntimePower：： SendPowerControl**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsruntimepower-sendpowercontrol) 方法将专用电源控件发送到 Windows PEP。

除了 *DeviceObject* 参数外，所有其他参数的定义与运行时 power Framework 的 [PoFxPowerControl](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol) 方法的参数相同。

 

