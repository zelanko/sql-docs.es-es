---
title: Elemento InstanceSelection (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- InstanceSelection Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41587ee5acd29ca8038e188a3a3a5681bb7b91d0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131465"
---
# <a name="instanceselection-element-assl"></a>Elemento InstanceSelection (ASSL)
  Proporciona una sugerencia a las aplicaciones cliente acerca de cómo se debe mostrar una lista de elementos, según el número estimado de elementos de la lista.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Ninguno*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Ninguno*|No muestre una lista de selección. Permite a los usuarios especificar directamente los valores.|  
|*Lista desplegable*|El número de elementos es lo suficientemente pequeño como para mostrarlos en una lista desplegable.|  
|*Listaa*|El número de elementos es demasiado grande para una lista desplegable, pero no requiere filtrado.|  
|*FilteredList*|El número de elementos es lo suficientemente grande como para requerir que los usuarios filtren los elementos que se van a mostrar.|  
|*MandatoryFilter*|El número de elementos es tan grande que siempre se debe filtrar.|  
  
 La enumeración que corresponde a los valores permitidos para `InstanceSelection` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.InstanceSelection>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
