---
title: 事务对象
description: 事务对象
keywords:
- 事务 WDK KTM，对象
- 事务 WDK KTM
- 事务性客户端 WDK KTM，创建事务
- 内核事务管理器 WDK，事务
- KTM WDK，事务
- 事务对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae4155137559dfe88eed00c073c4ae9433f15469
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814259"
---
# <a name="transaction-objects"></a>事务对象


*Transaction 对象* 表示事务。 事务客户端创建一个事务，执行一些工作，并提交或回滚该事务。

KTM 提供一组可供内核模式事务客户端调用的 [事务对象例程](/windows-hardware/drivers/ddi/index) 。 KTM 还提供用户模式应用程序可以调用的一组类似的用户模式例程。 有关用户模式例程的详细信息，请参阅 Microsoft Windows SDK。

当客户端调用 [**ZwCreateTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)时，KTM 会创建事务对象。 客户端可以调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) 或 [**ZwRollbackTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction) 来提交或回滚事务。

[TPS 组件](understanding-tps-components.md) 可以调用 [**ZwOpenTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction) 来打开事务对象的其他句柄。

客户端通过调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)关闭它们对事务对象的句柄。 如果在提交事务对象之前结束最后一个句柄，则 KTM 会将事务 \_ 通知 \_ 回滚通知发送到所有具有事务登记的资源管理器。

当最后一个句柄关闭并且 KTM 释放了对该对象的所有引用后，操作系统将删除该对象。

 

