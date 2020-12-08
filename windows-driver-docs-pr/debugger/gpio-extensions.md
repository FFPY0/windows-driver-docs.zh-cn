---
title: GPIO 扩展
description: 常规用途输入/输出 (GPIO) extension 命令显示 GPIO 控制器的软件状态。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a816d83707e2f9da474a5a2ddaf5488a51e16684
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837343"
---
# <a name="gpio-extensions"></a>GPIO 扩展


常规用途输入/输出 (GPIO) extension 命令显示 GPIO 控制器的软件状态。 这些命令显示 GPIO 框架扩展驱动程序所维护的数据结构 ( # A0) 的信息。 有关 GPIO framework 扩展的信息，请参阅 [常规用途 i/o (GPIO) 驱动程序](/windows-hardware/drivers/ddi/_gpio/)。

GPIO 调试器扩展命令在 gpiokd.dll 中实现。 若要加载 GPIO 命令，请在调试器中输入 " **load gpiokd.dll** 。

每个 GPIO 控制器都有一组银行。 每个银行都有一个包含 pin 数组的固定表。 GPIO 调试器扩展命令显示有关 GPIO 控制器、银行、固定表和 pin 的信息。

## <a name="span-iddata-structures-used-by-the-gpio-commandsspanspan-iddata_structures_used_by_the_gpio_commandsspandata-structures-used-by-the-gpio-commands"></a><span id="data-structures-used-by-the-gpio-commands"></span><span id="DATA_STRUCTURES_USED_BY_THE_GPIO_COMMANDS"></span>GPIO 命令使用的数据结构


GPIO 调试器扩展命令使用这些数据结构，这些数据结构由 Msgpioclx.sys 定义。

<span id="msgpioclx__DEVICE_EXTENSION"></span><span id="msgpioclx__device_extension"></span><span id="MSGPIOCLX__DEVICE_EXTENSION"></span>**msgpioclx！ \_设备 \_ 扩展**  
GPIO framework 扩展驱动程序的设备扩展结构。 此结构保存有关单个 GPIO 控制器的信息。

<span id="msgpioclx__GPIO_BANK_ENTRY"></span><span id="msgpioclx__gpio_bank_entry"></span><span id="MSGPIOCLX__GPIO_BANK_ENTRY"></span>**msgpioclx！ \_GPIO \_ BANK \_ 条目**  
此结构保存有关 GPIO 控制器的单个银行的信息。

<span id="msgpioclx__GPIO_PIN_INFORMATION_ENTRY"></span><span id="msgpioclx__gpio_pin_information_entry"></span><span id="MSGPIOCLX__GPIO_PIN_INFORMATION_ENTRY"></span>**msgpioclx！ \_GPIO \_ PIN \_ 信息 \_ 条目**  
此结构保存有关 GPIO 控制器银行中单个 pin 的信息。

## <a name="span-idgetting_started_with_gpio_debuggingspanspan-idgetting_started_with_gpio_debuggingspanspan-idgetting_started_with_gpio_debuggingspangetting-started-with-gpio-debugging"></a><span id="Getting_started_with_GPIO_debugging"></span><span id="getting_started_with_gpio_debugging"></span><span id="GETTING_STARTED_WITH_GPIO_DEBUGGING"></span>GPIO 调试入门


若要开始调试 GPIO 问题，请输入 [**！ gpiokd. clientlist**](-gpiokd-clientlist.md) 命令。 **！ Gpiokd. clientlist** 命令显示所有已注册的 gpio 控制器的概述，并显示可传递给其他 GPIO 调试器命令的地址。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-help.md" data-raw-source="[!gpiokd.help](-gpiokd-help.md)">!gpiokd.help</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-help.md" data-raw-source="[!gpiokd.help](-gpiokd-help.md)">！ Gpiokd</a></strong>命令显示 GPIO 调试器扩展命令的帮助。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">!gpiokd.bankinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">！ Gpiokd. bankinfo</a></strong>命令显示有关 GPIO bank 的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">!gpiokd.clientlist</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">！ Clientlist</a></strong>命令显示所有已注册的 GPIO 控制器 gpiokd。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">!gpiokd.gpioext</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">！ Gpiokd. gpioext</a></strong>命令显示有关 GPIO 控制器的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">!gpiokd.pininfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">！ Gpiokd. pininfo</a></strong>命令显示有关指定 GPIO pin 的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">!gpiokd.pinisrvec</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">！ Gpiokd. pinisrvec</a></strong>命令显示 (ISR 的中断服务例程) 指定的 pin 的矢量信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">!gpiokd.pintable</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">！ Gpiokd. pintable</a></strong>命令显示有关 GPIO pin 数组的信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[专业扩展命令](specialized-extensions.md)

 

