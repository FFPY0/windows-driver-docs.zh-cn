---
title: 默认规则集 (KMDF)
description: 了解 (KMDF) 的默认规则集，它指定了在分析驱动程序时要使用的建议规则集。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: a494145dfaaa8916bcab9631119b90ddf49fc133
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839777"
---
# <a name="default-rule-set-kmdf"></a>默认规则集 (KMDF)


默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。

[DDI 用量规则集 (KMDF) ](ddi-usage-rule-set--kmdf-.md) 
[IrpProcessing 规则集 (KMDF) ](irpprocessing-rule-set--kmdf-.md) 
[Irql 规则集 (KMDF) ](irql-rule-set--kmdf-.md) 
[ (KMDF) ](locking-rule-set--kmdf-.md) 
 锁定规则集[其他规则集 (KMDF) ](miscellaneous-rule-set--kmdf-.md) 
[RequestProcessing 规则集 (KMDF) ](requestprocessing-rule-set--kmdf-.md) 
[Usb 规则集 (KMDF) ](usb-rule-set--kmdf-.md) 
**选择默认规则**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **默认**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

