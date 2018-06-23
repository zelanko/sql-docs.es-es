---
title: Elemento MemberUniqueNameStyle (ASSL) | Documentos de Microsoft
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
- MemberUniqueNameStyle Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MemberUniqueNameStyle element
ms.assetid: f0771c81-0127-4203-9501-ae4f864730fa
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ca327bceaddce4c0f7ac1b7a726d321a02cdffc1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200219"
---
# <a name="memberuniquenamestyle-element-assl"></a>Elemento MemberUniqueNameStyle (ASSL)
  Determina cómo únicos nombres se generan para los miembros de las jerarquías contenidas en el [CubeDimension](../data-type/dimension-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeDimension>  
   ...  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Nativo*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[CubeDimension](../data-type/dimension-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Nativo*|La instancia determina automáticamente los nombres únicos de los miembros.|  
|*NamePath*|La instancia genera un nombre compuesto formado por cada nivel y el título del miembro.|  
  
## <a name="remarks"></a>Notas  
 El elemento que corresponde al elemento primario de `MemberUniqueNameStyle` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento de dimensión &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [Tipo de datos CubeDimension &#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)  
  
  