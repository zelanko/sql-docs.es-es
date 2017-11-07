---
title: Elemento Capability (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Capability Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Capability
- http://schemas.microsoft.com/analysisservices/2003/engine#Capability
- microsoft.xml.analysis.capability
helpviewer_keywords:
- Capability element
ms.assetid: 544a733e-77fc-48a0-8f92-9cd1fdbcf824
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 50a1509e5b4b51778e329dec7bea9554cfca4234
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="capability-element-xmla"></a>Elemento Capability (XMLA)
  Indica la compatibilidad con una prestación de protocolo en el elemento primario de [ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md) elemento de encabezado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **capacidad** elemento indica que cierta prestación específica, como binario o compresión, es compatible con la aplicación que incluyen la **ProtocolCapabilities** elemento de encabezado en el Encabezado SOAP de la solicitud SOAP o la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que incluyen la **ProtocolCapabilities** elemento de encabezado en el encabezado SOAP de la respuesta SOAP. El valor del elemento **Capability** es el nombre de la función que se va a admitir.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite las prestaciones descritas en la siguiente tabla.  
  
|Nombre de la prestación|Descripción|  
|---------------------|-----------------|  
|sx|Compatibilidad de XML binario|  
|xpress|Compatibilidad de compresión|  
  
## <a name="see-also"></a>Vea también  
 [Administrar las conexiones y sesiones &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

