---
title: (ASSL) del elemento Target | Microsoft Docs
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
- Target Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec2f4a43b8b03e2f28d4bd8c61a9c6e4a9d20eb5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180772"
---
# <a name="target-element-assl"></a>Elemento Target (ASSL)
  Identifica el destino de la [acción](../objects/action-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
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
|Elemento primario|[Acción](../objects/action-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor esperado de este elemento depende del valor de la [TargetType](targettype-element-assl.md) (elemento) para el elemento primario `Action`. En la siguiente tabla se describen los valores esperados de `Target` basados en el valor de `TargetType`.  
  
|Valor TargetType|Valor esperado|  
|----------------------|--------------------|  
|*Cubo*|El nombre de un cubo.|  
|*Celdas*|Una expresión de subcubo.|  
|*Conjunto*|Una expresión de conjunto o el nombre de un conjunto con nombre. **Nota:** no se puede usar una instrucción de subselección.|  
|*Jerarquía, HierarchyMembers*|Es el nombre de una jerarquía.|  
|*Dimensión, DimensionMembers*|El nombre de una dimensión.|  
|*Nivel de LevelMembers*|El nombre de un nivel.|  
|*Atributo, AttributeMembers*|El nombre de un atributo.|  
  
 El elemento que se corresponde con el elemento primario de `Target` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
