---
title: 检查 IRP_MJ_READ 操作的 Oplock 状态
description: 检查 IRP_MJ_READ 操作的 Oplock 状态
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: deb12d4a60f4b0d8b6be22c9b0a58ef3a04e3775
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793775"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_read-operation"></a>检查 IRP_MJ_READ 操作的 Oplock 状态

读取 *流* 时，将应用以下 [oplock 中断](./breaking-oplocks.md)条件。 如果 TxF 事务处理读取器执行读取，则不会执行此检查，因为事务读取器会排除编写器 (也就是说，持有 oplock 的编写器不能出现在所有) 上。

### <a name="conditions-for-level-2-filter-read-and-read-handle-request-types"></a>级别2、筛选、读取和 Read-Handle 请求类型的条件

- Oplock 不会中断。

- 不需要确认，操作会立即继续。

### <a name="conditions-for-level-1-batch-read-write-and-read-write-handle-request-types"></a>级别1、批处理、读写和读写句柄请求类型的条件

- 当读取操作发生在带有 oplock 键的 FILE_OBJECT 上时 IRP_MJ_READ 中断，该操作与拥有 oplock 的 FILE_OBJECT 的键不同。 如果 oplock 中断：

  - 级别1和批处理请求中断到级别2。

  - 要读取 Read-Write 请求中断。

  - 读写-处理请求中断到读取句柄。

- 必须先收到确认，然后才能继续操作。
