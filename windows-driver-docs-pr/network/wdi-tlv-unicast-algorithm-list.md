---
title: WDI_TLV_UNICAST_ALGORITHM_LIST
description: WDI_TLV_UNICAST_ALGORITHM_LIST 是 TLV 包含单播数据算法对的数组。
ms.assetid: E216BE6A-5425-498F-ABDE-1229170DA5DB
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_UNICAST_ALGORITHM_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b5351e1998506075789ccfe78d12b2380ac01ccb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522691"
---
# <a name="wditlvunicastalgorithmlist"></a>WDI\_TLV\_单播\_算法\_列表


WDI\_TLV\_单播\_算法\_列表是包含数组的单播数据算法对 TLV。

## <a name="tlv-type"></a>TLV 类型


0x13

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_ALGO\_对元素。 该数组必须包含一个或多个元素。

**请注意**  WDI\_ALGO\_对不是 WDI 结构。 它定义在 WDI TLV 分析器生成器，并仅供文档使用。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                 | 描述                                            |
|----------------------|--------------------------------------------------------|
| WDI\_ALGO\_PAIRS\[\] | 身份验证和加密算法对的数组。 |

 

WDI\_ALGO\_对以下元素组成。

| 在任务栏的搜索框中键入  | 描述                                                                                     |
|-------|-------------------------------------------------------------------------------------------------|
| UINT8 | 如中所定义的身份验证算法[ **WDI\_身份验证\_算法**](https://msdn.microsoft.com/library/windows/hardware/dn897792)。 |
| UINT8 | 如中所定义的密码算法[ **WDI\_密码\_算法**](https://msdn.microsoft.com/library/windows/hardware/dn897802)。     |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 



