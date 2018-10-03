---
title: Elemento FoldingParameters (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- FoldIndex
- FoldCount
- MaxCases
- FoldingParameters
- FoldTargetAttribute
helpviewer_keywords:
- FoldingParameters element
ms.assetid: 5f5c5a3e-4aed-48fb-bca5-e67f421bef2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f7f32684686f7b8f12bb147bb4f6b7ea87537e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117430"
---
# <a name="foldingparameters-element-assl"></a>Elemento FoldingParameters (ASSL)
  Especifica los parámetros que usa el servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cuando realiza la validación cruzada de los modelos de minería de datos.  
  
> [!NOTE]  
>  Estos parámetros solo son para uso interno. La información proporcionada aquí solo sirve de referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModel>  
   ...  
   <ddl100_100:FoldingParameters>...  
      <ddl100_100:FoldIndex>...</ddl100_100:FoldIndex>  
      <ddl100_100:FoldCount>...</ddl100_100:FoldCount>  
      <ddl100_100:MaxCases>...</ddl100_100:MAxCases>  
      <ddl100_100:FoldTargetAttribute>...</ddl100_100:FoldTargetAttribute  
...</ddl100_100:FoldingParameters>  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|*FoldIndex*|Número entero que indica la posición inicial de la partición que se utiliza para la validación cruzada.|  
|*FoldCount*|Número entero que indica el número de particiones en el modelo después de la validación cruzada.|  
|*MaxCases*|Número entero que indica cuántos casos del modelo se utilizan para la validación cruzada.<br /><br /> El valor 0 indica que se utilizan todos los casos.|  
|*FoldTargetAttribute*|Cadena que indica el identificador de la columna de modelo que contiene el atributo de predicción.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModel](../objects/miningmodel-element-assl.md)|  
|Elementos secundarios|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>Comentarios  
 Estas propiedades solo son para uso interno y no se pueden usar en instrucciones DDL.  
  
 Para obtener información sobre cómo usar la validación cruzada en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], consulte [medidas en el informe de validación cruzada](../../data-mining/measures-in-the-cross-validation-report.md).  
  
 Para obtener información acerca de cómo realizar la validación cruzada mediante el uso de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] los procedimientos almacenados, vea [procedimientos almacenados minería de datos &#40;Analysis Services - minería de datos&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
