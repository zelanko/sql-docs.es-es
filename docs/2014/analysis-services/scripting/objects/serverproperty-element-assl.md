---
title: Elemento ServerProperty (ASSL) | Documentos de Microsoft
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
- ServerProperty Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SERVERPROPERTY
helpviewer_keywords:
- ServerProperty element
ms.assetid: f152a1b5-0972-40d8-907f-f131c2a108bb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6cb62681b0c25c83d54076a67a37addc764102da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105219"
---
# <a name="serverproperty-element-assl"></a>Elemento ServerProperty (ASSL)
  Define una propiedad del servidor asociada con un [Server](server-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ServerProperties>  
   <ServerProperty>  
      <Name>...</Name>  
      <Value>...</Value>  
            <RequiresRestart>...</RequiresRestart>  
            <PendingValue>...</PendingValue>  
      <DefaultValue>...</DefaultValue>  
      <DisplayFlag>...</DisplayFlag>  
   </ServerProperty>  
</ServerProperties>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[ServerProperties](../collections/serverproperties-element-assl.md)|  
|Elementos secundarios|[DefaultValue](../properties/value-element-assl.md), [DisplayFlag](../properties/displayflag-element-assl.md), [nombre](../properties/name-element-assl.md), [PendingValue](../properties/pendingvalue-element-assl.md), [RequiresRestart](../properties/requiresrestart-element-assl.md), [valor](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El `ServerProperty` elemento describe los datos y metadatos para una propiedad del servidor asociada a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. A diferencia de los elementos contenidos por otras colecciones en Analysis Services Scripting Language (ASSL), el elemento `ServerProperty` utiliza pares de nombre/valor en lugar de elementos nombrados de manera explícita para describir las propiedades del servidor. Los pares de nombre/valor proporcionan flexibilidad y extensibilidad.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Server &#40;ASSL&#41;](server-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  