---
title: 使用分段筛选器的示例应用程序
description: 使用分段筛选器的示例应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd99639a337682f48a4578c6074c559bc50300a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816725"
---
# <a name="example-application-using-a-segmentation-filter"></a>示例：使用分段筛选器的应用程序





下面的代码示例演示了一个简单的应用程序如何使用分段筛选器。 为清楚起见，已省略错误检查代码，以及释放和释放接口指针和内存的代码。

```cpp
IWiaSegmentationFilter *pWiaSegmentationFilter = NULL;
IWiaTransferCallback *pMyWiaTransferCallback = NULL;
IWiaTransfer  *pWiaTransfer = NULL;

...

pWiaItem2->QueryInterface(IID_IWiaTransfer, (void**)&pWiaTransfer);

pMyWiaTransferCallback = new MyWiaTransferCallback();


//
// Do preview scan.
//    
pWiaTransfer->Download(lFlags, pMyWiaTransferCallback);

//
// If an application changes any properties in pWiaItem2, it
// should call IWiaPropertyStorage::GetPropertyStream on
// that item to save its property settings (so they can be
// restored) before calling IWiaSegmentationFilter::DetectRegions.
//

if (ReadPropertyLong(WIA_IPS_SEGMENTATION_FILTER, &lUseSegFilter) &&
    (lUseSegFilter == WIA_USE_SEGMENTATION_FILTER)
{
    bstrSegmentation = SysAllocStr(WIA_SEGMENTATION_FILTER_STR);

    pWiaItem2->GetExtension(bstrSegmentation,
                            IID_IWiaSegmentationFilter,
                           (void**)& pWiaSegmentationFilter);

//
// m_pInputStream is a pointer to the IStream that the application's
// implementation of MyWiaTransferCallback::GetNextStream
// returns.
//
// Note: If the application has changed any properties into
// pWiaItem2 since the call to Download, it must now restore
// these properties with IWiaPropertyStorage::SetPropertyStream.
//

//
// The application is responsible for resetting m_pInputStream
// before calling DetectRegions!
//
    LARGE_INTEGER  ul = {0};

    m_pInputStream->Seek(ul, STREAM_SEEK_SET, NULL);

    pWiaSegmentationFilter->DetectRegions(m_pInputStream,
                                          pWiaItem2);

   ...
}

//
// Display the subregions to the users (if segmentation was
// supported) and let them pick the images they want to scan,
// as well as change the properties in the child items

//
// For each child item, pChildItem, do the following ( alternatively,
// do a folder acquisition on pWiaItem2).
//
IWiaTransfer  *pWiaTransferChild= NULL;

pChildItem->QueryInterface(IID_IWiaTransfer,
                           (void**)& pWiaTransferChild);

pWiaTransferChild->Download(lFlags, pMyWiaTransferCallback); 
```

 

 




