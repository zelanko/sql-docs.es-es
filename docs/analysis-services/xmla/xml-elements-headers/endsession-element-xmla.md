---
title: Elemento EndSession (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9529d3d704fd1c8bb8eded66c713137b1233d99a
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574927"
---
# <a name="endsession-element-xmla"></a>Elemento EndSession (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para terminar una sesión existente en una instancia de Analysis Services.  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <EndSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis"  
         SessionId="string" />  
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
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|SessionId|Atributo **String** requerido que identifica la sesión que se va a terminar. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] utiliza un identificador único global (GUID) para identificar una sesión.|  
  
## <a name="remarks"></a>Notas  
 El **EndSession** encabezado elemento forma parte de la solicitud SOAP enviada a una sesión existente explícitamente iniciada un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. Si se envía el elemento de encabezado **EndSession** , pero contiene un identificador de la sesión que ya no es válido, se devuelve un error de SOAP que indica que no se puede encontrar la sesión.  
  
## <a name="see-also"></a>Vea también
 [Elemento BeginSession &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)   
 [Elemento de la sesión &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [Administrar conexiones y sesiones &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Encabezados &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
