---
title: 特定于设备的上下文
description: 特定于设备的上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99bec1f10205e12ccc58412b935a2890bf616f35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839259"
---
# <a name="device-specific-contexts"></a>特定于设备的上下文





微型驱动程序可以选择性地利用专用上下文来存储特定于设备的信息。 此设备特定的上下文可以减少微型驱动程序必须调用设备以获取设备信息的次数。 特定微型驱动程序的每个驱动程序项只能有一个设备特定的上下文。 当不再需要驱动程序项时，WIA 服务将调用微型驱动程序的 [**IWiaMiniDrv：:D rvfreedrvitemcontext**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext) 方法，以释放附加到设备特定上下文的所有资源。

例如，当照相机驱动程序从设备检索缩略图数据时，它通常会将数据缓存在与相应的驱动程序项相关联的驱动程序上下文中。 请注意，WIA 服务释放上下文。 驱动程序的责任只是释放其上下文所持有的所有资源。 如果上一个示例的缩略图数据存储在特定于设备的上下文中的内存中，则保存该缓存数据的内存应在此处释放，而不是在上下文本身中。

 

