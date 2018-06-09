---
title: Elemento BeginSession (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 34bdcfb37eaf5e2f960b7ea282c2628eca91916f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34574847"
---
# <a name="beginsession-element-xmla"></a>Elemento BeginSession (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Usa un encabezado SOAP en un mensaje de solicitud SOAP para iniciar una nueva sesión en una instancia de Analysis Services.  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <BeginSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis" />  
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
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **BeginSession** encabezado elemento forma parte de una solicitud SOAP enviada a una [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia e inicia explícitamente una sesión nueva en la instancia. El encabezado SOAP devuelto por la respuesta SOAP contiene un [sesión](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md) elemento que identifica la sesión nuevo. Este nuevo identificador de sesión se almacenan y se enviarán en solicitudes SOAP posteriores utilizando el **sesión** elemento de encabezado.  
  
 Si el **BeginSession** no se envía el elemento de encabezado, no se inicia explícitamente una sesión. Si no se inicia una sesión explícitamente, no se pueden administrar transacciones en esa sesión. En otras palabras, no puede usar el siguiente código XML para los comandos de Analysis (XMLA): [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), y [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md). Todos los métodos XMLA y comandos ejecutados en una sesión iniciada implícitamente se consideran transacciones atómicas.  
  
## <a name="see-also"></a>Vea también
 [Elemento EndSession &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Elemento de la sesión &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [Administrar conexiones y sesiones &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Encabezados &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
