---
title: D3DKMT \_ PINDIRECTFLIPRESOURCES 结构
description: 了解 \_ 保留供系统使用的 D3DKMT PINDIRECTFLIPRESOURCES 结构。 请勿在您的驱动程序中使用。
keywords:
- D3DKMT_PINDIRECTFLIPRESOURCES 结构显示设备
topic_type:
- apiref
api_name:
- D3DKMT_PINDIRECTFLIPRESOURCES
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 58c6db8383c82c2cb12bc6f43cbcee0d2e60d912
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793037"
---
# <a name="d3dkmt_pindirectflipresources-structure"></a>D3DKMT \_ PINDIRECTFLIPRESOURCES 结构


预留给系统使用。 请勿在您的驱动程序中使用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _D3DKMT_PINDIRECTFLIPRESOURCES {
  D3DKMT_HANDLE hDevice;
  UINT          ResourceCount;
  D3DKMT_HANDLE *pResourceList;
} D3DKMT_PINDIRECTFLIPRESOURCES;
```

<a name="members"></a>成员
-------

**hDevice**

**ResourceCount**

**pResourceList**

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmthk (包含 D3dkmthk) </td>
</tr>
</tbody>
</table>

 

 





