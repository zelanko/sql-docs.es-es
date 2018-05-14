---
title: Elemento FoldingParameters (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 51a035c923f1598147c36e4b0860b5ab233577de
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="foldingparameters-element-assl"></a>Elemento FoldingParameters (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
 Para obtener información acerca de cómo realizar la validación cruzada mediante [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] los procedimientos almacenados, vea [procedimientos almacenados minería de datos &#40;Analysis Services: minería de datos&#41;](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
