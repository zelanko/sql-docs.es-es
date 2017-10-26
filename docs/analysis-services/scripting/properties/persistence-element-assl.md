---
title: Elemento Persistence (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Persistence Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Persistence
helpviewer_keywords:
- Persistence element
ms.assetid: dafe3df2-4795-48ea-bebe-33c1a3bf18b6
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fd24f62070693d74949bd9ff328c87f66567929f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="persistence-element-assl"></a>Elemento Persistence (ASSL)
  Determina qué partes de los datos de origen enlazados son dinámicos y se comprueban para las actualizaciones con la frecuencia especificada por el [RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Persistence>...</Persistence>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*NotPersisted*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*NotPersisted*|Metadatos del origen, miembros y datos son todos dinámicos.|  
|*Metadatos*|Los metadatos del origen son estáticos, pero los miembros y datos son dinámicos.|  
|*Todos*|Metadatos del origen, miembros y datos son todos estáticos.|  
  
 La enumeración que corresponde a los valores permitidos para **persistencia** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PersistenceType>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

