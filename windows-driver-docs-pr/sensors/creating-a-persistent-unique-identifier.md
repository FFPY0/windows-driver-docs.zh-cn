---
title: '为传感器创建持久的唯一标识符 (早期版本) '
description: '为传感器创建持久的唯一标识符 (早期版本) '
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b18b22f81be973d0b9cb717bb7d55326c6e1921a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831041"
---
# <a name="creating-a-persistent-unique-identifier-for-a-sensor-previous-version"></a>为传感器创建持久的唯一标识符 (早期版本) 


驱动程序必须为每个传感器 (PUID) 创建永久唯一标识符。 PUID 是跨会话存储并在设备上唯一标识该对象的 GUID 值。 当查询名为传感器 \_ 属性 \_ 持久 \_ 唯一 ID 的属性时，驱动程序必须返回 PUID 值 \_ 。 如果设备包含多个传感器，则必须为每个传感器分配其自己的 PUID。 应用程序可以通过调用传感器 API 中的 [ISensor：： GetID](/windows/win32/api/sensorsapi/nf-sensorsapi-isensor-getid) 方法来检索此 ID。

当传感器第一次连接到计算机时，应该为每个传感器创建新的 PUID，并存储此值供以后使用。

在初始化传感器类扩展之前，驱动程序应创建或检索 PUID，例如，在 [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)中调用该扩展时。 此方法提供一个指针，该指针指向表示传感器的 [IWDFDevice](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice) 接口。 此指针可用于访问每个设备的特定属性存储。

下面的代码示例创建一个函数，该函数根据需要创建、存储和检索 PUID。

```cpp
// Sets the persistent unique ID property in the WDF property store
// and returns the GUID for use in PortableDeviceValues property bags.
HRESULT CMyDevice::GetUniqueID(__in IWDFDevice* pWdfDevice,
                                            __in LPCWSTR wszSensorID, __out GUID* puid)
{
    HRESULT hr = S_OK;

    // Smart pointer to the WDF property store.
    // This pointer can store or retrieve the ID.
    CComPtr<IWDFNamedPropertyStore> spPropStore;
    if (SUCCEEDED(hr))
    {
        // Create the property store for this device or
        // retrieve the existing one.
        hr = pWdfDevice->RetrieveDevicePropertyStore(NULL, WdfPropertyStoreCreateIfMissing, &spPropStore, NULL);
    }

    if(SUCCEEDED(hr))
    {
        GUID idGuid;

        PROPVARIANT vID;

        // Try to get the PUID value previously stored as a string.
        hr = spPropStore->GetNamedValue(wszSensorID, &vID);
        if (SUCCEEDED(hr))
        {
            // Convert the PUID string to a GUID.
            hr = ::CLSIDFromString(vID.bstrVal, &idGuid);
        }
        else
        {
            // There was no value in the store, so create a new value.
            hr = ::CoCreateGuid(&idGuid);

            if (SUCCEEDED(hr))
            {
                // Convert the GUID to a string.
                LPOLESTR lpszGUID = NULL;
                hr = ::StringFromCLSID(idGuid, &lpszGUID);
                if (SUCCEEDED(hr))
                {
                    // Put the new value into the property store.
                    PropVariantInit(&vID);
                    vID.vt = VT_LPWSTR;
                    vID.pwszVal = lpszGUID;
                    hr = spPropStore->SetNamedValue(wszSensorID, &vID);
                    PropVariantClear(&vID);
                }
            }
        }

        // Return the PUID GUID.
        *puid = idGuid;
    }

    return hr;
}
```

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](../gnss/sensors-geolocation-driver-sample.md)
