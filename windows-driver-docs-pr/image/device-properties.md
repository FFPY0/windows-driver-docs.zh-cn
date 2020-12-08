---
title: 图像处理设备属性
description: 图像处理设备属性
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 40ccba565a3f1d67eebc2b98c95af7ec93abae5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792869"
---
# <a name="imaging-device-properties"></a>图像处理设备属性

所有静止图像设备都具有描述该设备的特定特征。 例如，平板扫描仪的两个特征是其水平和垂直床大小。 数字摄像机的可能特征是电池状态，它指示电池剩余寿命。

同样，还可以通过特征来描述设备生成的数据或存储的数据。 例如，扫描程序生成的数据可以按行上的像素数和每个像素的位数来进行描述。

在 WIA 中，描述设备和数据的特性称为 *属性*。 集中存在属性;WIA 微型驱动程序将它们保留在 WIA 驱动程序项中。
