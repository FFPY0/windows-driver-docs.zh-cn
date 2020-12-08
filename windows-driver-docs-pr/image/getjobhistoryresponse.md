---
title: GetJobHistoryResponse 元素
description: 必需的 GetJobHistoryResponse 元素返回已完成作业的摘要。
keywords:
- GetJobHistoryResponse 元素图像设备
topic_type:
- apiref
api_name:
- wscn GetJobHistoryResponse
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: d4583959591e2c294ad32a05700ffd811cbac3be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808793"
---
# <a name="getjobhistoryresponse-element"></a>GetJobHistoryResponse 元素

必需的 **GetJobHistoryResponse** 元素返回已完成作业的摘要。

## <a name="usage"></a>使用情况

```xml
<wscn:GetJobHistoryResponse>
  child elements
</wscn:GetJobHistoryResponse>
```

## <a name="attributes"></a>特性

没有特性。

## <a name="child-elements"></a>子元素

| 元素 |
|--|
| [**JobHistory**](jobhistory.md) |

## <a name="parent-elements"></a>父元素

没有父元素。

## <a name="remarks"></a>备注

WSD 扫描服务必须支持 **GetJobHistoryResponse** 操作元素。

客户端可以调用 [**GetJobHistoryRequest**](getjobhistoryrequest.md) 来确定先前完成的作业的与作业相关的变量的值。 WSD 扫描服务必须使用包含客户端请求的信息的 **GetJobHistoryResponse** 操作元素或适当的错误代码进行响应。

WSD 扫描服务维护的作业历史记录量是特定于实现的。

## <a name="examples"></a>示例

下面的代码示例演示如何返回无作业历史记录，以响应客户端对作业历史记录的请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory />
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

下面的代码示例返回最后两个已完成作业的作业和关联数据的列表。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory>
        <wscn:JobSummary>
          <wscn:JobId>1</wscn:JobId>
          <wscn:JobName>SampleJob 1</wscn:JobName>
          <wscn:JobOriginatingUserName>Joe.Smith</wscn:JobOriginatingUserName>
          <wscn:JobState>Completed</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>None</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>4</wscn:ScansCompleted>
        </wscn:JobSummary>
        <wscn:JobSummary>
          <wscn:JobId>2</wscn:JobId>
          <wscn:JobName>Sample Job 2</wscn:JobName>
          <wscn:JobOriginatingUserName>JaneRogers</wscn:JobOriginatingUserName>
          <wscn:JobState>Canceled</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>JobCanceledAtDevice</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>1</wscn:ScansCompleted>
        </wscn:JobSummary>
      </wscn:JobHistory>
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅

[**GetJobHistoryRequest**](getjobhistoryrequest.md)

[**JobHistory**](jobhistory.md)
