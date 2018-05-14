---
title: Elemento InstanceSelection (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1f00127f58bb1f8c5a6792bec3ddcb8420f0d24b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="instanceselection-element-assl"></a>Elemento InstanceSelection (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Valor predeterminado|*None*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas siguientes:  
  
|Value|Description|  
|-----------|-----------------|  
|*Ninguno*|No muestre una lista de selección. Permite a los usuarios especificar directamente los valores.|  
|*Lista desplegable*|El número de elementos es lo suficientemente pequeño como para mostrarlos en una lista desplegable.|  
|*Listaa*|El número de elementos es demasiado grande para una lista desplegable, pero no requiere filtrado.|  
|*FilteredList*|El número de elementos es lo suficientemente grande como para requerir que los usuarios filtren los elementos que se van a mostrar.|  
|*MandatoryFilter*|El número de elementos es tan grande que siempre se debe filtrar.|  
  
 La enumeración que corresponde a los valores permitidos para **InstanceSelection** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.InstanceSelection>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
