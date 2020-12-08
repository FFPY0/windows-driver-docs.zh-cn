---
title: 锁定和解锁流指针
description: 锁定和解锁流指针
keywords:
- 流指针 WDK AVStream、锁定和解锁
- 锁定的流指针 WDK AVStream
- 未锁定的流指针 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5038e225b86051d96bf38cde322ba0ef2d744b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794151"
---
# <a name="locking-and-unlocking-stream-pointers"></a>锁定和解锁流指针





每个流指针都保持锁定状态：锁定或解锁。

锁定的流指针保证引用队列中的数据。 无法取消锁定流指针指向的数据帧。 因此，微型驱动程序应最大程度地减少其持有锁定的流指针所花费的时间。

不保证解除锁定的流指针引用队列中的数据帧。 通过保存未锁定的流指针，微型驱动程序可以保留数据指针，但仍允许取消帧。

可以通过未锁定的流指针访问指向的数据。 如果在 [**KsStreamPointerClone**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)中提供的 *CancelCallback* 例程调用 [**KsStreamPointerDelete**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)，则应同步 *CancelCallback* 及其执行的任何数据访问。 微型驱动程序必须确保取消回调例程不会删除流指针，而另一个线程正在使用该指针。

如果取消回调例程未调用 **KsStreamPointerDelete**，则可能无需同步。

若要锁定流指针，请调用 [**KsStreamPointerLock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)。 若要解锁流指针，请调用 [**KsStreamPointerUnlock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)。

取消 IRP 后，AVStream 将为指向 IRP 内的帧的所有未锁定流指针调用取消回调。

仅在不使用前导和尾随边缘流指针时对其进行解锁。

 

