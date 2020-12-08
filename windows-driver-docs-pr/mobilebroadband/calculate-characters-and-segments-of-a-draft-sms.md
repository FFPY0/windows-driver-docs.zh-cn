---
title: 计算短信草稿的字符数和段数
description: 计算短信草稿的字符数和段数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382695d7e832880ae369830ef81fd1313adfff85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782487"
---
# <a name="calculate-characters-and-segments-of-a-draft-sms"></a>计算短信草稿的字符数和段数


移动宽带 SMS 平台提供了一个函数，用于估计在多部分消息中使用的剩余字符数和段数 (在 SMS 消息的撰写过程中) 。

**注意**  
每个段中的字符数不是常量，并且根据消息正文中的文本字符串和网络类型而变化。 在 GSM 网络上，一条短信最多支持 160 7 位字符或 70 16 位字符。 由于附加的标头信息，跨越多个段的消息支持每个段 142 7 位字符。

 

为在撰写 SMS 消息时使用的段数提供准确估计会提高用户信心，因为用户通常按发送的短信收费。

**JavaScript 代码示例**

``` syntax
var smsMessage = new Windows.Devices.Sms.SmsTextMessage();
smsMessage.body = id('messageText').value;  // Set message body text to text of messageText HTML element
var messageLength = smsDevice.calculateLength(smsMessage);
id('remainingCharsCount').innerText = messageLength.charactersPerSegment - messageLength.characterCountLastSegment;
id('messageSegmentsCount').innerText = messageLength.segmentCount;
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用文本模式界面发送短信](calculate-characters-and-segments-of-a-draft-sms.md)

 

 






