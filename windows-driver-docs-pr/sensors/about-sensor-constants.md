---
title: 关于传感器常量
description: 关于传感器常量
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a82a3e852a3a1b9e6ebff7a65ca3adcaef44362f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831103"
---
# <a name="about-sensor-constants"></a>关于传感器常量


Windows 传感器和位置平台通过多种方式使用常量。 本部分介绍这些常量及其用法。

该平台定义了各种可在传感器驱动程序代码中使用的常量。 您还可以定义自己的常量。 你可以在文件 Sensorsdef 中查找平台定义的常量的定义。

## <a name="sensor-and-data-organization"></a>传感器和数据组织

平台按以下方式组织传感器及其数据：

-   *类别* 表示传感器设备的广泛类别。 类别提供了一种将可能提供相似类型的信息或以某种方式相关的传感器组合在一起的方法。 每个类别都由一个 GUID 常量表示。 例如，报告纬度和经度坐标的传感器属于位置传感器类别，该类别由 " [**传感器 \_ 类别 \_ 位置**](sensor-category-loc.md) " 常数表示。

-   *传感器类型* 表示特定类型的传感器。 每个传感器类型都适合特定类别。 不同类型的两个传感器可以属于同一类别或两个不同的类别。 每个传感器类型都由一个 GUID 常量表示。 例如，全局定位系统传感器将由传感器 \_ 类型 \_ 位置 \_ GPS 常量标识，而使用 Internet IP 地址提供当前位置的传感器将由传感器 \_ 类型 \_ 位置 \_ 查找常量标识。 但是，这两个传感器都属于位置传感器类别。

-   *数据类型* 表示传感器可以提供的特定类型的信息。 传感器数据类型可以包含实际度量值，例如海拔高度、用于表示数据的单位的相关信息，例如计量，数据的参考点，例如海平面级别。 每种数据类型由 **PROPERTYKEY** 常量表示。 例如，表示 g 中 x 轴加速度的数据类型将为传感器 \_ 数据 \_ 类型 \_ 加速度 \_ x \_ g 常量。

-   在报告数据时，一个值被视为包含在一个 *数据字段* 中，而一组相关的数据字段则构成 *数据报告*。 数据报表使用 [IPortableDeviceValues](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues) 接口打包在一起。 每个数据报表必须包含至少一个有效的数据字段和一个标识数据报表创建时间的时间戳。 时间戳由传感器 \_ 数据 \_ 类型 \_ TIMESTAMP 属性键表示。


## <a name="other-constants"></a>其他常量

驱动程序还需要使用其他类型的常量。 这些常量包括：

-   传感器属性，如传感器 \_ 属性 \_ 描述。 这些常量包括 WPD 常量，如 WPD \_ 函数 \_ 对象 \_ 类别。 通常，这些常量用于描述传感器，如在 [**ISensorDriver：： OnGetSupportedSensorObjects**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)中调用时。 还会通过 [**ISensorDriver：： OnGetSupportedProperties**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties) 和 [**ISensorDriver：： OnGetProperties**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)返回属性值。

-   某些传感器属性需要由你的驱动程序提供，某些属性可由客户端应用程序设置，而有些则必须始终返回相同的值。 " [**传感器属性**](sensor-properties.md) 参考" 部分提供了每个属性的相关信息。 若要了解特定方法所需的属性，请参阅 [Windows 传感器参考](/windows-hardware/drivers/ddi/_sensors/#functions) 部分的方法文档。

-   [**事件常数**](about-sensor-driver-events.md)，如传感器 \_ 事件 \_ 状态 \_ 已更改。 事件常量包括 GUID （表示事件类型）和 PROPERTYKEYs （表示事件参数类型）。 当 [**ISensorDriver：： OnGetSupportedEvents**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)中的类扩展调用或通过 [**ISensorClassExtension：:P ostevent**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent) 或 [**ISensorClassExtension：:P oststatechange**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)引发事件时，将使用这些常量。

-   图标常数。 驱动程序可以指定一个特定图标来表示 Windows 中的设备。 请参阅 [指定图标](specifying-an-icon.md)。

-   传感器平台定义 GUID_DEVINTERFACE_SENSOR 常量，用于标识传感器设备接口类。 在其安装过程中，驱动程序将注册至少一个设备接口类。 传感器类扩展为你注册传感器设备接口类。



## <a name="persistent-unique-identifier"></a>永久性唯一标识符

名为传感器 \_ 属性 \_ 持久唯一 ID 的传感器属性 \_ \_ 需要特别注意。 对于设备上的每个传感器，此属性的值必须是唯一的。 同时，每次传感器平台使用此值时，该传感器的值必须保持一致。 有关如何在驱动程序代码中创建永久唯一标识符的示例，请参阅 [创建持久的唯一标识符](creating-a-persistent-unique-identifier.md)。

## <a name="providing-geolocation-information"></a>提供地理位置信息

有时，即使传感器不是位置传感器，用户也需要知道传感器的物理位置。 例如，天气工作站提供的数据含义与工作站的位置紧密关联。

若要提供此类型的地理位置数据，任何传感器都可以使用 [**传感器 \_ 类别 \_ 位置**](sensor-category-loc.md) 类别中适当的数据字段，即使传感器不是位置传感器。 因此，天气工作站可以通过使用传感器 \_ 数据 \_ 类型 " \_ 纬度度" 和 " \_ 传感器 \_ 数据类型" \_ " \_ 经度 \_ 度数据字段常量" 报告其位置。 但是，在 [**ISensorDriver：： OnGetProperties**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)中调用时，不要将此类传感器报告为属于位置类别，这一点很重要。

Windows 将传感器与位置类别中的现有位置类型（ (传感器 \_ 类别位置) 中的现有位置类型视为相同 \_ 。 因此，这些传感器位于 location 权限模型下。 不应尝试绕过位置传感器的权限模型 (例如，将 GPS 传感器类型呈现为传感器 \_ 类型 \_ 位置 \_ GPS，但指定非位置类别) 。

## <a name="custom-values"></a>自定义值

您可以为类别、传感器类型、数据字段、属性和事件定义自定义值。

有关如何定义常量的自定义值的指南和示例，请参阅 [定义常量的自定义值](defining-custom-values-for-constants.md)。

