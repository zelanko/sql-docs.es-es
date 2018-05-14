---
title: Elemento OrderBy (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2d2c8caf392e5d80d82b06a7d7fd9b5cd724a35e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="orderby-element-assl"></a>Elemento OrderBy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe cómo ordenar los miembros incluidos en el atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <OrderBy>...</OrderBy>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Nombre*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nombre*|Se ordena por el nombre de miembro.|  
|*Key*|Se ordena por la clave de miembro.|  
|*AttributeKey*|Se ordena por la clave de miembro del atributo especificado en el [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md) elemento de **DimensionAttribute**.|  
|*AttributeName*|Se ordena por el nombre de miembro del atributo especificada en el elemento **OrderByAttributeID** de **DimensionAttribute**.|  
  
 La enumeración que corresponde a los valores permitidos para **OrderBy** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.OrderBy>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
