---
title: 有关 MB 微型端口驱动程序 IP 地址通知的指导原则
description: 有关 MB 微型端口驱动程序 IP 地址通知的指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fabb04c31727dfe6d88b18d39a6f2b0e2fbb6854
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840029"
---
# <a name="guidelines-for-mb-miniport-driver-ip-address-notifications"></a>有关 MB 微型端口驱动程序 IP 地址通知的指导原则


用于指定其 INF 文件中的 *EnableDhcp* 等于零的微型端口驱动程序可以使用内核模式下的 [ip 帮助](ip-helper.md) 程序和关联的 [功能](./ip-helper.md) 来创建、更改和删除 IP 地址：

若要在内核模式下使用 IP Helper 函数，微型端口驱动程序必须包含 Netioapi 头文件，并链接到 Netio。

当微型端口驱动程序指定 *EnableDhcp* 等于零时，需要执行以下操作来通知 MB 服务有关以下任何事件：

-   设置 MB 接口的 IP 地址

-   设置默认网关地址

-   更新 DNS 地址

使用 IP 帮助程序 API 设置的 IP 地址和默认网关将保留网络连接或断开连接事件，或同时保留两者。 因此，如果新的 IP 地址或默认网关的值不同于当前设置的值，微型端口驱动程序应该首先清除以前的值，然后再设置网络连接事件的新值。

