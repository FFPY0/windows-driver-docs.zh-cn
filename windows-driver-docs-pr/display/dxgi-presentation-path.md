---
title: DXGI 呈现路径
description: DXGI 呈现路径
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efa07f12beaa589c2c5aa43a25eb8fd6ae92708f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809073"
---
# <a name="dxgi-presentation-path"></a>DXGI 呈现路径


DXGI 为应用程序提供了 "只工作" 的演示方法。 例如，应用程序无需执行任何特殊操作即可在窗口模式和全屏模式间切换。 此演示方法之所以可行，是因为 DXGI 和用户模式显示驱动程序协同工作以跨多个样本抗锯齿组合来保留演示 (MSAA) 、监视旋转、后端和前端缓冲区差异的大小和格式，以及全屏与开窗模式。 DXGI 的另一个优点是，它允许显示适配器限制扫描 MSAA 和旋转曲面的功能，因为 DXGI 提供 "无状态" DDI。 在无状态 DDI 中，适配器的驱动程序无需跨 DDI 调用记录数据。

显示的基本任务是将数据从呈现的后台缓冲区移到主要表面进行查看。 此任务在以下各节所述的不同情况下执行。

### <a name="span-idwindowed_mode_with_dwm_onspanspan-idwindowed_mode_with_dwm_onspanwindowed-mode-with-dwm-on"></a><span id="windowed_mode_with_dwm_on"></span><span id="WINDOWED_MODE_WITH_DWM_ON"></span>具有 DWM 的窗口模式

