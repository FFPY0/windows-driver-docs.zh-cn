---
title: 网络 INF 文件中的 Remove 节
description: 网络 INF 文件中的 Remove 节
keywords:
- INF 文件 WDK 网络，删除部分
- 网络 INF 文件 WDK，删除部分
- 删除部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0101bf8394362d477beca81afee434f966a4bfe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827493"
---
# <a name="remove-section-in-a-network-inf-file"></a>网络 INF 文件中的 Remove 节





**NetClient**、 **NetTrans** 和 **空间** 组件支持删除部分，但不支持 **删除**)  (适配器的 **网络** 组件。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

网络类安装程序不跟踪适配器实例。 **删除删除** 其他适配器或多个适配器实例共享的文件的删除部分可能导致这些适配器或适配器实例无法工作。
如果有必要删除 **网络** 组件使用的驱动程序文件，请使用共同安装程序来跟踪使用该文件的所有驱动程序。 此类共同安装程序还应跟踪同一设备的多个实例，以及多个设备的驱动程序。 有关共同安装程序的详细信息，请参阅 [创建 INF 文件](../install/overview-of-inf-files.md)。

 

