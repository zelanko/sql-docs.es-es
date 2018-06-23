---
title: Elemento RootMemberIf (ASSL) | Documentos de Microsoft
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
- RootMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a923b08efc636d2635d60b00f85c42dc00a312e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107720"
---
# <a name="rootmemberif-element-assl"></a>Elemento RootMemberIf (ASSL)
  Determina cómo se identifican los miembros raíz de un atributo primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <RootMemberIf>...</RootMemberIf>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*ParentIsBlankSelfOrMissing*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de la `RootMemberIf` elemento se utiliza únicamente por los atributos primarios (en otras palabras, el valor de la [uso](usage-element-dimensionattribute-assl.md) elemento de la `DimensionAttribute` elemento primario se establece en *primario*) para determinar la raíz () miembros de nivel superior) de una jerarquía de elementos primarios y secundarios.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|Solo los miembros que cumplen una o varias de las condiciones descritas para *ParentIsBlank*, *ParentIsSelf*, o *ParentIsMissing* se tratan como miembros raíz.|  
|*ParentIsBlank*|Solo los miembros con un valor null, cero o una cadena vacía en las columnas de clave representadas por la [KeyColumns](../collections/columns-element-assl.md) colección de `DimensionAttribute` se tratan como miembros raíz.|  
|*ParentIsSelf*|Únicamente los miembros que son elementos primarios se tratan como miembros raíz.|  
|*ParentIsMissing*|Únicamente los miembros cuyos elementos primarios no se pueden encontrar se tratan como miembros raíz.|  
  
 La enumeración que corresponde a los valores permitidos para `RootMemberIf` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.RootIfValue>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  