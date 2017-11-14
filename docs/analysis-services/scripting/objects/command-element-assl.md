---
title: Comando elemento (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Command Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Command
helpviewer_keywords:
- Command element
ms.assetid: 277598b5-9939-4d7f-8c75-06470c3fabdd
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd3c9638d6c63a7b7a44d201659d666474fbf1c5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="command-element-assl"></a>Elemento Command (ASSL)
  Define un comando que está disponible para su uso en el contexto del elemento primario de la [comandos](../../../analysis-services/scripting/collections/commands-element-assl.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Commands>  
   <Command>  
      <Text>...</Text>  
   </Command>  
</Commands >  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Comandos](../../../analysis-services/scripting/collections/commands-element-assl.md)|  
|Elementos secundarios|[Texto](../../../analysis-services/scripting/properties/text-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Command>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

