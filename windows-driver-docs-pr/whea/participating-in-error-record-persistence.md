---
title: 参与错误记录持久性
description: 参与错误记录持久性
keywords:
- Windows 硬件错误体系结构 WDK，错误记录持久性
- WHEA WDK，错误记录暂留
- 硬件错误 WDK WHEA，错误记录暂留
- 错误，WDK WHEA，错误记录暂留
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误记录暂留
- PSHED 插件 WDK WHEA，错误记录暂留
- 错误记录持久性 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1497013f8293f1b00139cca5cb4735220fc09a3a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787093"
---
# <a name="participating-in-error-record-persistence"></a>参与错误记录持久性


若要参与错误记录持久性，PSHED 插件必须实现以下回调函数：

[*WriteErrorRecord*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_write_error_record)

[*ReadErrorRecord*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_read_error_record)

[*ClearErrorRecord*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_clear_error_record)

下面的代码示例演示如何实现这些回调函数。

```cpp
//
// The PSHED plug-in's WriteErrorRecord callback function
//
NTSTATUS
  WriteErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONG RecordLength,
    IN PWHEA_ERROR_RECORD ErrorRecord
    )
{
  // Check if dummy write operation
  if (Flags & WHEA_WRITE_FLAG_DUMMY)
  {
    return STATUS_SUCCESS;
  }

  // Write the error record to the persistent data storage
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to write the error record
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}

//
// The PSHED plug-in's ReadErrorRecord callback function
//
NTSTATUS
  ReadErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONGLONG ErrorRecordId,
    OUT ULONGLONG NextErrorRecordId,
    IN OUT PULONG RecordLength,
    IN OUT PWHEA_ERROR_RECORD ErrorRecord
    )
{
  ULONG Length;
  PWHEA_ERROR_RECORD Record;

  // Check if an error record that matches the
  // identifier in the ErrorRecordId parameter
  // exists in the persistent data storage
  if (...)
  {
    // Retrieve the length of the specified error
    // record from the persistent data storage
    Length = ...;

    // Check if the buffer is too small to contain
    // the error record
    if (*RecordLength < Length)
    {
      // Set the RecordLength to the required length
      *RecordLength = Length;

      // Return error status
      return STATUS_BUFFER_TOO_SMALL;
    }

    // Retrieve the error record from the
    // persistent data storage and copy it
    // into the buffer pointed to by the
    // ErrorRecord parameter.
    ...

    // If successful
    if (...)
    {
      // Set RecordLength to the length of the
      // error record
      *RecordLength = Length;

      // Check if there are any other error records
      // in the persistent data storage
      if (...)
      {
        // Return the identifier of the next
        // error record
        *NextErrorRecordId = ...;
      }

      // No other error records
      else
      {
        // Return the identifier of this error record
        *NextErrorRecordId = ErrorRecordId;
      }

      // Return success status
      return STATUS_SUCCESS;
    }

    // Failed to read the error record
    else
    {
      // Return error status
      return STATUS_UNSUCCESSFUL;
    }
  }

  // The error record does not exist in the
  // persistent data storage
  else
  {
    // Return error status
    return STATUS_OBJECT_NOT_FOUND;
  }
}

//
// The PSHED plug-in's ClearErrorRecord callback function
//
NTSTATUS
  ClearErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONGLONG ErrorRecordId
    )
{
  // Clear the error record that matches the specified
  // error record identifier from the persistent data
  // storage.
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to clear the error record
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

参与错误记录持久性的 PSHED 插件必须在向操作系统 [注册](registering-a-pshed-plug-in.md)自身时指定 **PshedFAErrorRecordPersistence** 标志。

有关错误记录持久性的详细信息，请参阅 [错误记录永久性机制](error-record-persistence-mechanism.md)。

 