**注意** 微型端口驱动程序可以从传递给微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的 [**NDIS \_ 微型端口 \_ INIT \_ PARAMETERS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构的 **NetLuid** 或 **IfIndex** 成员那里找到 MB 接口的 **LUID** 和 **索引**。

 

### <a name="resetting-the-ip-address-and-gateway-address"></a>正在重置 IP 地址和网关地址

对 TCP/IP 堆栈进行的某些更改（如加载必需筛选器驱动程序）可以删除 IP helper 函数设置的 IP 和网关地址。 如果对 TCP/IP 堆栈的更改删除了这些设置，则微型端口驱动程序必须重置 IP 和网关地址。

小型端口驱动程序应使用以下过程在删除地址时收到通知，并且必须再次重置。

1.  在 **驱动程序初始化** 期间，微型端口驱动程序应指定一个回调函数，以便使用 [**NotifyIpInterfaceChange**](/previous-versions/windows/hardware/drivers/ff568805(v=vs.85))注册 IP 接口更改通知。 Windows 将调用 wheneven 函数，以添加、删除或更改 IP 接口。

2.  在 **适配器初始化** 过程中，微型端口驱动程序应保存在微型端口驱动程序的本地适配器上下文中将从传递给微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的 [**NDIS \_ 微型端口 \_ INIT \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构中的 **LUID** 值。 此值包含标识适配器接口的 *NetLuid* ，用于通知回调。

3.  在 **通知回调** 中，Windows 将以下参数传递给注册到 [**NotifyIpInterfaceChange**](/previous-versions/windows/hardware/drivers/ff568805(v=vs.85))的通知函数：

    -   一个指向 [**MIB \_ IPINTERFACE \_ 行**](/previous-versions/windows/hardware/drivers/ff559254(v=vs.85)) 结构的指针，该结构包含微型端口适配器接口的 *NetLuid* 。
    -   通知的类型，可以是 **MibAddInstance**、 **MibDeleteInstance** 或 **MibParameterNotification**。

    当适配器处于连接状态且通知类型为 **MibAddInstance**，并且 [**MIB \_ IPINTERFACE \_ 行**](/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))中的 *NetLuid* 对应于在适配器初始化期间保存的某个微型端口驱动程序适配器时，微型端口驱动程序应重置 IP 和网关地址。

    然后，小型端口驱动程序应遵循设置 MB 接口的 IP 地址，并设置默认的网关地址过程来重置相应的地址。

4.  在 **驱动程序卸载** 期间，微型端口驱动程序应使用 [**CancelMibChangeNotify2**](/previous-versions/windows/hardware/drivers/ff544864(v=vs.85)) IP helper 函数取消注册通知回调函数。

### <a name="setting-the-ip-address-for-the-mb-interface"></a>设置 MB 接口的 IP 地址

若要设置 IPv4 地址，请使用以下过程。 你可以使用类似的 IP Helper 功能来设置 IPv6 地址。

1.  使用 [**GetUnicastIpAddressTable**](/previous-versions/windows/hardware/drivers/ff552594(v=vs.85)) IP Helper 函数查找系统中的所有 IP 地址条目。

2.  对于其 **InterfaceLuid** 值与 MB 接口的 **InterfaceLuid** 匹配的每个条目：
    1.  查找与先前连接中使用的 IP 地址匹配的 IP 地址条目。 首次连接时，不会有以前的 IP 地址。
    2.  如果新 IP 地址与以前的 IP 地址不同，请使用 [**DeleteUnicastIpAddressEntry**](/previous-versions/windows/hardware/drivers/ff546370(v=vs.85)) IP Helper 函数删除以前连接 ip 地址的 IP 地址条目。
    3.  如果新 IP 地址与以前的 IP 地址相同，请验证所需的条目是否已存在。

3.  如果微型端口驱动程序在上一循环中找不到所需的 IP 地址条目，则它应添加新条目。
    1.  使用 [**InitializeUnicastIpAddressEntry**](/previous-versions/windows/hardware/drivers/ff554886(v=vs.85)) IP Helper 函数初始化 [**MIB \_ UNICASTIPADDRESS \_ 行**](/previous-versions/windows/hardware/drivers/ff559308(v=vs.85)) 结构，并设置结构的以下成员：
        1.  根据需要设置 **InterfaceLuid** 或 **InterfaceIndex** 成员。
        2.  设置 **OnlinePrefixLength** 成员。 这是子网掩码中的值为1的位数。 例如，如果子网掩码为255.255.255.0，则 **OnlinePrefixLength** 应为24。
        3.  设置 **地址** 成员。
        4.  将 **PrefixOrigin** 成员设置为 **IpPrefixOriginManual**。

    2.  将初始化的 MIB \_ UNICASTADDRESS \_ 行结构传递到 [**CreateUnicastIpAddressEntry**](/previous-versions/windows/hardware/drivers/ff546227(v=vs.85)) ip HELPER 函数以创建 IP 地址条目。

### <a name="setting-default-gateway-address"></a>设置默认网关地址

若要设置 IPv4 网关地址，请使用以下过程。 你可以使用类似的 IP Helper 功能来设置 IPv6 网关地址。

1.  使用 [**GetIpForwardTable2**](/previous-versions/windows/hardware/drivers/ff552536(v=vs.85)) IP Helper 函数获取系统中的所有路由条目。

2.  对于其 **InterfaceLuid** 值与 MB 接口的 **InterfaceLuid** 值匹配的每个项，如果 **DestinationPrefix** 为 "0.0.0.0/0"，请调用 [**DeleteIpForwardEntry2**](/previous-versions/windows/hardware/drivers/ff546365(v=vs.85)) IP Helper 函数以删除路由（如果 **NextHop** 不等于新的网关地址）。 否则，该路由条目已在系统中。

3.  如果微型端口驱动程序在上一循环中找不到所需的路由条目，则应通过使用 [**InitializeIpForwardEntry**](/previous-versions/windows/hardware/drivers/ff554882(v=vs.85)) IP Helper 函数初始化 [**MIB \_ IPFORWARD \_ table2.row2**](/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)) 结构来添加新条目。 初始化结构的以下成员：

    **InterfaceLuid** 或 **InterfaceIndex** 。

    为默认网关将 **DestinationPrefix** 设置为 0.0.0.0/0。  (前缀 = 0.0.0.0，PrefixLength = 0) 

    将 **NextHop** 设置为默认网关的 IP 地址。

    其他成员在初始化期间设置为默认值。 微型端口驱动程序应使用这些成员的默认值。

4.  将 [**MIB \_ IPFORWARD \_ table2.row2**](/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)) 结构传递到 [**CreateIpForwardEntry2**](/previous-versions/windows/hardware/drivers/ff546209(v=vs.85)) IP Helper 函数，以设置新的默认网关地址。

### <a name="to-set-dns-addresses"></a>设置 DNS 地址

-   设置 **NameServer** 注册表项，如 [MB dns 更新](mb-dns-updates.md) 中所述，用于通知 WINDOWS 已更新的 DNS 地址。

 

