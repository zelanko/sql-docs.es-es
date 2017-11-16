---
title: Elemento MembersWithDataCaption (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f254c1fb3c747a64e3e8e5df50bf30d532678d09
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="memberswithdatacaption-element-assl"></a>Elemento MembersWithDataCaption (ASSL)
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
 [MembersWithData, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [Tipo de datos AttributeTranslation &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

