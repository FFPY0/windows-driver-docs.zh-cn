---
title: 帮助程序函数的封送处理
description: 本主题提供有关 sensorsutils 标头文件中的封送处理 helper 函数的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e27930ec95e245e84be49b094ba0be404946942b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812319"
---
# <a name="marshalling-helper-functions"></a>帮助程序函数的封送处理

本主题提供有关 *sensorsutils* 标头文件中的封送处理 helper 函数的信息。

这些帮助程序函数由 v2 传感器驱动程序使用，它们与传感器设备驱动程序软件接口一起使用 (DDSI) 。

如果实现自己的封送处理程序帮助程序函数，请记住，在 [**传感器 \_ 配置**](/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_config) 结构中填充枚举列表时，或使用 [**SensorsCxSensorDataReady**](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready) 函数报告更新的数据时，不得使用 helper 函数。

## <a name="in-this-section"></a>在本节中

|主题|描述|
|--|--|
|[时间戳帮助程序](timestamp-helper.md)|时间戳 helper 函数由 v2 传感器驱动程序使用，并用于传感器设备驱动程序软件接口 (DDSI) 。|
|[PropVariant 帮助程序](propvariant-helpers.md)|V2 传感器驱动程序使用 PropVariant helper 函数操作与传感器关联的 [PropVariant](/windows/win32/api/propidl/ns-propidl-propvariant) 结构。|
|[集合列表帮助程序](collection-list-helpers.md)|V2 传感器驱动程序使用集合列表 helper 函数来处理 [SENSOR_COLLECTION_LIST](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构。|
|[集合列表序列化帮助程序](collection-list-serialization-helpers.md)|V2 传感器驱动程序使用集合列表序列化帮助器函数来执行对 [SENSOR_COLLECTION_LIST](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构的序列化相关操作。|
|[集合列表旧版帮助程序](collection-list-legacy-helpers.md)|V2 传感器驱动程序使用集合列表旧 helper 函数与 [SENSOR_COLLECTION_LIST](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构进行交互。|

## <a name="requirements"></a>要求

**标头：** Sensorsutils
