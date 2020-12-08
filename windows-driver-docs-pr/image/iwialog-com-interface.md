---
title: IWiaLog COM 接口
description: IWiaLog COM 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29b11f10049965f7a56b7ebc8d821f5b3ccdb698
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808757"
---
# <a name="iwialog-com-interface"></a>IWiaLog COM 接口





[**IWiaLog 接口**](/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwialog)在 MICROSOFT Windows XP 和更高版本中已过时，不再受支持。 请改用 WIA 诊断日志宏。

提供它只是为了实现向后兼容性。 此接口中的方法允许微型驱动程序将错误、跟踪和警告消息写入日志。 **IWiaLog** 接口提供以下方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-initializelog" data-raw-source="[&lt;strong&gt;IWiaLog::InitializeLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-initializelog)"><strong>IWiaLog：： InitializeLog</strong></a></p></td>
<td><p>初始化日志记录实用程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-log" data-raw-source="[&lt;strong&gt;IWiaLog::Log&lt;/strong&gt;](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-log)"><strong>IWiaLog：： Log</strong></a></p></td>
<td><p>将消息记录到文件或其他目标。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-hresult" data-raw-source="[&lt;strong&gt;IWiaLog::hResult&lt;/strong&gt;](/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-hresult)"><strong>IWiaLog：： hResult</strong></a></p></td>
<td><p>将 HRESULT 转换为字符串。</p></td>
</tr>
</tbody>
</table>

 

有关此接口的详细信息，请参阅 [IWiaLog 接口和诊断日志宏](/windows-hardware/drivers/ddi/_image/index)。

