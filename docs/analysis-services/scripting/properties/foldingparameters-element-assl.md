---
title: Elemento FoldingParameters (ASSL) | Documentos de Microsoft
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
apitype: Schema
applies_to:
- SQL Server 2016 Preview
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
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8f6fa2a178bc1d8f9722a101d7305cedfa248663
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="foldingparameters-element-assl"></a>Elemento FoldingParameters (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Especifica los parámetros utilizados por la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidor mientras se realiza la validación cruzada de modelos de minería de datos.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|*FoldIndex*|Número entero que indica la posición inicial de la partición que se utiliza para la validación cruzada.|  
|*FoldCount*|Número entero que indica el número de particiones en el modelo después de la validación cruzada.|  
|*MaxCases*|Número entero que indica cuántos casos del modelo se utilizan para la validación cruzada.<br /><br /> El valor 0 indica que se utilizan todos los casos.|  
|*FoldTargetAttribute*|Cadena que indica el identificador de la columna de modelo que contiene el atributo de predicción.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Elementos secundarios|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>Comentarios  
 Estas propiedades solo son para uso interno y no se pueden usar en instrucciones DDL.  
  
 Para obtener información sobre cómo usar la validación cruzada en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], consulte [medidas en el informe de validación cruzada](../../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
 Para obtener información acerca de cómo realizar la validación cruzada mediante [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] los procedimientos almacenados, vea [procedimientos almacenados minería de datos &#40; Analysis Services: minería de datos &#41; ](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
