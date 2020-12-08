---
title: 演示如何实现帮助程序方法的代码示例
description: 演示如何实现帮助程序方法的代码示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d34fc671fe82e37c7d999c4f5e0609f076d88813
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839261"
---
# <a name="code-example-for-implementing-helper-methods"></a>演示如何实现帮助程序方法的代码示例

> [!IMPORTANT]  
> 已弃用 WSD 争取冠军宝座功能，并且2018中将删除所有与 WSD 争取冠军宝座相关的文档。

下面的代码示例演示了用于初始化 WSD 质询接口并注册设备质询的帮助器方法的实现。

```cpp
/**************************************************************************\
* CWSDDevice::InitializeChallengeInterface
*
* Initializes the WSD challenge API interface
*
* Arguments:
*
*    None
*
* Return Value:
*
*    S_OK if operation is successful, an error HRESULT otherwise
*
\**************************************************************************/

HRESULT
CWSDDevice::InitializeChallengeInterface()
{
    HRESULT hr = S_OK;
    DWORD dwErr = NO_ERROR; 
    WCHAR wszDllPath[MAX_PATH + 1] = {0} ;

    //
    // Reset the previous initialization, if any
    //
    if (m_pfnRegisterDeviceToChallenge)
    {
        UnInitializeChallengeInterface();
    }

    //
    // Set up the path name for the WSD Challenge DLL
    //
    if (!GetSystemDirectory(wszDllPath, sizeof(wszDllPath) / sizeof(wszDllPath[0])))
    {
        dwErr = ::GetLastError();
        hr = HRESULT_FROM_WIN32(dwErr);
        if (SUCCEEDED(hr))
        {
            hr = E_FAIL;
        }
        WIAS_ERROR((g_hInst, "GetSystemDirectory failed (0x%08X), hr = 0x%08X", dwErr, hr));
    }
    if (SUCCEEDED(hr))
    {
        hr = StringCbCat(wszDllPath, sizeof(wszDllPath), WSDCHNGR_DLL_NAME);
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "StringCbCat(%ws, %ws) failed, hr = 0x%08X", wszDllPath, WSDCHNGR_DLL_NAME, hr));
        }
    }

    //
    // Load the WSD Challenge DLL
    //
    if (SUCCEEDED(hr))
    {
        m_hChallengeDll = LoadLibrary(wszDllPath);
        if (!m_hChallengeDll)
        {
            dwErr = ::GetLastError();
            hr = HRESULT_FROM_WIN32(dwErr);
            if (SUCCEEDED(hr))
            {
                hr = E_FAIL;
            }
            WIAS_ERROR((g_hInst, "LoadLibrary(%ws) failed (0x%08X), hr = 0x%08X", wszDllPath, dwErr, hr));
        }
    }

    //
    // Find the WSDCHNGRInitialize API
    //
    if (SUCCEEDED(hr))
    {
        m_pfnInitializeChallenge = (PFN_WSDCHNR_INITIALIZE)GetProcAddress(m_hChallengeDll, WSDCHNR_INITIALIZE);
        if (!m_pfnInitializeChallenge)
        {
            dwErr = ::GetLastError();
            hr = HRESULT_FROM_WIN32(dwErr);
            if (SUCCEEDED(hr))
            {
                hr = E_FAIL;
            }
            WIAS_ERROR((g_hInst, "GetProcAddress(%s) failed (0x%08X), hr = 0x%08X", WSDCHNR_INITIALIZE, dwErr, hr));
        }
    }

    //
    // Find the WSDCHNGRShutdown API
    //
    if (SUCCEEDED(hr))
    {
        m_pfnShutdownChallenge = (PFN_WSDCHNR_SHUTDOWN)GetProcAddress(m_hChallengeDll, WSDCHNR_SHUTDOWN);
        if (!m_pfnShutdownChallenge)
        {
            dwErr = ::GetLastError();
            hr = HRESULT_FROM_WIN32(dwErr);
            if (SUCCEEDED(hr))
            {
                hr = E_FAIL;
            }
            WIAS_ERROR((g_hInst, "GetProcAddress(%s) failed (0x%08X), hr = 0x%08X", WSDCHNR_SHUTDOWN, dwErr, hr));
        }
    }

    //
    // Find the WSDCHNGRRegisterDeviceToChallenge API
    //
    if (SUCCEEDED(hr))
    {
        m_pfnRegisterDeviceToChallenge = (PFN_WSDCHNR_REGISTER_DEVICE_TO_CHALLENGE)
            GetProcAddress(m_hChallengeDll, WSDCHNR_REGISTER_DEVICE_TO_CHALLENGE);

        if (!m_pfnRegisterDeviceToChallenge)
        {
            dwErr = ::GetLastError();
            hr = HRESULT_FROM_WIN32(dwErr);
            if (SUCCEEDED(hr))
            {
                hr = E_FAIL;
            }
            WIAS_ERROR((g_hInst, "GetProcAddress(%s) failed (0x%08X), hr = 0x%08X", WSDCHNR_REGISTER_DEVICE_TO_CHALLENGE, dwErr, hr));
        }
    }
 
    //
    // Call WSDCHNGRInitialize
    // 
    if (SUCCEEDED(hr))
    {
        hr = (*m_pfnInitializeChallenge)();
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "WSDCHNGRInitialize failed, hr = 0x%08X", hr));
        }
    }

    if (FAILED(hr))
    {
        UnInitializeChallengeInterface();
    }

    return hr;
}

/**************************************************************************\
* CWSDDevice::UnInitializeChallengeInterface
*
* Uninitializes the WSD challenge API interface
*
* Arguments:
*
*    None
*
* Return Value:
*
*    S_OK if operation is successful, an error HRESULT otherwise
*
\**************************************************************************/

void
CWSDDevice::UnInitializeChallengeInterface()
{
    HRESULT hr = S_OK;

    if ((m_hChallengeDll) && (m_pfnShutdownChallenge))
    {
        hr = (*m_pfnShutdownChallenge)();
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "WSDCHNGRShutdown failed, hr = 0x%08X", hr));
        }
    }

    if (m_hChallengeDll)
    {
        FreeLibrary(m_hChallengeDll);
        m_hChallengeDll = NULL;

    }

    m_pfnRegisterDeviceToChallenge = NULL;
    m_pfnInitializeChallenge = NULL;
    m_pfnShutdownChallenge = NULL;

    return;
}

/**************************************************************************\
* CWSDDevice::RegisterDeviceToChallenge
*
* Registers the device to be challenged by WSDCHNGR.DLL
*
* Arguments:
*
*    None
*
* Return Value:
*
*    S_OK if operation is successful or the challenge interface is disabled, 
*    S_FALSE if the device is already registered, an error HRESULT otherwise
*
\**************************************************************************/

HRESULT
CWSDDevice::RegisterDeviceToChallenge()
{
    HRESULT hr = S_OK;
    if (!m_pFunctionInstance)
    {
        hr = E_POINTER;
        WIAS_ERROR((g_hInst, "Invalid IFunctionInstance pointer, hr = 0x%08X", hr));    
    }

    if (SUCCEEDED(hr))
    {
        if (m_pfnRegisterDeviceToChallenge)
        {
            WIAS_TRACE((g_hInst, "Registering device to challenge.."));
 
            hr = (*m_pfnRegisterDeviceToChallenge)(m_pFunctionInstance);    
            if (FAILED(hr))
            {
                WIAS_ERROR((g_hInst, "WSDCHNGRRegisterDeviceToChallenge failed, hr = 0x%08X", hr));
            }
        }
        else 
        {
            WIAS_TRACE((g_hInst, "Challenge interface disabled or not initialized, hr = 0x%08X", hr));
        }
    }

    if (S_OK == hr)
    {
        //
        // WSDCHNGRRegisterDeviceToChallenge returns S_FALSE when the device is already registered
        //
        WIAS_TRACE((g_hInst, "Device registered to challenge"));
        DoTraceMessage(WSDSCDRV_TRC, L"Device registered to challenge");
    }

    return hr;
}
```

 

 




