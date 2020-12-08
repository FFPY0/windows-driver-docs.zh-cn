---
title: 文件系统筛选器驱动程序类和类 GUID
description: 文件系统筛选器驱动程序类和类 GUID
keywords:
- Guid WDK 文件系统
- 类 Guid WDK 文件系统
- 类 WDK 文件系统
- 筛选器驱动程序 WDK 文件系统，类
- 文件系统筛选器驱动程序 WDK、类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ef1d91312ec087e2bf5d168e29ea13ee88dd967
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794949"
---
# <a name="file-system-filter-driver-classes-and-class-guids"></a>文件系统筛选器驱动程序类和类 GUID


## <span id="ddk_file_system_filter_driver_classes_and_class_guids_if"></span><span id="DDK_FILE_SYSTEM_FILTER_DRIVER_CLASSES_AND_CLASS_GUIDS_IF"></span>


Microsoft Windows XP 和更高版本的操作系统为文件系统筛选器驱动程序提供了安装程序类。 这些类提供系统提供的设备安装程序类为硬件设备提供的功能的子集。  (有关硬件设备安装程序类的详细信息，请参阅 [设备安装程序类](../install/overview-of-device-setup-classes.md)。 ) 

每个安装程序类都与一个类 GUID 相关联。 系统定义的类 Guid 是在 devguid 中定义的。

本主题列出了文件系统筛选器驱动程序的安装程序类。 在每个类的定义中， **class** 和 **ClassGuid** 项包含应在筛选器的 Inf 文件的 [**inf 版本部分**](../install/inf-version-section.md) 中指定的值。 筛选器驱动程序应使用与驱动程序的 INF 文件中指定的加载顺序组相匹配的类和 GUID。

在 INF 文件中为设备（而不是 **类** 类名称条目）提供适当的类 GUID 值，  =  *class-name* 可以显著提高搜索系统 INF 文件的性能。

以下列表包括文件系统筛选器驱动程序的系统定义的类和类 Guid。 此列表中的条目对应于在 Windows XP 和更高版本的操作系统中为文件系统筛选器驱动程序创建的加载顺序组。

**注意**   三个加载顺序组不会显示在列表中，因为它们不被视为安装类，因此不会为它们分配类 Guid： Filter、FSFilter Top 和 FSFilter 底端。

 

<span id="FSFilter_Activity_Monitor"></span><span id="fsfilter_activity_monitor"></span><span id="FSFILTER_ACTIVITY_MONITOR"></span>FSFilter 活动监视器<br/>
类 = ActivityMonitor<br/>
ClassGuid = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}

<span id="FSFilter_Undelete"></span><span id="fsfilter_undelete"></span><span id="FSFILTER_UNDELETE"></span>FSFilter 删除<br/>
类 = 撤消删除<br/>
ClassGuid = {fe8f1572-c67a-48c0-bbac-0b5c6d66cafb}

<span id="FSFilter_Anti-Virus"></span><span id="fsfilter_anti-virus"></span><span id="FSFILTER_ANTI-VIRUS"></span>FSFilter 防病毒<br/>
类 = 防病毒<br/>
ClassGuid = {b1d1a169-c54f-4379-81db-bee7d88d7454}

<span id="FSFilter_Replication"></span><span id="fsfilter_replication"></span><span id="FSFILTER_REPLICATION"></span>FSFilter 复制<br/>
类 = 复制<br/>
ClassGuid = {48d3ebc4-4cf8-48ff-b869-9c68ad42eb9f}

<span id="FSFilter_Continuous_Backup"></span><span id="fsfilter_continuous_backup"></span><span id="FSFILTER_CONTINUOUS_BACKUP"></span>FSFilter 连续备份<br/>
类 = ContinuousBackup<br/>
ClassGuid = {71aa14f8-6fad-4622-ad77-92bb9d7e6947}

<span id="FSFilter_Content_Screener"></span><span id="fsfilter_content_screener"></span><span id="FSFILTER_CONTENT_SCREENER"></span>FSFilter 内容筛选程序<br/>
类 = ContentScreener<br/>
ClassGuid = {3e3f0674-c83c-4558-bb26-9820e1eba5c5}

<span id="FSFilter_Quota_Management"></span><span id="fsfilter_quota_management"></span><span id="FSFILTER_QUOTA_MANAGEMENT"></span>FSFilter 配额管理<br/>
类 = QuotaManagement<br/>
ClassGuid = {8503c911-a6c7-4919-8f79-5028f5866b0c}

<span id="FSFilter_Cluster_File_System"></span><span id="fsfilter_cluster_file_system"></span><span id="FSFILTER_CLUSTER_FILE_SYSTEM"></span>FSFilter 群集文件系统<br/>
类 = CFSMetaDataServer<br/>
ClassGuid = {cdcf0939-b75b-4630-bf76-80f7ba655884}

<span id="FSFilter_HSM"></span><span id="fsfilter_hsm"></span><span id="FSFILTER_HSM"></span>FSFilter HSM<br/>
类 = HSM<br/>
ClassGuid = {d546500a-2aeb-45f6-9482-f4b1799c3177}

<span id="FSFilter_Compression"></span><span id="fsfilter_compression"></span><span id="FSFILTER_COMPRESSION"></span>FSFilter 压缩<br/>
类 = 压缩<br/>
ClassGuid = {f3586baf-b5aa-49b5-8d6c-0569284c639f}

<span id="FSFilter_Encryption"></span><span id="fsfilter_encryption"></span><span id="FSFILTER_ENCRYPTION"></span>FSFilter 加密<br/>
类 = 加密<br/>
ClassGuid = {a0a701c0-a511-42ff-aa6c-06dc0395576f}

<span id="FSFilter_Physical_Quota_Management"></span><span id="fsfilter_physical_quota_management"></span><span id="FSFILTER_PHYSICAL_QUOTA_MANAGEMENT"></span>FSFilter 物理配额管理<br/>
类 = PhysicalQuotaManagement<br/>
ClassGuid = {6a0a8e78-bba6-4fc4-a709-1e33cd09d67e}

<span id="FSFilter_Open_File"></span><span id="fsfilter_open_file"></span><span id="FSFILTER_OPEN_FILE"></span>FSFilter 打开文件<br/>
类 = OpenFileBackup<br/>
ClassGuid = {f8ecafa6-66d1-41a5-899b-66585d7216b7}

<span id="FSFilter_Security_Enhancer"></span><span id="fsfilter_security_enhancer"></span><span id="FSFILTER_SECURITY_ENHANCER"></span>FSFilter Security 不得不一直<br/>
类 = SecurityEnhancer<br/>
ClassGuid = {d02bc3da-0c8e-4945-9bd5-f1883c226c8c}

<span id="FSFilter_Copy_Protection"></span><span id="fsfilter_copy_protection"></span><span id="FSFILTER_COPY_PROTECTION"></span>FSFilter 复制保护<br/>
类 = CopyProtection<br/>
ClassGuid = {89786ff1-9c12-402f-9c9e-17753c7f4375}

<span id="FSFilter_System"></span><span id="fsfilter_system"></span><span id="FSFILTER_SYSTEM"></span>FSFilter 系统<br/>
类 = FSFilterSystem<br/>
ClassGuid = {5d1b9aaa-01e2-46af-849f-272b3f324c46}

<span id="FSFilter_Infrastructure"></span><span id="fsfilter_infrastructure"></span><span id="FSFILTER_INFRASTRUCTURE"></span>FSFilter 基础结构<br/>
类 = 基础结构<br/>
ClassGuid = {e55fa6f9-128c-4d04-abab-630c74b1453a}
 

