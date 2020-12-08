---
title: 实现音频处理对象
description: 本主题介绍如何 (APO) 实现音频处理对象。 有关的一般信息，请参阅音频处理对象体系结构。
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: fa4a68ae94b81152e64e54383ecaacd8f88c3bfa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784761"
---
# <a name="implementing-audio-processing-objects"></a>实现音频处理对象

本主题介绍如何 (APO) 实现音频处理对象。 有关的一般信息，请参阅 [音频处理对象体系结构](audio-processing-object-architecture.md)。

## <a name="implementing-custom-apos"></a>实现自定义

自定义的是作为进程内 COM 对象实现的，因此它们在用户模式下运行，并打包在动态链接库中 (DLL) 。 有三种类型的 APO，它们是在信号处理图形中插入的位置。

-  (SFX) 的流效果
- MFX)  (模式效果
- EFX)  (的端点效果

每个逻辑设备可以与每个类型的一个 APO 关联。 有关模式和效果的详细信息，请参阅 [音频信号处理模式](audio-signal-processing-modes.md)。

可以通过将自定义类基于在 Baseaudioprocessingobject 文件中声明的 CBaseAudioProcessingObject 基类来实现 APO。 此方法涉及到在 CBaseAudioProcessingObject 基类中添加新功能，以创建自定义的 APO。 CBaseAudioProcessingObject 基类实现 APO 所需的大部分功能。 它为所需的三个接口中的大多数方法提供默认实现。 主要的例外是 [**IAudioProcessingObjectRT：： APOProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess) 方法。

执行以下步骤以实现自定义的。

1. 创建自定义 APO com 对象，以提供所需的音频处理。
2. （可选）创建一个用户界面，用于配置自定义的用户使用。
3. 创建一个 INF 文件来安装和注册 "用户" 和 "自定义" 用户界面。

## <a name="design-considerations-for-custom-apo-development"></a>自定义 APO 开发的设计注意事项

所有自定义项必须具有以下常规特性：

- APO 必须有一个输入和一个输出连接。 这些连接是音频缓冲区，可以有多个通道。
- APO 只能修改通过其 [**IAudioProcessingObjectRT：： APOProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess) 例程传递给它的音频数据。 APO 无法更改基础逻辑设备的设置，包括其 KS 拓扑。
- 除 IUnknown 外，其中必须公开以下接口：

  - [IAudioProcessingObject](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)。 处理安装任务（例如初始化和格式协商）的接口。

  - [IAudioProcessingObjectConfiguration](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)。 配置接口。

  - [IAudioProcessingObjectRT](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)。 处理音频处理的实时接口。 可以从实时处理线程调用它。

  - [IAudioSystemEffects](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)。 使音频引擎将 DLL 识别为系统效果 APO 的接口。

- 所有的都必须具有实时系统兼容性。 这意味着：

  - 作为实时接口成员的所有方法必须作为非阻止成员实现。 它们不能阻止、使用分页的内存或调用任何阻止的系统例程。

  - APO 处理的所有缓冲区都必须为不可分页。 进程路径中的所有代码和数据都必须是不可分页。

  - 不应将明显延迟引入音频处理链。

- 自定义的不能公开 IAudioProcessingObjectVBR 接口。

>[!NOTE]
>有关所需接口的详细信息，请参阅 Windows 工具包内部版本号中的 Audioenginebaseapo 和 Audioenginebaseapo 文件， \\ &lt; &gt; \\ 其中包括 \\ um 文件夹。

## <a name="using-sample-code-to-accelerate-the-development-process"></a>使用示例代码加速开发过程

使用 SYSVAD Swap APO 代码示例作为模板，可以加快自定义 APO 开发过程。 交换示例是为说明音频处理对象的某些功能而开发的示例。 Swap APO 示例将左声道交换为右通道，同时实现 SFX 和 MFX 效果。 可以使用 "属性" 对话框来启用和禁用通道交换音频效果。

[Windows 驱动程序示例 GitHub](https://github.com/Microsoft/Windows-driver-samples)上提供了 SYSVAD 音频示例。

可在此处浏览 Sysvad 音频示例：

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

### <a name="download-and-extract-the-sysvad-audio-sample-from-github"></a>从 GitHub 下载并提取 Sysvad 音频示例

按照以下步骤下载并打开 "SYSVAD" 示例。

a. 您可以使用 GitHub 工具来处理示例。 你还可以将通用驱动程序示例下载到一个 zip 文件中。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b. 将 master.zip 文件下载到本地硬盘驱动器。

c. Selecct 并按住 (或右键单击) *Windows-driver-samples-master.zip*，然后选择 " **全部提取**"。 指定一个新文件夹，或浏览到将存储所提取文件的现有文件夹。 例如，可以指定 *C： \\ DriverSamples \\* 作为要将文件提取到的新文件夹。

d. 提取文件后，导航到以下子文件夹： *C： \\ DriverSamples \\ 音频 \\ Sysvad*

### <a name="open-the-driver-solution-in-visual-studio"></a>在 Visual Studio 中打开驱动程序解决方案

在 Microsoft Visual Studio 中，选择 " **文件**" " &gt; **打开** &gt; **项目/解决方案 ...** "，然后导航到包含所提取文件的文件夹 (例如， *C： \\ DriverSamples \\ Audio \\ Sysvad*) 。 双击 " *Sysvad* " 解决方案文件以将其打开。

在 Visual Studio 中找到解决方案资源管理器。  (如果尚未打开，则从 "**视图**" 菜单中选择 "**解决方案资源管理器**"。 ) 解决方案资源管理器中，你可以看到一个包含六个项目的解决方案。

### <a name="swapapo-example-code"></a>SwapAPO 示例代码

SYSVAD 示例中有五个项目，其中一项是 APO 开发人员的主要兴趣。

|**Project**|**说明**|
|----|----|
|SwapAPO|示例 APO 的示例代码|

下面总结了 Sysvad 示例中的其他项目。

|**Project**|**说明**|
|----|----|
| PhoneAudioSample       | 移动音频驱动程序的示例代码。     |
| TabletAudioSample      | 备用音频驱动程序的示例代码。 |
| KeywordDetectorAdapter | 关键字检测器适配器的示例代码 |
| EndpointsCommon        | 常见终结点的示例代码。          |

SwapAPO 示例的主头文件为 SwapAPO。 下面总结了其他主要代码元素。

|**File**|**说明**|
|----|----|
| 交换 .cpp             | 包含交换 APO 的实现的 c + + 代码。        |
| SwapAPOMFX .cpp       | CSwapAPOMFX 的实现                                     |
| SwapAPOSFX .cpp       | CSwapAPOSFX 的实现                                     |
| SwapAPODll .cpp       | DLL 导出的实现。                                    |
| SwapAPODll .idl       | DLL 的 COM 接口和组件类的定义。           |
| SwapAPOInterface .idl | Swap APO 功能的接口和类型定义。    |
| swapapodll       | COM 导出定义                                           |

## <a name="implementing-the-com-object-audio-processing-code"></a>实现 COM 对象音频处理代码

可以通过将自定义类基于在 Baseaudioprocessingobject 文件中声明的 **CBaseAudioProcessingObject** 基类来包装系统提供的 APO。 此方法涉及到在 **CBaseAudioProcessingObject** 基类中引入新功能，以创建自定义的 APO。 **CBaseAudioProcessingObject** 基类实现 APO 所需的大部分功能。 它为所需的三个接口中的大多数方法提供默认实现。 主要的例外是 [**IAudioProcessingObjectRT：： APOProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess) 方法。

通过使用 **CBaseAudioProcessingObject**，你可以更轻松地实现 APO。 如果 APO 没有特殊的格式要求并且操作所需的 float32 格式，则 **CBaseAudioProcessingObject** 中包含的接口方法的默认实现应足以满足需要。 给定默认实现，只能实现三个主要方法： [**IAudioProcessingObject：： IsInputFormatSupported**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)、 [**IAudioProcessingObjectRT：： APOProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)和 **ValidateAndCacheConnectionInfo**。

若要基于 **CBaseAudioProcessingObject** 类开发您的，请执行以下步骤：

1. 创建从 **CBaseAudioProcessingObject** 继承的类。

    下面的 c + + 代码示例演示如何创建从 **CBaseAudioProcessingObject** 继承的类。 对于此概念的实际实现，请按照 **音频处理对象驱动程序示例** 部分中的说明操作，转到交换示例，然后引用 *Swapapo* 文件。

    ```cpp
    // Custom APO class - LFX
    Class MyCustomAPOLFX: public CBaseAudioProcessingObject
    {
     public:
    //Code for custom class goes here
    ...
    };
    ```

    **注意**   由于 SFX APO 执行的信号处理不同于 MFX 或 EFX APO 执行的信号处理，因此必须为每个创建单独的类。

2. 实现以下三种方法：

    - [**IAudioProcessingObject：： IsInputFormatSupported**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)。 此方法处理与音频引擎的格式协商。

    - [**IAudioProcessingObjectRT：： APOProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess)。 此方法使用自定义算法来执行信号处理。

    - **ValidateAndCacheConnectionInfo**。 此方法分配内存以存储格式详细信息，例如，通道计数、采样率、样本深度和通道掩码。

下面的 c + + 代码示例演示了在步骤1中创建的示例类的 [**APOProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess) 方法的实现。 对于此概念的实际实现，请按照 **音频处理对象驱动程序示例** 部分中的说明操作，转到交换示例，然后引用 *Swapapolfx* 文件。

```cpp
// Custom implementation of APOProcess method
STDMETHODIMP_ (Void) MyCustomAPOLFX::APOProcess (...)
{
// Code for method goes here. This code is the algorithm that actually
// processes the digital audio signal.
...
}
```

下面的代码示例演示 **ValidateAndCacheConnectionInfo** 方法的实现。 若要实现此方法的实际实现，请按照 **音频处理对象驱动程序示例** 部分中的说明操作，转到交换示例，然后引用 *Swapapogfx* 文件。

```cpp
// Custom implementation of the ValidateAndCacheConnectionInfo method.
HRESULT CSwapAPOGFX::ValidateAndCacheConnectionInfo( ... )
{
// Code for method goes here.
// The code should validate the input/output format pair.
...
}
```

**注意**  类继承自 **CBaseAudioProcessingObject** 的剩余接口和方法在 Audioenginebaseapo 文件中进行了详细介绍。

## <a name="replacing-system-supplied-apos"></a>替换系统提供的

在实现 APO 接口时，有两种方法：可以编写自己的实现，也可以调入收件箱。

此伪代码演示包装系统 APO。

```cpp
CMyWrapperAPO::CMyWrapperAPO {
    CoCreateInstance(CLSID_InboxAPO, m_inbox);
}

CMyWrapperAPO::IsInputFormatSupported {
    Return m_inbox->IsInputFormatSupported(…);
}
```

此伪代码说明如何创建自己的自定义 APO。

```cpp
CMyFromScratchAPO::IsInputFormatSupported {
    my custom logic
}
```

当你开发的是替换系统提供的程序时，你必须在以下列表中使用相同的名称，以获取接口和方法。 某些接口除了列出所需的方法之外，还具有更多方法。 若要确定是要实现所有方法还是只实现所需的方法，请参阅这些接口的参考页。

其余的实现步骤与自定义 APO 相同。

为 COM 组件实现以下接口和方法：

- [IAudioProcessingObject](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobject)。 此接口所需的方法为： [**Initialize**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-initialize) 和 [**IsInputFormatSupported。**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)
- [IAudioProcessingObjectConfiguration](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectconfiguration)。 此接口的必需方法为： [**LockForProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess) 和 [**UnlockForProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-unlockforprocess)
- [IAudioProcessingObjectRT](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudioprocessingobjectrt)。 此接口所需的方法是 [**APOProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectrt-apoprocess) 的，它是实现 DSP 算法的方法。
- [IAudioSystemEffects](/windows/win32/api/audioenginebaseapo/nn-audioenginebaseapo-iaudiosystemeffects)。 此接口使音频引擎可以将 DLL 识别为 APO。

## <a name="working-with-visual-studio-and-apos"></a>使用 Visual Studio 和

在 Visual Studio 中使用时，请为每个 APO 项目执行这些任务。

### <a name="link-to-the-crt"></a>链接到 CRT

面向 Windows 10 的驱动程序应动态地链接到通用 CRT。

如果需要支持 Windows 8，1，请通过在 C/c + + 中设置项目属性，代码生成启用静态链接。 对于发布版本，请将 "运行时库" 设置为 */mt* ，或将 */MTd* 设置为用于调试版本。 进行此更改的原因是，对于驱动程序，很难再分发 MSVCRT.LIB &lt; 的 &gt; 二进制文件。 解决方案是以静态方式链接 libcmt.dll。 有关详细信息，请参阅 [/md、/mt、/ld (使用 Run-Time 库) ](/cpp/build/reference/md-mt-ld-use-run-time-library) 。

### <a name="disable-use-of-an-embedded-manifest"></a>禁止使用嵌入清单

通过设置 APO 项目的项目属性，禁止使用嵌入清单。 选择 " **清单工具**"、" **输入和输出**"。 然后将 "嵌入清单" 从默认的 *"是* " 更改为 " *否*"。 如果有嵌入的清单，则会触发在受保护环境内禁止使用某些 Api。 这意味着你的 APO 将在 DisableProtectedAudioDG = 1 的情况下运行，但在删除此测试密钥时，你的 APO 将无法加载，即使已对其进行了 WHQL 签名也是如此。

## <a name="packaging-your-apo-with-a-driver"></a>将 APO 与驱动程序一起打包

当你开发自己的音频驱动程序并包装或替换系统提供的时，你必须提供用于安装驱动程序的驱动程序包。 对于 Windows 10，请参阅适用 [于音频的通用 Windows 驱动程序](audio-universal-drivers.md)。 音频相关的驱动程序包应遵循详细说明的策略和打包模型。  

自定义 APO 打包为 DLL，并且任何配置 UI 打包为单独的 UWP 或桌面桥应用。 APO 设备 INF 将 Dll 复制到关联的 INF CopyFile 指令中指定的系统文件夹。 包含 AddReg 的 DLL 必须在 INF 文件中包含一个部分，自行注册。

以下段落和 INF 文件片段显示了使用标准 INF 文件复制和注册的必要修改。

Sysvad 示例附带的 inf 文件演示了如何注册 SwapApo.dll。

## <a name="registering-apos-for-processing-modes-and-effects-in-the-inf-file"></a>在 INF 文件中注册用于处理模式和效果的

可以使用某些允许的注册表项组合来注册特定模式的。 若要详细了解哪些效果可用以及有关中的常规信息，请参阅 [音频处理对象体系结构](audio-processing-object-architecture.md)。

请参阅以下参考主题，了解有关每个 APO INF 文件设置的信息。

[PKEY \_ FX \_ StreamEffectClsid](./pkey-fx-streameffectclsid.md)

[PKEY \_ FX \_ ModeEffectClsid](./pkey-fx-modeeffectclsid.md)

[PKEY \_ FX \_ EndpointEffectClsid](./pkey-fx-endpointeffectclsid.md)

[\_ \_ \_ 支持 \_ \_ 流式处理的 PKEY SFX ProcessingModes](./pkey-sfx-processingmodes-supported-for-streaming.md)

[PKEY \_ MFX \_ ProcessingModes \_ 支持 \_ \_ 流式处理](./pkey-mfx-processingmodes-supported-for-streaming.md)

[\_ \_ \_ 支持 \_ \_ 流式处理的 PKEY EFX ProcessingModes](./pkey-efx-processingmodes-supported-for-streaming.md)

以下 INF 文件示例说明了如何在特定模式下为) 注册音频处理对象 (。 它们说明了此列表中可用的可能组合。

- PKEY \_ FX \_ STREAMEFFECTCLSID with PKEY \_ SFX \_ ProcessingModes \_ 支持 \_ \_ 流式处理
- PKEY \_ FX \_ MODEEFFECTCLSID with PKEY \_ MFX \_ ProcessingModes \_ Suppoted \_ For \_ 流式处理
- PKEY \_ FX \_ ModeEffectClsid （无 PKEY \_ MFX \_ ProcessingModes Suppoted） \_ \_ 进行 \_ 流式处理
- PKEY \_ FX \_ EndpointEffectClsid，不 \_ \_ \_ 支持 \_ \_ 流式处理的 PKEY EFX ProcessingModes

这两个示例中未显示一种附加的有效组合。

- \_ \_ \_ \_ \_ 支持 \_ \_ 流式处理的 PKEY FX EndpointEffectClsid 与 PKEY EFX ProcessingModes

### <a name="sysvad-tablet-multi-mode-streaming-effect-apo-inf-sample"></a>SYSVAD Tablet 多模式流式处理效果 APO INF 示例

此示例演示如何使用 SYSVAD Tablet INF 文件中的 AddReg 条目注册多模式流式处理效果。

此示例代码来自 SYSVAD 音频示例，在 GitHub 上提供： <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad> 。

此示例演示了这种系统效果组合：

- PKEY \_ FX \_ STREAMEFFECTCLSID with PKEY \_ SFX \_ ProcessingModes \_ 支持 \_ \_ 流式处理
- PKEY \_ FX \_ MODEEFFECTCLSID with PKEY \_ MFX \_ ProcessingModes \_ Suppoted \_ For \_ 流式处理

```inf
[SWAPAPO.I.Association0.AddReg]
; Instruct audio endpoint builder to set CLSID for property page provider into the
; endpoint property store
HKR,EP\0,%PKEY_AudioEndpoint_ControlPanelPageProvider%,,%AUDIOENDPOINT_EXT_UI_CLSID%

; Instruct audio endpoint builder to set the CLSIDs for stream, mode, and endpoint APOs
; into the effects property store
HKR,FX\0,%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,FX\0,%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,FX\0,%PKEY_FX_UserInterfaceClsid%,,%FX_UI_CLSID%

; Driver developer would replace the list of supported processing modes here
; Concatenate GUIDs for DEFAULT, MEDIA, MOVIE
HKR,FX\0,%PKEY_SFX_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%

; Concatenate GUIDs for DEFAULT, MEDIA, MOVIE
HKR,FX\0,%PKEY_MFX_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%

;HKR,FX\0,%PKEY_EFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
```

请注意，在示例 INF 文件中，EFX \_ 流式处理属性被注释掉，因为音频处理已转换为该层之上的内核模式，因此不需要使用流式处理属性，因此不会使用此属性。 为发现目的指定 PKEY FX EndpointEffectClsid 是有效的 \_ \_ ，但为 \_ \_ \_ \_ \_ 流式处理指定 PKEY EFX ProcessingModes 会是错误的。 这是因为模式混合/t 会在堆栈中较低，因此无法插入终结点 APO。

### <a name="componentized-apo-installation"></a>组件化 APO 安装

从 Windows 10 开始，版本1809，使用音频引擎 APO 注册使用组件化音频驱动程序模型。 使用音频组件化创建更平稳、更可靠的安装体验，并更好地支持组件服务。 有关详细信息，请参阅 [创建组件化音频驱动程序安装](./audio-universal-drivers.md#creating-a-componentized-audio-driver-installation)。

下面的示例代码从公共 ComponentizedAudioSampleExtension 和 ComponentizedApoSample 提取。 请参阅 GitHub 上提供的 SYSVAD 音频示例，网址为： <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad> 。

使用新创建的 APO 设备，将 APO 与音频引擎注册。 要使音频引擎能够使用新的 APO 设备，它必须是音频设备的 PNP 子元素、音频终结点的同级。 新的组件化 APO 设计不允许将 APO 在多个不同的驱动程序上全局注册和使用。 每个驱动程序都必须注册其自己的 APO。

APO 的安装分为两部分。 首先，驱动程序扩展 INF 会将 APO 设备添加到系统：

```inf
[DeviceExtension_Install.Devices]
AddDevice = SwapApo,,Apo_AddDevice

[Apo_AddDevice]
HardwareIds = APO\VEN_SMPL&CID_APO
Description = "Audio Proxy APO Sample"
Capabilities = 0x00000008 ; SWDeviceCapabilitiesDriverRequired
```

此 APO 设备在 SYSVAD 示例中触发了 APO INF 的第二部分，这是在 ComponentizedApoSample 中完成的。 此 INF 文件专用于 APO 设备。 它将设备类指定为 AudioProcessingObject，并添加用于 CLSID 注册的所有 APO 属性，并向音频引擎注册。

>[!NOTE]
> 在大多数情况下，通过使用 HKR 注册表项，显示的 INF 文件示例支持驱动程序包隔离。 前面的示例使用 HKCR 存储持久值。 例外情况是， (COM) 对象的组件对象模型的注册，可以在 HKCR 下编写一个密钥。
有关详细信息，请参阅[使用通用 INF 文件](../install/using-a-universal-inf-file.md)。

```inf
[Version]
Signature   = "$WINDOWS NT$"
Class       = AudioProcessingObject
ClassGuid   = {5989fce8-9cd0-467d-8a6a-5419e31529d4}

[ApoComponents.NT$ARCH$]
%Apo.ComponentDesc% = ApoComponent_Install,APO\VEN_SMPL&CID_APO

[Apo_AddReg]
; CLSID registration
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%,,,%SFX_FriendlyName%
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,,0x00020000,%%SystemRoot%%\System32\swapapo.dll
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,ThreadingModel,,"Both"
…
;Audio engine registration
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"FriendlyName",,%SFX_FriendlyName%
...
```

当此 INF 安装组件化 APO 时，桌面系统 "音频处理对象" 将显示在 Windows 设备管理器中。

### <a name="bluetooth-audio-sample-apo-inf-sample"></a>蓝牙音频示例 APO INF 示例

此示例演示了这种系统效果组合：

- PKEY \_ FX \_ STREAMEFFECTCLSID with PKEY \_ SFX \_ ProcessingModes \_ 支持 \_ \_ 流式处理

- PKEY \_ FX \_ MODEEFFECTCLSID with PKEY \_ MFX \_ ProcessingModes \_ Suppoted \_ For \_ 流式处理

此示例代码支持蓝牙免提和立体声设备。

```inf
; wdma_bt.inf – example usage
...
[BthA2DP]
Include=ks.inf, wdmaudio.inf, BtaMpm.inf
Needs=KS.Registration,WDMAUDIO.Registration,BtaMPM.CopyFilesOnly,mssysfx.CopyFilesAndRegister
...
[BTAudio.SysFx.Render]
HKR,"FX\\0",%PKEY_ItemNameDisplay%,,%FX_FriendlyName%
HKR,"FX\\0",%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,"FX\\0",%PKEY_FX_UiClsid%,,%FX_UI_CLSID%
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"FX\\0",%PKEY_SFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
HKR,"FX\\0",%PKEY_MFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
...
[Strings]
FX_UI_CLSID      = "{5860E1C5-F95C-4a7a-8EC8-8AEF24F379A1}"
FX_STREAM_CLSID  = "{62dc1a93-ae24-464c-a43e-452f824c4250}"
PKEY_FX_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},5"
PKEY_FX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},6"
PKEY_SFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},5"
PKEY_MFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},6"
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
```

### <a name="apo-inf-audio-sample"></a>APO INF 音频示例

此示例 INF 文件说明了以下系统效果组合：

- PKEY \_ FX \_ STREAMEFFECTCLSID with PKEY \_ SFX \_ ProcessingModes \_ 支持 \_ \_ 流式处理

- PKEY \_ FX \_ MODEEFFECTCLSID with PKEY \_ MFX \_ ProcessingModes \_ Suppoted \_ For \_ 流式处理

- PKEY \_ FX \_ EndpointEffectClsid，不 \_ \_ \_ 支持 \_ \_ 流式处理的 PKEY EFX ProcessingModes

```inf
[MyDevice.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%MyFilterName%,MyAudioInterface

[MyAudioInterface]
AddReg=MyAudioInterface.AddReg

[MyAudioInterface.AddReg]
;To register an APO for discovery, use the following property keys in the .inf (or at runtime when registering the KSCATEGORY_AUDIO device interface):
HKR,"FX\\0",%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_MODE_CLSID%

;To register an APO for streaming and discovery, add the following property keys as well (to the same section):
HKR,"FX\\0",%PKEY_SFX_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%

;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the modes:
HKR,"FX\\0",%PKEY_MFX_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

### <a name="define-a-custom-apo-and-clsid-apo-inf-sample"></a>定义自定义 APO 和 CLSID APO INF 示例

此示例演示如何为自定义 APO 定义自己的 CLSID。 此示例使用 MsApoFxProxy CLSID {889C03C8-ABAD-4004-BF0A-BC7BB825E166}。 共同 iopalisserverextension-此 GUID 在 MsApoFxProxy.dll 中实例化一个类，该类实现 IAudioProcessingObject 接口，并通过 KSPROPSETID AudioEffectsDiscovery 属性集查询基础驱动程序 \_ 。

此 INF 文件示例显示了 \[ BthHfAud \] 部分，该部分将 \[ \] 从 wdmaudio BthHfAud 中提取 MSAPOFXPROXY \[ \] ，然后将 AnlgACapture \_ FX \_ AddReg 注册为 MsApoFxProxy.dll 的知名 CLSID。

此 INF 文件示例还演示了此系统效果组合的用法：

- PKEY \_ FX \_ EndpointEffectClsid，不 \_ \_ \_ 支持 \_ \_ 流式处理的 PKEY EFX ProcessingModes

```inf
;wdma_bt.inf
[BthHfAud]
Include=ks.inf, wdmaudio.inf, BtaMpm.inf
Needs=KS.Registration, WDMAUDIO.Registration, BtaMPM.CopyFilesOnly, MsApoFxProxy.Registration
CopyFiles=BthHfAud.CopyList
AddReg=BthHfAud.AddReg

; Called by needs entry in oem inf
[BthHfAudOEM.CopyFiles]
CopyFiles=BthHfAud.CopyList

[BthHfAud.AnlgACapture.AddReg.Wave]
HKR,,CLSID,,%KSProxy.CLSID%
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_DISCOVER_EFFECTS_APO_CLSID%
#endif
```

### <a name="sample-apo-effect-registration"></a>示例 APO 效果注册

此示例显示 \[ \] Sysvad ComponentizedApoSample. inx 中的 Apo_AddReg 部分。 本部分将交换流 GUID 注册到 COM 并注册 Swap Stream APO 效果。 \[Apo_CopyFiles \] 节将 swapapo.dll 复制到 C： \\ Windows system32 中 \\ 。

```inf
; ComponentizedApoSample.inx

...

[ApoComponent_Install]
CopyFiles = Apo_CopyFiles
AddReg    = Apo_AddReg

[Apo_CopyFiles]
swapapo.dll

...

[Apo_AddReg]
; Swap Stream effect APO COM registration
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%,,,%SFX_FriendlyName%
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,,0x00020000,%13%\swapapo.dll
HKCR,CLSID\%SWAP_FX_STREAM_CLSID%\InProcServer32,ThreadingModel,,"Both"

'''
; Swap Stream effect APO registration
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"FriendlyName",,%SFX_FriendlyName%
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"Copyright",,%Copyright%
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MajorVersion",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MinorVersion",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"Flags",0x00010001,%APO_FLAG_DEFAULT%
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MinInputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MaxInputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MinOutputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MaxOutputConnections",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"MaxInstances",0x00010001,0xffffffff
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"NumAPOInterfaces",0x00010001,1
HKR,AudioEngine\AudioProcessingObjects\%SWAP_FX_STREAM_CLSID%,"APOInterface0",,"{FD7F2B29-24D0-4B5C-B177-592C39F9CA10}"
...

[Strings]
; Driver developers would replace these CLSIDs with those of their own APOs
SWAP_FX_STREAM_CLSID   = "{B48DEA3F-D962-425a-8D9A-9A5BB37A9904}"

...
```

## <a name="apo-registration"></a>APO 注册

APO 注册用于支持使用加权计算动态匹配终结点效果的进程。 加权计算使用以下属性存储区。 每个音频接口都有零个或多个 *终结点属性存储* ，并影响通过 .inf 或在运行时注册的 *属性存储* 。 最特定的终结点属性存储和最具体的影响属性存储具有最大权重，并使用。 所有其他属性存储将被忽略。

具体计算方式如下：

终结点属性存储权重

1. 具有特定 KSNODETYPE 的 FX
2. KSNODETYPE \_ ANY
3. 具有特定 KSNODETYPE 的 MSFX
4. MSFX with KSNODETYPE \_ ANY

效果属性存储权重

1. 具有特定 KSNODETYPE 的 EP
2. 具有 \_ KSNODETYPE 的 EP
3. 具有特定 KSNODETYPE 的 MSEP
4. MSEP with KSNODETYPE \_ ANY

数字必须从0开始，并按顺序递增： MSEP \\ 0、MSEP \\ 1、...、MSEP \\ n 如果 (例如) EP \\ 3 缺失，则 WINDOWS 将停止查找 ep \\ n，即使存在，也不会看到 ep \\ 4

"效果" 属性的 PKEY \_ FX \_ association (的值用于 \_ \_ 将终结点) 属性存储) 或 PKEY EP 关联 (与 KSPINDESCRIPTOR 进行比较。信号路径的硬件端的固定工厂的类别值（由内核流公开）。

只有第三方开发人员 (可以包装的 Microsoft 收件箱类驱动程序) 应使用 MSEP 和 MSFX;所有第三方驱动程序应使用 EP 和 FX。

### <a name="apo-node-type-compatibility"></a>APO 节点类型的兼容性

以下 INF 文件示例说明了如何将 PKEY \_ FX \_ 关联密钥设置为与 APO 关联的 GUID。

```inf
;; Property Keys
PKEY_FX_Association = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},0"
"
```

```inf
;; Key value pairs
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
```

由于音频适配器能够支持多个输入和输出，因此您必须显式指示与您的自定义 APO 兼容的内核流式处理 (KS) 节点类型。 在上述 INF 文件片段中，APO 显示为与 KS 节点类型% KSNODETYPE \_ ANY% 关联。 稍后在本 INF 文件中，KSNODETYPE \_ ANY 定义如下：

```inf
[Strings]
;; Define the strings used in MyINF.inf
...
KSNODETYPE_ANY      = "{00000000-0000-0000-0000-000000000000}"
KSNODETYPE_SPEAKER  = "{DFF21CE1-F70F-11D0-B917-00A0C9223196}"
...
```

对于 KSNODETYPE， **NULL** 值为 NULL \_ 表示此 APO 与任何类型的 KS 节点类型兼容。 例如，若要指示 APO 仅与 KSNODETYPE 发言人的 KS 节点类型兼容 \_ ，则 INF 文件会显示 ks 节点类型和 APO 关联，如下所示：

```inf
;; Key value pairs
...
HKR,"FX\\0",%PKEY_FX_Association%,,%KSNODETYPE_SPEAKER%
...
```

有关不同 KS 节点类型的 GUID 值的详细信息，请参阅 Ksmedia 头文件。

## <a name="troubleshooting-apo-load-failures"></a>APO 加载失败疑难解答

提供以下信息是为了帮助你了解如何监视监视失败的情况。 您可以使用此信息对无法合并到音频图形中的进行故障排除。

音频系统监视 APO 返回代码，以确定是否已将其中一种合并到图形中。 它通过跟踪任何指定方法返回的 HRESULT 值来监视返回代码。 系统为合并到图形中的每个 SFX、MFX 和 EFX APO 维护单独的失败计数值。

音频系统从以下四种方法监视返回的 HRESULT 值。

- CoCreateInstance

- IsInputFormatSupported

- IsOutputFormatSupported

- LockForProcess

每次返回失败代码时，APO 的失败计数值都将递增。 当 APO 返回的代码指示已成功将其合并到音频图形中时，失败计数将重置为零。 成功调用 [**LockForProcess**](/windows/win32/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobjectconfiguration-lockforprocess) 方法是一种很好的方法，指出已成功添加 APO。

特别是对于 [**CoCreateInstance**](/windows/win32/api/combaseapi/nf-combaseapi-cocreateinstance) ，返回的 HRESULT 代码可能表明失败的原因有很多。 这三个主要原因如下：

- 该图形正在运行受保护的内容，但 APO 未正确签名。

- APO 未注册。

- APO 已被重命名或篡改。

此外，如果 SFX、MFX 或 EFX APO 的失败计数值达到系统指定的限制，则会通过将 PKEY \_ 终结点 \_ 禁用 \_ SysFx 注册表项设置为 "1" 来禁用 "sfx"、"MFX" 和 "efx"。 系统指定的限制当前为值10。

## <a name="related-topics"></a>相关主题

[Windows 音频处理对象](windows-audio-processing-objects.md)

[Using a Universal INF File](../install/using-a-universal-inf-file.md)（使用通用 INF 文件）

[创建组件化音频驱动程序安装](./audio-universal-drivers.md#creating-a-componentized-audio-driver-installation)
