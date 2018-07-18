---
title: (ASSL) del elemento Target | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 98ec5c729f5735343f5eaa87e5232fcfb138cf38
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045783"
---
# <a name="target-element-assl"></a>Elemento Target (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica el destino de la [acción](../../../analysis-services/scripting/objects/action-element-assl.md) elemento.  
  
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
|Elemento primario|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor esperado de este elemento depende del valor de la [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) (elemento) para el elemento primario **acción**. En la siguiente tabla se describen los valores esperados de **Target** basados en el valor de **TargetType**.  
  
|Valor TargetType|Valor esperado|  
|----------------------|--------------------|  
|*Cubo*|El nombre de un cubo.|  
|*Celdas*|Una expresión de subcubo.|  
|*Conjunto*|Una expresión de conjunto o el nombre de un conjunto con nombre.<br /><br /> Nota: No se puede usar una instrucción de subselección.|  
|*Jerarquía, HierarchyMembers*|Es el nombre de una jerarquía.|  
|*Dimensión, DimensionMembers*|El nombre de una dimensión.|  
|*Nivel de LevelMembers*|El nombre de un nivel.|  
|*Atributo, AttributeMembers*|El nombre de un atributo.|  
  
 El elemento que se corresponde con el elemento primario de **destino** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
