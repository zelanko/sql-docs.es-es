---
title: Elemento (ASSL) como destino | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Target Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2da603c7ea9fa044147bebe3230afce79c75996c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor esperado de este elemento depende del valor de la [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) elemento para el elemento primario **acción**. En la siguiente tabla se describen los valores esperados de **Target** basados en el valor de **TargetType**.  
  
|Valor TargetType|Valor esperado|  
|----------------------|--------------------|  
|*Cubo*|El nombre de un cubo.|  
|*Celdas*|Una expresión de subcubo.|  
|*Conjunto*|Una expresión de conjunto o el nombre de un conjunto con nombre.<br /><br /> Nota: No se puede usar una instrucción de subselección.|  
|*Jerarquía, HierarchyMembers*|Es el nombre de una jerarquía.|  
|*Dimensión, DimensionMembers*|El nombre de una dimensión.|  
|*Nivel de LevelMembers*|El nombre de un nivel.|  
|*Atributo, AttributeMembers*|El nombre de un atributo.|  
  
 El elemento que corresponde al elemento primario de **destino** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
