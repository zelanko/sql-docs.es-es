---
title: Elemento AggregationUsage (ASSL) | Microsoft Docs
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
- AggregationUsage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationUsage
helpviewer_keywords:
- AggregationUsage element
ms.assetid: af0c2e7f-b659-4fbf-9b1a-66128db669a2
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a073ca27168bec785d9098d9e6b3ad4974b7018
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259471"
---
# <a name="aggregationusage-element-assl"></a>Elemento AggregationUsage (ASSL)
  Controles de cómo el Diseñador de agregaciones de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] diseña las agregaciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeAttribute>  
   ...  
   <AggregationUsage>...</AggregationUsage>  
   ...  
</CubeAttribute>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Valor de DB-Library*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[CubeAttribute](../data-type/cubeattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Completa*|Todas las agregaciones del cubo deben incluir este atributo.|  
|*Ninguno*|Ninguna agregación del cubo debe incluir este atributo.|  
|*Sin restricciones*|No se aplica ninguna restricción en el Diseñador de agregaciones.|  
|*Valor de DB-Library*|El Diseñador de agregaciones aplica una regla predeterminada basada en el tipo de atributo (*Full* para las claves, *Unrestricted* para los demás elementos).|  
  
 La enumeración que corresponde a los valores permitidos para `AggregationUsage` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.AggregationUsage>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
