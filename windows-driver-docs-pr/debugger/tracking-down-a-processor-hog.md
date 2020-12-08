---
title: 跟踪占用大量处理器资源的进程
description: 跟踪占用大量处理器资源的进程
keywords:
- 处理器占用
- 占用处理器
- 从而使应用程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08eb5f04a290e0776aead8bf891030c437625eaf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803279"
---
# <a name="tracking-down-a-processor-hog"></a>跟踪占用大量处理器资源的进程


## <span id="ddk_tracking_down_a_processor_hog_dbg"></span><span id="DDK_TRACKING_DOWN_A_PROCESSOR_HOG_DBG"></span>


如果一个应用程序正在使用 ( "占用" ) 处理器的所有关注项，则其他进程将结束 "从而使"，无法运行。

使用以下过程来更正此类错误。

**调试使用所有 CPU 周期的应用程序**

1.  **确定导致此问题的应用程序：** 使用 " **任务管理器** " 或 " **Perfmon** " 查找正在使用99% 或100% 的处理器周期的进程。 这也可能会告诉您问题的线索。

2.  将 WinDbg、KD 或 CDB 附加到此进程。

3.  **确定导致此问题的线程：** 进入有问题的应用程序。 使用 [**！失控 3**](-runaway.md) 扩展来获取 "快照"，其中的所有 CPU 时间都在此。 使用 [**g (中转)**](g--go-.md) 并等待几秒钟。 然后，中断并再次使用 **！失控 3** 。

    ```dbgcmd
    0:002> !runaway 3
     User Mode Time
     Thread    Time
     4e0        0:12:16.0312
     268        0:00:00.0000
     22c        0:00:00.0000
     Kernel Mode Time
     Thread    Time
     4e0        0:00:05.0312
     268        0:00:00.0000
     22c        0:00:00.0000

    0:002> g

    0:001> !runaway 3
     User Mode Time
     Thread    Time
     4e0        0:12:37.0609
     3d4        0:00:00.0000
     22c        0:00:00.0000
     Kernel Mode Time
     Thread    Time
     4e0        0:00:07.0421
     3d4        0:00:00.0000
     22c        0:00:00.0000
    ```

    比较两组数字，并查找其用户模式时间或内核模式时间增加最多的线程。 由于 **！失控** 按降序排列 CPU 时间，因此，有问题的线程通常是列表顶部的那个线程。 在这种情况下，线程0x4E0 导致了问题。

4.  使用 [**~ (线程状态)**](---thread-status-.md) 和 [**~ s (设置当前线程)**](-s--set-current-thread-.md) 命令，使其成为当前线程：
    ```dbgcmd
    0:001> ~
       0  Id: 3f4.3d4 Suspend: 1 Teb: 7ffde000 Unfrozen
    .  1  Id: 3f4.22c Suspend: 1 Teb: 7ffdd000 Unfrozen
     2  Id: 3f4.4e0 Suspend: 1 Teb: 7ffdc000 Unfrozen

    0:001> ~2s
    ```

5.  使用 [**kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 以获取此线程的堆栈跟踪：
    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffc74  77f6c600  000000c8.00000000 77fa5ad0 BuggyProgram!CreateMsgFile+0x1b
    0b4ffce4  01836060  0184f440 00000001 0b4ffe20 BuggyProgram!OpenDestFileStream+0xb3
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76
    ```

6.  在当前正在运行的函数的返回地址上设置断点。 在这种情况下，返回地址显示为0x77F6C600 的第一行。 返回地址等效于第二行中显示的函数偏移量 (**BuggyProgram！OpenDestFileStream + 0xB3**) 。 如果没有可用于应用程序的符号，则函数名称可能不会出现。 使用符号或十六进制地址，在达到此返回地址之前，使用 [**g (中转)**](g--go-.md) 命令执行：
    ```dbgcmd
    0:002> g BuggyProgram!OpenDestFileStream+0xb3
    ```

7.  如果命中此断点，请重复该过程。 例如，假设已命中此断点。 应采取以下步骤：

    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffce4  01836060  0184f440 00000001 0b4ffe20 BuggyProgram!OpenDestFileStream+0xb3
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76

    0:002> g BuggyProgram!SaveMsgToDestFolder+0xb3
    ```

    如果遇到这种情况，请继续：

    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76

    0:002> g BuggyProgram!DispatchToConn+0xa4
    ```

8.  最后，你会发现未命中的断点。 在这种情况下，您应假设最后一个 " **g** " 命令设置为正在运行的，并且不会中断。 这意味着 **SaveMsgToDestFolder ( # B1** 函数永远不会返回。

9.  再次中断线程并在 BuggyProgram 上设置断点 **！SaveMsgToDestFolder + 0xB3** 与 [**Bp (设置断点)**](bp--bu--bm--set-breakpoint-.md) 命令。 然后重复使用 **g** 命令。 如果此断点立即出现，无论你执行了多少次目标，都很可能已确定有问题的函数：
    ```dbgcmd
    0:002> bp BuggyProgram!SaveMsgToDestFolder+0xb3

    0:002> g 

    0:002> g 
    ```

10. 使用 [**p (Step)**](p--step-.md) 命令继续执行函数，直到确定循环指令序列的位置。 然后，你可以分析应用程序的源代码，以确定旋转线程的原因。 原因通常是在一 **段** 时间内、 **执行** 时间、 **转** 到或 **for** 循环的逻辑中出现问题。

 

 





