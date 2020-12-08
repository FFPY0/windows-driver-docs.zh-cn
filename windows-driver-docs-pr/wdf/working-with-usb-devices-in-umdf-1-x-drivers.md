---
title: 在 UMDF 1.x 驱动程序中使用 USB 设备
description: 在 UMDF 1.x 驱动程序中使用 USB 设备
keywords:
- UMDF WDK，USB 设备
- User-Mode Driver Framework WDK，USB 设备
- 用户模式驱动程序 WDK UMDF、USB 设备
- USB 设备 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db5e4e43c10edf6fc6b59b9822cd1915b36dfbe4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833939"
---
# <a name="working-with-usb-devices-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中使用 USB 设备


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

该框架将每个 USB 设备表示为框架 USB 设备对象。 UMDF 驱动程序必须创建一个框架 USB 设备对象，驱动程序才能访问该框架对 USB i/o 目标的支持。 UMDF 提供了 USB 设备对象方法，使 UMDF 驱动程序能够：

-   [创建 UMDF-USB 设备对象](#creating-a-umdf-usb-device-object)

-   [获取设备信息](#obtaining-umdf-usb-device-information)

-   [发送控件传输](#send-a-control-transfer-to-a-umdf-usb-device-object)

-   [设置电源策略](#set-power-policy-for-a-umdf-usb-device-object)

### <a name="creating-a-umdf-usb-device-object"></a>创建 UMDF-USB 设备对象

若要使用框架的 USB i/o 目标功能，UMDF 驱动程序必须首先获取指向 [IWDFUsbTargetFactory](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetfactory) 接口的指针。 若要获取指针，驱动程序必须调用设备的 [IWDFDevice](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)接口的 **QueryInterface** 方法。 下面的代码示例演示如何调用 **QueryInterface** 以获取指针：

```cpp
hr = pdevice->QueryInterface(IID_IWDFUsbTargetFactory, (LPVOID*)&ppUsbTargetFactory);
```

接下来，驱动程序必须调用 [**IWDFUsbTargetFactory：： CreateUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice) 方法为设备创建 USB i/o 目标对象。 驱动程序创建 USB i/o 目标后，该驱动程序可以向 i/o 目标发送请求。 通常，驱动程序从 [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)回调函数中调用 **IWDFUsbTargetFactory：： CreateUsbTargetDevice** 。

驱动程序调用 **IWDFUsbTargetFactory：： CreateUsbTargetDevice** 后，驱动程序可以 [获取 usb 设备信息](#obtaining-umdf-usb-device-information) (例如，设备、usb 接口和接口终结点) 的 usb 描述符。 Usb 规范中介绍了 USB 描述符。

### <a name="obtaining-umdf-usb-device-information"></a>获取 UMDF-USB 设备信息

在 UMDF 驱动程序调用 [**IWDFUsbTargetFactory：： CreateUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice) 方法来创建一个 umdf usb 目标设备对象之后，驱动程序可以调用 usb 目标设备对象为获取有关 usb 设备的信息定义的以下方法：

<a href="" id="iwdfusbtargetdevice--retrievedescriptor"></a>[**IWDFUsbTargetDevice::RetrieveDescriptor**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)  
获取设备的 USB 设备描述符。

<a href="" id="iwdfusbtargetdevice--getnuminterfaces"></a>[**IWDFUsbTargetDevice::GetNumInterfaces**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)  
获取设备支持的 USB 接口数量。

<a href="" id="iwdfusbtargetdevice--retrieveusbinterface"></a>[**IWDFUsbTargetDevice::RetrieveUsbInterface**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)  
获取指向 [IWDFUsbInterface](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface) 接口的指针，该接口公开设备支持的一个 USB 接口。

<a href="" id="iwdfusbtargetdevice--retrievedeviceinformation"></a>[**IWDFUsbTargetDevice::RetrieveDeviceInformation**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedeviceinformation)  
检索与 USB 设备关联的功能信息。

<a href="" id="iwdfusbtargetdevice--retrievepowerpolicy"></a>[**IWDFUsbTargetDevice::RetrievePowerPolicy**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievepowerpolicy)  
检索 WinUsb 电源策略。

<a href="" id="iwdfusbtargetdevice--getwinusbhandle"></a>[**IWDFUsbTargetDevice::GetWinUsbHandle**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getwinusbhandle)  
获取与 i/o 目标设备对象相关联的 WinUsb 接口句柄。

### <a name="sending-a-control-transfer-to-a-umdf-usb-device-object"></a><a href="" id="send-a-control-transfer-to-a-umdf-usb-device-object"></a>将控件传输发送到 UMDF USB 设备对象

UMDF 驱动程序可以调用 [**IWDFUsbTargetDevice：： FormatRequestForControlTransfer**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer) 方法来格式化描述标准、设备特定的或特定于供应商的 USB 控制传输的 i/o 请求。 然后，该驱动程序可以调用 [**IWDFIoRequest：： send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法以同步或异步方式发送请求。

### <a name="setting-power-policy-for-a-umdf-usb-device"></a><a href="" id="set-power-policy-for-a-umdf-usb-device-object"></a>设置 UMDF USB 设备的电源策略

UMDF 驱动程序可以调用 [**IWDFUsbTargetDevice：： SetPowerPolicy**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy) 方法来设置 WINUSB 用于 USB 设备的电源策略。 USB 设备的电源策略影响设备的电源管理状态。

 

