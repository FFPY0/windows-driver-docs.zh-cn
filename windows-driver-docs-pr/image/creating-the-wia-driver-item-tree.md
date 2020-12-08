---
title: 创建 WIA 驱动程序项树
description: 创建 WIA 驱动程序项树
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afd9d32f8becd25e18edc2aa8115595584af38ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837259"
---
# <a name="creating-the-wia-driver-item-tree"></a>创建 WIA 驱动程序项树





初始化微型驱动程序后，必须通过以下方式在 [**IWiaMiniDrv：:D rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia) 方法中创建驱动程序项树：

1.  如果驱动程序项树尚不存在，则创建它。 微型驱动程序设置根项标志，并通过调用驱动程序服务库函数 [**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)创建根项。 微型驱动程序将返回的指针存储到私有成员变量中的根项。

2.  使用 [**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem) 函数为设备上的每个项创建子项目。 此函数创建设备特定的上下文，微型驱动程序可以在此上下文中存储有关项的信息。

3.  对每个子项调用 [**IWiaDrvItem：： AddItemToFolder**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder) 方法，将该项添加到驱动程序项树中。

 

