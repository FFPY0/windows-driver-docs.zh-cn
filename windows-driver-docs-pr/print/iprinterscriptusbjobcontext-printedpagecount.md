---
title: 'IPrinterScriptUsbJobContext PrintedPageCount 方法 (out) '
description: 返回当前作业中打印设备打印的页数。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- PrintedPageCount 方法打印设备
- PrintedPageCount 方法打印设备，IPrinterScriptUsbJobContext 接口
- IPrinterScriptUsbJobContext 接口打印设备，PrintedPageCount 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.PrintedPageCount
api_type:
- COM
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 595505f9c8de4995c4e6cf33807a3a69fc2bf596
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835555"
---
# <a name="iprinterscriptusbjobcontextprintedpagecount-method-out"></a>IPrinterScriptUsbJobContext：:P rintedPageCount 方法 (out) 

返回当前作业中打印设备打印的页数。

## <a name="syntax"></a>语法

```cpp
HRESULT PrintedPageCount(
  [out, retval] UINT32 *value
);
```

## <a name="parameters"></a>参数

*值* \[out，retval\]  
当前作业中打印设备打印的页数。

## <a name="return-value"></a>返回值

此方法返回 **HRESULT** 值。

## <a name="remarks"></a>备注

**PrintedPageCount** 是读/写方法。 IHV JavaScript **writeData** 函数应将打印页计数保持为最新状态，以允许 USBMon 设置作业的正确进度。

如果 IHV JavaScript 代码从不调用 **PrintedPageCount** 来设置打印的页计数，则假定页面的准确计数不可能，USBMon 将允许后台处理程序继续估计进度。

有关使用打印设备进行 USBMon 和基于 USB 的双向通信的信息，请参阅 [USB 双向扩展](./usb-bidi-extender.md)器。

## <a name="requirements"></a>要求

**支持的最低客户端：** Windows 8.1

**支持的最低服务器：** Windows Server 2012 R2

**目标平台：** 机

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)

[USB 双向扩展程序](./usb-bidi-extender.md)
