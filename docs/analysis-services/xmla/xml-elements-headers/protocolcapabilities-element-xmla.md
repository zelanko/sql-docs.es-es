---
title: Elemento ProtocolCapabilities (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a7219d8b08480f8e05c1ea0ea14d1bb04e537bdc
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="protocolcapabilities-element-xmla"></a>Elemento ProtocolCapabilities (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para identificar las capacidades de protocolo entre una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y una aplicación cliente.  
  
 **Namespace** `http://schemas.microsoft.com/analysisservices/2003/engine`  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
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
 [Administrar las conexiones y sesiones & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Encabezados & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
