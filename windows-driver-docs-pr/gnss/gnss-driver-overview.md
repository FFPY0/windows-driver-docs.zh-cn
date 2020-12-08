---
title: 全局导航卫星系统 (GNSS) 驱动程序概述
description: 使用本指南了解如何通过全局导航卫星系统 (GNSS) 驱动程序实现 DeviceIoControl Api，以便 HLOS 如 GNSS 适配器可以访问 GNSS 功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7be8b38be6fabe388b1cd17987c13a8538aa140
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783943"
---
# <a name="global-navigation-satellite-system-gnss-driver-overview"></a>全局导航卫星系统 (GNSS) 驱动程序概述

使用全局导航卫星系统 (GNSS) 驱动程序设计指南来了解如何使用 GNSS 驱动程序实现 **DeviceIoControl** api，使高级操作系统组件 (HLOS) 如 GNSS 适配器可以访问所需的 GNSS 功能。

可通过 IHV 增强 GNSS 功能，以更低的功率成本提供位置，或在需要时提供更好的性能。

新的 GNSS 驱动程序由 Ihv 完全拥有和提供，不会在内核模式下运行任何 Microsoft 自有代码。

> [!NOTE]
> Ihv 不能将筛选器驱动程序添加到 GNSS/Location 堆栈。 筛选器驱动程序很难进行调试和维护，因此，一般不建议使用它们。 除此之外，在未来，Microsoft 可能还需要在 GNSS 设备堆栈中添加筛选器驱动程序，以便扩展功能，并将其他筛选器驱动程序用于 Ihv，使体系结构更复杂。

驱动程序遵循一般的 UMDF 2.0 模型， (功能驱动程序的用户模式驱动程序框架) 。 可以使用 KMDF (内核模式驱动程序框架) 驱动程序，但强烈建议不要这样做，因为它们增加了平台不稳定的风险，因而难以调试，它们无法直接使用用户模式的操作系统组件。
本设计指南假定你基本熟悉 UMDF 2.0、Windows 内核模式编程、内核 i/o 管理、电源管理和 PnP 设备堆栈。

## <a name="related-topics"></a>相关主题

[全局导航卫星系统 (GNSS) 驱动程序要求](gnss-driver-requirements.md)  

[全局导航卫星系统 (GNSS) 驱动程序体系结构](gnss-driver-architecture.md)  
