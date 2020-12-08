---
title: FLT_FILE_NAME_OPTIONS
description: FLT \_ 文件名 \_ \_ 选项
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e26eb50b8e6ffff708fbef1e491fe1230e05a9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790647"
---
# <a name="flt_file_name_options"></a>FLT \_ 文件名 \_ \_ 选项

FLT_FILE_NAME_OPTIONS 类型是标志的位掩码，它指定文件名格式、查询方法和文件名信息查询的标志。

```cpp
typedef ULONG FLT_FILE_NAME_OPTIONS;
#define FLT_VALID_FILE_NAME_FORMATS                       0x000000ff
    #define FLT_FILE_NAME_NORMALIZED                      0x00000001
    #define FLT_FILE_NAME_OPENED                          0x00000002
    #define FLT_FILE_NAME_SHORT                           0x00000003
#define FLT_VALID_FILE_NAME_QUERY_METHODS                 0x0000ff00
    #define FLT_FILE_NAME_QUERY_DEFAULT                   0x00000100
    #define FLT_FILE_NAME_QUERY_CACHE_ONLY                0x00000200
    #define FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY           0x00000300
    #define FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP 0x00000400
#define FLT_VALID_FILE_NAME_FLAGS                         0xff000000
    #define FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER   0x01000000
    #define FLT_FILE_NAME_DO_NOT_CACHE                    0x02000000
    #define FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE          0x04000000
```

位0到7指示文件格式，可以使用 [**FltGetFileNameFormat**](/previous-versions/ff543030(v=vs.85)) 宏对其进行查询。 有关这些格式的说明，请参阅 [**FLT_FILE_NAME_INFORMATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_file_name_information)。 当前定义了下列值。

| “值” | 含义 |
| ----- | ------- |
| FLT_FILE_NAME_NORMALIZED | 文件的规范化名称。 |
| FLT_FILE_NAME_OPENED | 打开此文件的句柄时使用的名称。 此名称不规范化。 |
| FLT_FILE_NAME_SHORT | 文件的简短 (8.3) 名称。 文件的短名称不包括卷名称、目录路径或流名称。 此名称不规范化。 |

Bits 8 到15指定筛选器管理器要使用的文件名查询方法，可以使用 [**FltGetFileNameQueryMethod**](/previous-versions/ff543040(v=vs.85)) 宏对其进行查询。 有关这些值的说明，请参阅 [**FltGetFileNameInformation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformation)。 当前定义了下列值。

| “值” | 含义 |
| ----- | ------- |
| FLT_FILE_NAME_QUERY_DEFAULT | 如果无法在文件系统中查询文件名，则无需执行任何操作。 否则，请在筛选器管理器的名称缓存中查询文件名信息。 如果在缓存中找不到该名称，则查询文件系统并缓存结果。 |
| FLT_FILE_NAME_QUERY_CACHE_ONLY | 在筛选器管理器的名称缓存中查询文件名信息。 不查询文件系统。 |
| FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY | 在文件系统中查询文件名信息。 不要查询筛选器管理器的名称缓存，也不缓存文件系统查询的结果。 |
| FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP | 在筛选器管理器的名称缓存中查询文件名信息。 如果在缓存中找不到该名称，并且此名称当前是安全的，请在文件系统中查询文件名信息并缓存结果。 |

当前未使用位16到23。

名称提供程序 minifilters 使用 Bits 24 到31来指定文件名标志。 当前定义了下列值。

| “值” | 含义 |
| ----- | ------- |
| FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER | 名称提供程序微筛选器可以使用此标志来指定名称查询请求应重定向到其自身 (名称提供程序微筛选器) ，而不是堆栈中较低名称提供程序满足此要求。 |
| FLT_FILE_NAME_DO_NOT_CACHE | 此标志表示不应缓存从此查询检索到的名称。 名称提供程序 minifilters 在执行中间查询以生成名称时使用此标志。 |
| FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE | 名称提供程序微筛选器可以使用此标志来指定在创建后路径中查询名称是安全的，即使返回 STATUS_REPARSE 也是如此。 调用方负责确保 **>FileName** "字段未更改。 不要将此标志与装入点或符号链接重新分析点一起使用。 |

## <a name="requirements"></a>要求

标头 * * * *： fltkernel (包含 fltkernel) 


## <a name="related-topics"></a>相关主题

[**FLT_FILE_NAME_INFORMATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_file_name_information)

[**FltGetDestinationFileNameInformation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)

[**FltGetFileNameFormat**](/previous-versions/ff543030(v=vs.85))

[**FltGetFileNameInformation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformation)

[**FltGetFileNameInformationUnsafe**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformationunsafe)

[**FltGetFileNameQueryMethod**](/previous-versions/ff543040(v=vs.85))
