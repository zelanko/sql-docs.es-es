---
title: Elemento MembersWithDataCaption (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MembersWithDataCaption Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 87fb2787dd88f1adfac622f869cb8be841be16d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="memberswithdatacaption-element-assl"></a>Elemento MembersWithDataCaption (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Proporciona una cadena de plantilla utilizada para crear títulos para los miembros de datos generados por el sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeTranslation> <!-- or DimensionAttribute -->  
   ...  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   ...  
</AttributeTranslation>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la **MembersWithDataCaption** elemento se utiliza únicamente por los atributos primarios (en otras palabras, el valor de la [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento de la **DimensionAttribute** primario elemento está establecido en *primario*) para determinar el título de los miembros de datos del atributo primario. Para obtener más información sobre los miembros de datos, vea [Atributos en las jerarquías de elementos primarios y secundarios](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
 Los elementos que corresponden a los elementos primarios de **MembersWithDataCaption** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.AttributeTranslation> y <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento MembersWithData &#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [Tipo de datos AttributeTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
