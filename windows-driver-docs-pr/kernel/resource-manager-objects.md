---
title: 资源管理器对象
description: 资源管理器对象
keywords:
- 资源管理器 WDK KTM，对象
- 资源管理器 WDK KTM
- 资源管理器 WDK KTM，例程
- 内核事务管理器 WDK，资源管理器
- KTM WDK，资源管理器
- resource manager 对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6c7dbfe698f1d79970f9e7dfc15398e05ec874
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091200"
---
# <a name="resource-manager-objects"></a>资源管理器对象


*资源管理器对象* 表示资源管理器。 每个资源管理器都必须调用 [**ZwCreateResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager) 来向 KTM 注册自身。

KTM 提供一组可供内核模式资源管理器调用的资源管理器对象例程。 KTM 还提供用户模式应用程序可以调用的一组类似的用户模式例程。 有关用户模式例程的详细信息，请参阅 Microsoft Windows SDK。

资源管理器调用 **ZwCreateResourceManager** 时，KTM 会创建资源管理器对象。

[TPS 组件](understanding-tps-components.md) 可以调用 [**ZwOpenResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager) 来打开资源管理器对象的其他句柄。 但大多数 TPS 设计不需要额外的开放句柄。

资源管理器通过调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)关闭其对资源管理器对象的句柄。 如果最后一个句柄已关闭，并且如果 resource manager 仍在尚未提交的事务中登记，则 KTM 会将事务 \_ 通知 \_ 回滚通知发送到与这些登记关联的事务的所有资源管理器。

当最后一个句柄关闭并且 KTM 释放了对该对象的所有引用后，操作系统将删除该对象。

 