在带有桌面 Windows 管理器的窗口模式下 (DWM) 的情况下，DXGI 与 DWM 通信，并打开一个共享资源视图，该共享资源是 DXGI 制造者的呈现目标和 DWM 纹理。 除应用程序创建的任何后台缓冲区外，还存在此共享资源。 DXGI 调用驱动程序的 [**BltDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 函数，以将数据从任何后台缓冲区移动到共享表面。 此操作可能需要拉伸、颜色转换和 MSAA 解析。 但是，此操作永远不需要源和目标子矩形。 事实上，无法在对 *BltDXGI* 的调用中表达这些子矩形。 此位块传输 (bitblt) 始终在 *pBltData* 参数指向的 [**DXGI \_ DDI \_ ARG \_ BLT**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_blt)结构的 **Flags** 成员中设置了 **显示** 标志。 设置 **当前** 标志指示驱动程序应以原子方式执行操作。 该驱动程序以原子方式执行 bitblt 操作，以最大程度地减少在 DWM 读取用于撰写的共享资源时的撕裂情况。

### <a name="span-idwindowed_mode_with_dwm_offspanspan-idwindowed_mode_with_dwm_offspanwindowed-mode-with-dwm-off"></a><span id="windowed_mode_with_dwm_off"></span><span id="WINDOWED_MODE_WITH_DWM_OFF"></span>具有 DWM 关闭的窗口模式

在具有 DWM 关闭大小写功能的开窗模式下，DXGI 会调用驱动程序的 [**PresentDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数，并在 *pPresentData* 参数指向的 [**DXGI \_ DDI \_ ARG \_ 现有**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present)结构的 **Flags** 成员中设置 **Blt** 标志。 在此 *PresentDXGI* 调用中，dxgi 可以在 **hSurfaceToPresent** 和 SrcSubResourceIndex 成员的 **SrcSubResourceIndex** 成员中指定任何应用程序创建的后台 \_ 缓冲区 \_ \_ 。 没有其他共享图面。

### <a name="span-idfull_screen_modespanspan-idfull_screen_modespanfull-screen-mode"></a><span id="full_screen_mode"></span><span id="FULL_SCREEN_MODE"></span>全屏模式

全屏大小写比打开或关闭 DWM 的窗口模式更为复杂。

当 DXGI 转换为全屏模式时，它会尝试利用翻转操作来减少带宽并获得垂直同步同步。 以下情况可能会阻止使用翻转操作：

-   应用程序不会以与主表面匹配的方式重新分配其后台缓冲区。

-   驱动程序指定它不会扫描后台缓冲区 (例如，因为后台缓冲区是旋转的，或者是 MSAA) 。

-   应用程序指定它不能接受 Direct3D 运行时丢弃后台缓冲区的内容，并且只请求一个缓冲区 (链中) 总数。  (在这种情况下，DXGI 分配一个后表面和一个主表面;但是，DXGI 使用驱动程序的 *PresentDXGI* 函数，并设置 **Blt** 标志。 ) 

如果出现上述某个情况，则会阻止执行翻转操作，并且对驱动程序的 [**PresentDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数的调用 **Blt** 标志集也不是合适的 (因为后台缓冲区与前台缓冲区完全相同) *proxy surface* 此代理图面与前台缓冲区匹配。 因此，可以在代理表面和前台缓冲区之间进行切换。 如果存在代理表面，DXGI 将使用驱动程序的 [**BltDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 函数，并清除 (0) 的 **现有** 标志，将应用程序的后台缓冲区复制到代理图面。 在此 *BltDXGI* 调用中，DXGI 可能会请求转换、拉伸和解析。 然后，DXGI 会调用驱动程序的 *PresentDXGI* 函数，并在 [**DXGI \_ DDI \_ ARG \_ 现有**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present)结构的 **Flags** 成员中设置 **翻转** 标志，以将代理图面位移动到 scan out。

为了通知用户模式显示驱动程序，驱动程序可以退出扫描，驱动程序将接收对可选的和非可选的扫描表面类的资源创建调用。 可选的扫描表面由 DXGI \_ DDI \_ 主要 \_ 可选标志指定。 非可选的扫描表面未 \_ 设置 DXGI DDI \_ 主要 \_ 可选标志。 有关这些类型的资源创建调用的详细信息，请参阅 [在资源创建时传递 DXGI 信息](passing-dxgi-information-at-resource-creation-time.md)。

DXGI 设置 DXGI \_ DDI \_ 主要 \_ 可选标志，用于创建所有后台缓冲区图面 (即) 的可选表面，并不设置任何前台缓冲或代理图面的标志 (即，非可选曲面) 。

如果为 \_ \_ \_ 后台缓冲区设置了 dxgi ddi primary OPTIONAL，则驱动程序可以设置 dxgi \_ ddi \_ 主 \_ 驱动程序 \_ 标志 \_ NO \_ SCANOUT 标志。 有关设置此标志的详细信息，请参阅 [在资源创建时传递 DXGI 信息](passing-dxgi-information-at-resource-creation-time.md)。 如果驱动程序 \_ 为可选缓冲区设置了 DXGI DDI \_ 主 \_ 驱动程序 \_ 标志 \_ no \_ SCANOUT，则除了之外，还将导致 DXGI 使用 **Blt** 标志（而不是设置 **翻转** 标志）调用驱动程序的 [**PresentDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数。

如果 \_ \_ \_ 没有为前台缓冲区或代理图面设置 DXGI DDI PRIMARY OPTIONAL，则驱动程序仍可以通过使资源创建调用失败并出现错误代码 DXGI ddi ERR 来退出扫描， \_ \_ \_ 并设置 DXGI \_ ddi \_ 主 \_ 驱动程序 \_ 标志 \_ NO \_ SCANOUT。

**注意**   无法在未设置 DXGI \_ DDI \_ 主 \_ 驱动程序标志的情况下创建调用 \_ ，因此 \_ 不 \_ 会为真正的故障情况（如内存不足）保留 SCANOUT。

 

当 DXGI 试图为 MSAA 或旋转后的缓冲区创建全屏表示链时，可以利用此选择退出方法。 如果驱动程序将不会扫描其中的任何一种或两种类型，则驱动程序将选择退出。然后，DXGI 将尝试创建非旋转图面、非 MSAA 面，或同时创建两者，直到驱动程序接受资源创建。 因此，DXGI 会逐渐恢复，直到非可选表面与前台缓冲区格式完全匹配、采样计数、旋转和大小。

如果驱动程序选择了任何非可选表面，则 DXGI 仍必须能够将 bits 从后台缓冲区移到主要表面。 因此，如果驱动程序退出用于 MSAA 和旋转的扫描，驱动程序会在 DXGI 调用驱动程序的 [**BltDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 函数时，将其弹出或同时进行解析。 当驱动程序退出时，DXGI 将创建一个代理接口，并调用 **BltDXGI** 将数据从后台缓冲区移到该代理表面。 由于代理与前台缓冲区完全匹配，因此，驱动程序不应选择退出此代理图面。

当应用程序在转换为全屏模式或从全屏模式转换后不重新创建其表面时，会出现以下异常情况：

-   如果应用程序在进入全屏模式时不会重新创建其表面，则 DXGI 会确定后台缓冲区与前台缓冲区不匹配，即使它们确实与格式、大小、旋转和采样计数匹配。 此确定的原因是，操作系统需要将后台缓冲区标记为在创建这些缓冲区时扫描到特定监视器。 仍无法将开窗后台缓冲区明确地分配给特定监视器，因为在输入全屏时，将动态选择该监视器。 因此，DXGI 不得将这些后台缓冲区发送到驱动程序，以便 (通过翻转操作) 进行扫描。 此类型的应用程序通常强制 DXGI 创建代理图面。

-   如果应用程序在返回到窗口模式时不重新创建其后台缓冲区，则 DXGI 可能会调用驱动程序的 [**BltDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 或 [**PresentDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (，其中 **Blt** 设置) 在之前为翻转操作创建的图面上执行 bitblt。 这种情况不应是一个问题，但此处所述的是完整性。 请注意，当应用程序转换为窗口模式时，DXGI 始终会销毁代理图面。

另外，请注意，应用程序可以在应用程序处于全屏模式时，动态调整其后台缓冲区的大小。 此操作会使前面的情况中描述的逻辑再次出现。 因此，可能会创建和销毁代理表面，即使应用程序仍处于全屏模式下，也可能在一段时间内不需要选择退出。 应用程序还可以动态地将其输出传输到另一个监视器，而无需离开全屏模式。 因此，应用程序会将切换回 bitblt 模式，因为应用程序的后台缓冲区已标记为不同的监视器。

最后，应注意，如果驱动程序未选择退出 MSAA 扫描，则返回有关 MSAA 缓冲区的情况。在这种情况下，驱动程序将会自行扫描 MSAA。 因此，DXGI 通过执行翻转操作来交换 MSAA 后台缓冲区和 MSAA 前台缓冲区，并通过与数字到模拟转换器 (DAC) 的等效项来执行解决操作。 在这种情况下，应用程序可以在全屏模式下动态调整其后台缓冲区的大小，这会强制 DXGI 切换到调用驱动程序的 [**BltDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 函数。 由于后台缓冲区和前台缓冲区的 MSAA 特征仍匹配，因此 DXGI 将指定该驱动程序执行不能解析的、可能进行颜色转换的 stretch bitblt。 然后，该驱动程序应复制但不解析，multisamples 到前台缓冲区（如果驱动程序选择扫描传出 MSAA，则这是必需的）。

 

