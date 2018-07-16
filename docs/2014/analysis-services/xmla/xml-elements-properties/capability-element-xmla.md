---
title: Elemento Capability (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Capability Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Capability
- http://schemas.microsoft.com/analysisservices/2003/engine#Capability
- microsoft.xml.analysis.capability
helpviewer_keywords:
- Capability element
ms.assetid: 544a733e-77fc-48a0-8f92-9cd1fdbcf824
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a5b14b43b41f74c05d433c599b18486c5737b27c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201895"
---
# <a name="capability-element-xmla"></a>Elemento Capability (XMLA)
  Indica la compatibilidad con una prestación de protocolo en el elemento primario [ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md) elemento de encabezado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `Capability` elemento indica que cierta prestación específica, como binario o compresión, es compatible con la aplicación que incluye el `ProtocolCapabilities` elemento de encabezado en el encabezado SOAP de la solicitud SOAP o la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que incluyen el `ProtocolCapabilities` elemento de encabezado en el encabezado SOAP de la respuesta SOAP. El valor del elemento `Capability` es el nombre de la función que se va a admitir.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite las prestaciones descritas en la siguiente tabla.  
  
|Nombre de la prestación|Descripción|  
|---------------------|-----------------|  
|sx|Compatibilidad de XML binario|  
|xpress|Compatibilidad de compresión|  
  
## <a name="see-also"></a>Vea también  
 [Administrar conexiones y sesiones &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
