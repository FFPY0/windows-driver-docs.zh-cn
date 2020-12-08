---
title: Bug 检查 0x1C4 DRIVER_VERIFIER_DETECTED_VIOLATION_LIVEDUMP
description: DRIVER_VERIFIER_DETECTED_VIOLATION_LIVEDUMP bug 检查的值为0x000001C4。
keywords:
- Bug 检查 0x1C4 DRIVER_VERIFIER_DETECTED_VIOLATION_LIVEDUMP
- DRIVER_VERIFIER_DETECTED_VIOLATION_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DETECTED_VIOLATION_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db492f7f48ca47f39d47dc2816345cc15d5ccf70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836891"
---
# <a name="bug-check-0x1c4-driver_verifier_detected_violation_livedump"></a>Bug 检查0x1C4：驱动程序 \_ 验证程序 \_ 检测到 \_ 违反 \_ LIVEDUMP


驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突 \_ LIVEDUMP bug 检查的值为0x000001C4。 这表示检测到尝试损坏系统的设备驱动程序。 这是因为在注册表中指定的驱动程序被管理员)  (可疑，并且内核已启用对此驱动程序的大量检查。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。



## <a name="driver_verifier_detected_violation_livedump-parameters"></a>驱动程序 \_ 验证程序 \_ 检测到 \_ 违反 \_ LIVEDUMP 参数

| 参数 | 描述                              |
|-----------|------------------------------------------|
|1| 驱动程序冲突的子类。 请参阅下面的值。|
|2| 请参阅下面的值。 |
|3| 请参阅下面的值。 |
|4| 请参阅下面的值。 |


**值**

```values
0x00081001: ID of the 'KsDeviceMutex' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00081002: ID of the 'KsStreamPointerClone' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00081003: ID of the 'KsStreamPointerLock' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved 

0x00081004: ID of the 'KsStreamPointerUnlock' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00081005: ID of the 'KsCallbackReturn' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00081006: ID of the 'KsIrqlDeviceCallbacks' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00081007: ID of the 'KsIrqlFilterCallbacks' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00081008: ID of the 'KsIrqlPinCallbacks' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00081009: ID of the 'KsIrqlDDIs' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0008100A: ID of the 'KsFilterMutex' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0008100B: ID of the 'KsProcessingMutex' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00082001: ID of the 'KsTimedPinSetDeviceState' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00082002: ID of the 'KsTimedDeviceCallbacks' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00082003: ID of the 'KsTimedFilterCallbacks' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00082004: ID of the 'KsTimedPinCallbacks' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00082005: ID of the 'KsTimedProcessingMutex' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00071001: ID of the 'PcIrqlDDIs' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00071003: ID of the 'PcIrqlIport' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00071004: ID of the 'PcUnmapAllocatedPages' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00071005: ID of the 'PcAllocatedPages' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00071006: ID of the 'PcRegisterAdapterPower' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00071007: ID of the 'PcAddAdapterDevice' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00071008: ID of the 'PcPropertyRequest' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00071009: ID of the 'PcAllocateAndMapPages' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0007100A: ID of the 'PcPoRequestPowerIrp' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00072001: ID of the 'PcTimedWaveRtStreamSetState' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00020002: ID of the 'IrqlApcLte' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020003: ID of the 'IrqlDispatch' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020004: ID of the 'IrqlExAllocatePool' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020005: ID of the 'IrqlExApcLte1' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020006: ID of the 'IrqlExApcLte2' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020007: ID of the 'IrqlExApcLte3' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020008: ID of the 'IrqlExPassive' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020009: ID of the 'IrqlIoApcLte' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002000A: ID of the 'IrqlIoPassive1' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002000B: ID of the 'IrqlIoPassive2' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002000C: ID of the 'IrqlIoPassive3' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002000D: ID of the 'IrqlIoPassive4' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002000E: ID of the 'IrqlIoPassive5' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002000F: ID of the 'IrqlKeApcLte1' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020010: ID of the 'IrqlKeApcLte2' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020011: ID of the 'IrqlKeDispatchLte' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020015: ID of the 'IrqlKeReleaseSpinLock' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020016: ID of the 'IrqlKeSetEvent' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020019: ID of the 'IrqlMmApcLte' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002001A: ID of the 'IrqlMmDispatch' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002001B: ID of the 'IrqlObPassive' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002001C: ID of the 'IrqlPsPassive' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002001D: ID of the 'IrqlReturn' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0002001E: ID of the 'IrqlRtlPassive' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0002001F: ID of the 'IrqlZwPassive' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00020022: ID of the 'IrqlIoDispatch' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00040003: ID of the 'CriticalRegions' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00040006: ID of the 'QueuedSpinLock' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00040007: ID of the 'QueuedSpinLockRelease' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00040009: ID of the 'SpinLock' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0004000A: ID of the 'SpinlockRelease' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0004000E: ID of the 'GuardedRegions' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0004100B: ID of the 'RequestedPowerIrp' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x0004100F: ID of the 'IoSetCompletionExCompleteIrp' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00043006: ID of the 'PnpRemove' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00091001: ID of the 'NdisOidComplete' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00091002: ID of the 'NdisOidDoubleComplete' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0009100E: ID of the 'NdisOidDoubleRequest' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00092003: ID of the 'NdisTimedOidComplete' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0009200D: ID of the 'NdisTimedDataSend' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0009200F: ID of the 'NdisTimedDataHang' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00092010: ID of the 'NdisFilterTimedPauseComplete' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00092011: ID of the 'NdisFilterTimedDataSend' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00092012: ID of the 'NdisFilterTimedDataReceive' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00093004: ID of the 'WlanAssociation' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00093005: ID of the 'WlanConnectionRoaming' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00093006: ID of the 'WlanDisassociation' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00093101: ID of the 'WlanAssert' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Reserved  
    Parameter 4 - Reserved  

0x00094007: ID of the 'WlanTimedAssociation' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00094008: ID of the 'WlanTimedConnectionRoaming' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x00094009: ID of the 'WlanTimedConnectRequest' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0009400B: ID of the 'WlanTimedLinkQuality' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo). 

0x0009400C: ID of the 'WlanTimedScan' rule that was violated.
    Parameter 2 - A pointer to the string describing the violated rule condition.
    Parameter 3 - Address of internal rule state (second argument to !ruleinfo).
    Parameter 4 - Address of supplemental states (third argument to !ruleinfo).
```
