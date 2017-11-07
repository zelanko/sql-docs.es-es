---
title: Elemento InstanceSelection (ASSL) | Documentos de Microsoft
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
- InstanceSelection Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4587536131aa3484846bc241a08be866a30d1da6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas siguientes:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Ninguno*|No muestre una lista de selección. Permite a los usuarios especificar directamente los valores.|  
|*Lista desplegable*|El número de elementos es lo suficientemente pequeño como para mostrarlos en una lista desplegable.|  
|*Listaa*|El número de elementos es demasiado grande para una lista desplegable, pero no requiere filtrado.|  
|*FilteredList*|El número de elementos es lo suficientemente grande como para requerir que los usuarios filtren los elementos que se van a mostrar.|  
|*MandatoryFilter*|El número de elementos es tan grande que siempre se debe filtrar.|  
  
 La enumeración que corresponde a los valores permitidos para **InstanceSelection** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.InstanceSelection>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

