---
title: Elemento ProtocolCapabilities (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ProtocolCapabilities Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 511cca07c0505db7bd1aaa21bed923498137e04f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="protocolcapabilities-element-xmla"></a>Elemento ProtocolCapabilities (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para identificar las capacidades de protocolo entre una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y una aplicación cliente.  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/engine`  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Capacidad](../../../analysis-services/xmla/xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **ProtocolCapabilities** elemento permite que las aplicaciones cliente negociar las capacidades de protocolo, como XML binario o compatibilidad con la compresión, con un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia en cualquier momento. La negociación de protocolo conlleva los pasos siguientes:  
  
1.  La aplicación cliente identifica su capacidad de protocolo enviando una solicitud SOAP que incluye el elemento **ProtocolCapabilities** como parte del encabezado SOAP.  
  
2.  La instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] recibe y procesa la solicitud SOAP.  
  
3.  Si el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia tiene la misma capacidad de protocolo que la solicitada, la instancia envía una respuesta SOAP que incluye el mismo **ProtocolCapabilities** elemento enviados en la solicitud SOAP, y el protocolo se ha se negocian correctamente. En caso contrario, las capacidades de protocolo no se negocian correctamente y la instancia devuelve un error de SOAP.  
  
 Después de negociar correctamente las capacidades de protocolo, el tiempo que las aplicaciones cliente y el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia utilicen un protocolo determinado depende de si la sesión es explícita o implícita:  
  
-   Una sesión explícita es aquella que se crea utilizando el [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) elemento de encabezado. Para una sesión explícita, el protocolo negociado se utiliza bien hasta que la aplicación cliente envía un nuevo elemento **ProtocolCapabilities** o bien hasta que la sesión termina.  
  
-   Una sesión implícita la crea una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y no es especificada explícitamente por la aplicación cliente al enviar una solicitud SOAP. Para una sesión implícita, el protocolo negociado se utiliza solamente hasta que se completa la solicitud SOAP.  
  
 Las capacidades de protocolo no tienen que ser negociadas explícitamente. Es decir, una aplicación cliente no tiene que incluir un elemento **ProtocolCapabilities** como parte de la solicitud SOAP. Si una solicitud SOAP no incluye un **ProtocolCapabilities** elemento, el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia responde con el mismo formato que la solicitud SOAP.  
  
## <a name="see-also"></a>Vea también  
 [Administrar las conexiones y sesiones &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Encabezados &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
