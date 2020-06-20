---
title: StorageBoundInMB (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- StorageBoundInMB element
ms.assetid: a8374910-bf68-4edb-b464-53a3a705e7f4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12dad78b6094e940a926fbcde7147d66ca1e2dfe
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007601"
---
# <a name="storageboundinmb-element-dta"></a>StorageBoundInMB (DTA, elemento)
  Especifica el espacio máximo en megabytes que puede consumir la recomendación de optimización del Asistente para la optimización de motor de base de datos (conjunto de índices y particiones).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <StorageBoundInMB>...</ StorageBoundInMB >  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`unsignedInt`, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Solo puede utilizarse una vez para el elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](tuningoptions-element-dta.md)|  
|**Elementos secundarios**|None|  
  
## <a name="remarks"></a>Observaciones  
 Cuando se optimizan varias bases de datos, se tienen en cuenta las recomendaciones para todas las bases de datos sobre el cálculo del espacio. De forma predeterminada, el Asistente para la optimización de motor de base de datos asume el menor de los siguientes tamaños de almacenamiento:  
  
-   Tres veces el tamaño actual de los datos sin procesar, lo que incluye el tamaño total de los montones y los clúster de las tablas.  
  
-   El espacio disponible en todas las unidades de disco adjuntas más el tamaño de los datos sin procesar.  
  
 El tamaño de almacenamiento predeterminado no incluye los índices no clúster ni las vistas indizadas.  
  
 Si el valor especificado para el elemento `StorageBoundInMB` supera el espacio en disco real, el Asistente para la optimización de motor de base de datos devuelve un error, aunque continúa optimizando. Una vez finalizada la optimización, puede agregar espacio en disco si decide seguir la recomendación.  
  
## <a name="example"></a>Ejemplo  
  
## <a name="description"></a>Descripción  
 El siguiente ejemplo de código muestra cómo establecer un límite de 1500 megabytes como el máximo espacio en disco que una recomendación de optimización puede utilizar:  
  
## <a name="code"></a>Código  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <StorageBoundInMB>1500</StorageBoundInMB>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
