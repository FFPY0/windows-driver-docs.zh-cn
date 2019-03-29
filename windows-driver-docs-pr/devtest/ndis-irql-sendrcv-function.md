---
title: Irql\_SendRcv\_函数规则 (ndis)
description: Irql\_SendRcv\_函数规则指定的发送和接收的 NDIS 驱动程序必须在正确的 IRQL 级别调用函数。
ms.assetid: adca6ebf-aa78-4fd6-b75b-4a6d856d03ca
ms.date: 05/21/2018
keywords:
- Irql_SendRcv_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_SendRcv_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c51299daa2df05c73f735d0be8207d8808901357
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546527"
---
# <a name="irqlsendrcvfunction-rule-ndis"></a>Irql\_SendRcv\_函数规则 (ndis)


**Irql\_SendRcv\_函数**规则指定发送和接收的 NDIS 驱动程序必须在正确的 IRQL 级别调用函数。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_SendRcv_Function</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisCancelSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561623)
[**NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598) 
 [ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)
[**NdisReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564534) 
 [ **NdisSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff564535)
 

 




