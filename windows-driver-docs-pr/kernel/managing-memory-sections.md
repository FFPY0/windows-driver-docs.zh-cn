---
title: 管理内存节
description: 管理内存节
keywords:
- 内存段 WDK 内核
- 节对象 WDK 内核
- 查看 WDK 内存部分
- 映射节视图
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9136e741c4ef251757ddf61a7752ec34a896e254
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793525"
---
# <a name="managing-memory-sections"></a>管理内存节





驱动程序可以通过调用 [**ZwCreateSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection)创建节对象，这将返回节对象的句柄。 使用 *FileHandle* 参数指定后备文件，如果该部分未进行文件支持，则为 **NULL** 。 可以使用 [**ZwOpenSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)打开节对象的其他句柄。

若要使属于节对象的数据可在当前进程的地址空间中访问，必须映射该部分的视图。 驱动程序可以使用 [**ZwMapViewOfSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection) 例程将节的视图映射到当前进程的地址空间。 *SectionOffset* 参数指定视图在部分中开始的字节偏移量， *ViewSize* 指定要映射的字节数。

*保护* 参数指定对视图所允许的操作。 为 \_ 只读视图指定页 READONLY，为 \_ 读/写视图指定页读写，并为页 \_ WRITECOPY 指定 "写入时复制" 视图。

在访问虚拟内存范围之前，不会为视图分配物理内存。 第一次访问内存范围会导致页错误;然后，系统将分配一个页来保存该内存位置。 如果该部分是文件支持的，则系统将读取对应于该页面的文件内容并将其复制到内存。  (请注意，未使用的节对象和视图会将某些分页和非分页池用于簿记目的。 ) 

当驱动程序不再使用某一视图时，它通过调用 [**ZwUnmapViewOfSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwunmapviewofsection)来 messagebox 取消它。 当驱动程序不再使用 section 对象后，它将关闭使用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)的节句柄。 请注意，在映射视图后，不会映射其他任何视图，可以安全地在节句柄上立即调用 **ZwClose** ;视图 (和节对象) 会继续存在，直到取消映射视图。 这是建议的做法，因为它降低了驱动程序未能关闭句柄的风险。

 

