---
title: Elemento RefreshPolicy (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: RefreshPolicy Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: RefreshPolicy
helpviewer_keywords: RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fe18ffe7b7453c0591591acb8f92d37cd545724f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="refreshpolicy-element-assl"></a>Elemento RefreshPolicy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina la frecuencia con la parte dinámica del grupo de medida o dimensión (según lo especificado por el [persistencia](../../../analysis-services/scripting/properties/persistence-element-assl.md) elemento) está activada para los cambios.  
  
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
|Valor predeterminado|Vea la siguiente tabla.|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
|Antecesor o elemento primario|Valor predeterminado|  
|------------------------|-------------------|  
|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|Ninguno|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ByQuery*|Cada consulta comprueba si los datos de origen han cambiado.|  
|*ByInterval*|Origen de datos solo se comprueba los cambios en el intervalo especificado por [RefreshInterval](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md).|  
  
 La enumeración que corresponde a los valores permitidos para **RefreshPolicy** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.RefreshPolicy>.  
  
## <a name="see-also"></a>Vea también  
 [Persistence, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
