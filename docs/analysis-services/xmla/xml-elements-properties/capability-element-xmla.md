---
title: Elemento Capability (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: a53bcd66141dfb367cc54239d9d8faab0e0e6576
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="capability-element-xmla"></a>Elemento Capability (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Indica compatibilidad con una prestación de protocolo en el elemento primario de encabezado [ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md) .  
  
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
 [Administrar las conexiones y sesiones & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
