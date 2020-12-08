---
title: EventingService WSDL
description: EventingService WSDL
keywords:
- WSDBIT 工具 WDK，WSDL
- WSDAPI 基本互操作性工具 WDK、WSDL
- EventingService 服务 WDK WSDBIT
- WSDBIT 工具 WDK，服务
- WSDAPI 基本互操作性工具 WDK，服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb8d4c092b03acee3fdf599bcf8f0b1fbe78cf73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784043"
---
# <a name="eventingservice-wsdl"></a>EventingService WSDL

下面的代码示例演示了 EventingService WSDL。

```xml
<wsdl:definitions
 targetNamespace="http://schemas.example.org/EventingService"
 xmlns:tns="http://schemas.example.org/EventingService"
 xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
 xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"
 xmlns:wsdp="http://schemas.xmlsoap.org/ws/2005/05/devprof"
 xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
 xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy"
 xmlns:wsoap12="http://schemas.xmlsoap.org/wsdl/soap12/"
    xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd"
 xmlns:wsx="http://schemas.xmlsoap.org/ws/2004/09/mex"
 xmlns:wsf="http://schemas.xmlsoap.org/ws/2004/09/transfer" >

 <wsp:Policy wsu:Id="Eventing" >
 <wsdp:Profile />
 <wsdp:PushDelivery />
 <wsdp:DurationExpiration />
 <wsdp:ActionFilter />
 </wsp:Policy>

 <wsdl:types>
 <xs:schema
   targetNamespace="http://schemas.example.org/EventingService"
   xmlns:tns="http://schemas.example.org/EventingService"
   xmlns:xs="http://www.w3.org/2001/XMLSchema"
   elementFormDefault="qualified"
   blockDefault="#all">

 <xs:element name="SimpleEvent" type="tns:SimpleEventType" />
 <xs:complexType name="SimpleEventType">
     <xs:sequence/>
 </xs:complexType>

 <xs:element name="IntegerEvent" type="tns:IntegerEventType" />
 <xs:complexType name="IntegerEventType">
 <xs:sequence>
 <xs:element name="Param" type="xs:int" />
 <xs:any minOccurs="0"
 maxOccurs="unbounded"
 namespace="##other"
 processContents="lax" />
 </xs:sequence>
 <xs:anyAttribute namespace="##other"
 processContents="lax" />
 </xs:complexType>
 </xs:schema>
 </wsdl:types>

 <wsdl:message name="SimpleEventMessageOut">
 <wsdl:part name="parameters" element="tns:SimpleEvent" />
 </wsdl:message>
 <wsdl:message name="IntegerEventMessageOut">
 <wsdl:part name="parameters" element="tns:IntegerEvent" />
 </wsdl:message>

   <wsdl:portType name="EventingService" wse:EventSource="true" >
        <wsdl:operation name="SimpleEvent">
            <wsdl:output
                message="tns:SimpleEventMessageOut"
                wsa:Action="http://schemas.example.org/EventingService/SimpleEvent"/>
        </wsdl:operation>
        <wsdl:operation name="IntegerEvent">
            <wsdl:output
                message="tns:IntegerEventMessageOut"
                wsa:Action="http://schemas.example.org/EventingService/IntegerEvent"/>
        </wsdl:operation>
    </wsdl:portType>

 <wsdl:binding name="EventingServiceSoap12Binding" type="tns:EventingService">
 <wsoap12:binding style="document"
 transport="http://schemas.xmlsoap.org/soap/http" />
 <wsp:PolicyReference URI="#Eventing" wsdl:required="true" />
        <wsdl:operation name="SimpleEvent">
            <wsoap12:operation
                soapAction="http://schemas.example.org/EventingService/SimpleEvent" />
            <wsdl:output>
                <wsoap12:body use="literal" />
            </wsdl:output>
        </wsdl:operation>
        <wsdl:operation name="IntegerEvent">
            <wsoap12:operation
                soapAction="http://schemas.example.org/EventingService/IntegerEvent" />
            <wsdl:output>
                <wsoap12:body use="literal" />
            </wsdl:output>
        </wsdl:operation>
 </wsdl:binding>

 <wsdl:service name="EventingService">
 <wsdl:port
   name="EventingPort"
   binding="tns:EventingServiceSoap12Binding">
 <wsoap12:address
 location="http://localhost/WebService/Eventing.asmx" />
 </wsdl:port>
 </wsdl:service>

</wsdl:definitions>
```
