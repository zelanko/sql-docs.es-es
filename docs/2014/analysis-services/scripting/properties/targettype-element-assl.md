---
title: Elemento TargetType (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TargetType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e4a36c4ca0e38fe00990f2185685205840eafc66
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199210"
---
# <a name="targettype-element-assl"></a>Elemento TargetType (ASSL)
  Identifica el tipo de elemento del elemento identificado en el [destino](target-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Acción](../objects/action-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Cubo*|El destino de la acción es un cubo.|  
|*Celdas*|El destino de la acción es un subcubo.|  
|*conjunto*|El destino de la acción es un conjunto.|  
|*Hierarchy*|El destino de la acción es una jerarquía.|  
|*Level*|El destino de la acción es un nivel.|  
|*DimensionMembers*|El destino de la acción es un miembro de una dimensión.|  
|*HierarchyMembers*|El destino de la acción es un miembro de una jerarquía.|  
|*LevelMembers*|El destino de la acción es un miembro de un nivel.|  
|*AttributeMembers*|El destino de la acción es un miembro de un atributo.|  
  
 La enumeración que corresponde a los valores permitidos para `TargetType` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ActionTargetType>.  
  
 El elemento que corresponde al elemento primario de `TargetType` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  