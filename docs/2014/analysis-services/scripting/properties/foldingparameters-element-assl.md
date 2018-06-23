---
title: Elemento FoldingParameters (ASSL) | Documentos de Microsoft
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
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 12cae8f4ad02f57f63fd168ff41503f233f53c4c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203759"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
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
  
## <a name="remarks"></a>Notas  
 Estas propiedades solo son para uso interno y no se pueden usar en instrucciones DDL.  
  
 Para obtener información sobre cómo usar la validación cruzada en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], consulte [medidas en el informe de validación cruzada](../../data-mining/measures-in-the-cross-validation-report.md).  
  
 Para obtener información acerca de cómo realizar la validación cruzada mediante [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] los procedimientos almacenados, vea [procedimientos almacenados minería de datos &#40;Analysis Services: minería de datos&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
