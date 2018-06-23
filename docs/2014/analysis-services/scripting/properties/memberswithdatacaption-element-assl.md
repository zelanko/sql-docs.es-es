---
title: Elemento MembersWithDataCaption (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MembersWithDataCaption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ef845a4c77a66ad1c59a0bdad527856a86849de9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111647"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AttributeTranslation](../data-type/translation-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de la `MembersWithDataCaption` elemento se utiliza únicamente por los atributos primarios (en otras palabras, el valor de la [uso](usage-element-dimensionattribute-assl.md) elemento de la `DimensionAttribute` elemento primario se establece en *primario*) para determinar la título de miembros de datos del atributo primario. Para obtener más información sobre los miembros de datos, vea [Atributos en las jerarquías de elementos primarios y secundarios](../../multidimensional-models/parent-child-dimension-attributes.md).  
  
 Los elementos que corresponden a los elementos primarios de `MembersWithDataCaption` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.AttributeTranslation> y <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento MembersWithData &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [Tipo de datos AttributeTranslation &#40;ASSL&#41;](../data-type/translation-data-type-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  