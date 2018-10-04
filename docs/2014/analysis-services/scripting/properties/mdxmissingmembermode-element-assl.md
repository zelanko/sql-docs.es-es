---
title: Elemento MdxMissingMemberMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MdxMissingMemberMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MdxMissingMemberMode element
ms.assetid: aca6130b-5fb8-4fa1-af8b-8e1ef361926f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c942587601c5e62d9e876be8eb1277f638eaa7ef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126746"
---
# <a name="mdxmissingmembermode-element-assl"></a>Elemento MdxMissingMemberMode (ASSL)
  Determina cómo se gestionan los miembros que faltan en las instrucciones MDX (Expresiones multidimensionales).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension>  
   ...  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Valor de DB-Library*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Dimension](../data-type/dimension-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Pasar por alto*|Se omiten los miembros que faltan.|  
|*Error*|Se produce un error si se detecta que faltan miembros.|  
|*Valor de DB-Library*|Se omiten los miembros que faltan.|  
  
 El elemento que se corresponde con el elemento primario de `MdxMissingMemberMode` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones multidimensionales &#40;MDX&#41; referencia](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
