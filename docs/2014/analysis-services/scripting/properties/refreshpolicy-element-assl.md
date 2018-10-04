---
title: Elemento RefreshPolicy (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RefreshPolicy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshPolicy
helpviewer_keywords:
- RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6322c725a0c4b339425b9cc9e10aa6596c9fc34c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144435"
---
# <a name="refreshpolicy-element-assl"></a>Elemento RefreshPolicy (ASSL)
  Determina la frecuencia con la parte dinámica de la dimensión o grupo de medida (según lo especificado por el [persistencia](persistence-element-assl.md) elemento) está activada para los cambios.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
|Antecesor o elemento primario|Valor predeterminado|  
|------------------------|-------------------|  
|[DimensionBinding](../data-type/binding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|None|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*ByQuery*|Cada consulta comprueba si los datos de origen han cambiado.|  
|*ByInterval*|Origen de datos solo se comprueba los cambios en el intervalo especificado por [RefreshInterval](refreshinterval-element-assl.md).|  
  
 La enumeración que corresponde a los valores permitidos para `RefreshPolicy` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.RefreshPolicy>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Persistence &#40;ASSL&#41;](persistence-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
