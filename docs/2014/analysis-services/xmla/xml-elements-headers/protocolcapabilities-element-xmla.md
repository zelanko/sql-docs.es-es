---
title: Elemento ProtocolCapabilities (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProtocolCapabilities Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12e4cac0c9846582c40213048e71c7f3793ff736
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219045"
---
# <a name="protocolcapabilities-element-xmla"></a>Elemento ProtocolCapabilities (XMLA)
  Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para identificar las capacidades de protocolo entre una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y una aplicación cliente.  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/engine  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <ProtocolCapabilities xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
         <Capability>...</Capability>  
      </ProtocolCapabilities>  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Capacidad](../xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `ProtocolCapabilities` permite a las aplicaciones cliente negociar las capacidades de protocolo, como XML binario o compatibilidad de compresión, con una instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en cualquier momento. La negociación de protocolo conlleva los pasos siguientes:  
  
1.  La aplicación cliente identifica su capacidad de protocolo enviando una solicitud SOAP que incluye el `ProtocolCapabilities` elemento como parte del encabezado SOAP.  
  
2.  La instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] recibe y procesa la solicitud SOAP.  
  
3.  Si la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tiene la misma capacidad de protocolo que la solicitada, la instancia envía una respuesta SOAP que incluye el mismo elemento `ProtocolCapabilities` enviado en la solicitud SOAP y el protocolo se negocia correctamente. En caso contrario, las capacidades de protocolo no se negocian correctamente y la instancia devuelve un error de SOAP.  
  
 Después de negociar correctamente las capacidades de protocolo, ¿cuánto tiempo la aplicación de cliente y el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] utilicen instancia un protocolo determinado depende de si la sesión es explícita o implícita:  
  
-   Una sesión explícita es aquella que se crea utilizando el [BeginSession](session-element-xmla.md) elemento de encabezado. Para una sesión explícita, se utiliza el protocolo negociado hasta que la aplicación de cliente envía un nuevo `ProtocolCapabilities` elemento o finalice la sesión.  
  
-   Una sesión implícita la crea una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y no es especificada explícitamente por la aplicación cliente al enviar una solicitud SOAP. Para una sesión implícita, el protocolo negociado se utiliza solamente hasta que se completa la solicitud SOAP.  
  
 Las capacidades de protocolo no tienen que ser negociadas explícitamente. Es decir, una aplicación cliente no tiene que incluir un `ProtocolCapabilities` elemento como parte de la solicitud SOAP. Si una solicitud SOAP no incluye un elemento `ProtocolCapabilities`, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] responde utilizando el mismo formato que la solicitud SOAP.  
  
## <a name="see-also"></a>Vea también  
 [Administrar conexiones y sesiones &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Encabezados &#40;XMLA&#41;](xml-elements-headers.md)  
  
  
