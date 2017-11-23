---
title: Elemento CaseCubeDimensionID (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CaseCubeDimensionID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CaseCubeDimensionID
helpviewer_keywords: CaseCubeDimensionID element
ms.assetid: 96720e13-7f9b-4768-ad4b-4def40758707
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 836a033ae3ac296e3138f018900253718dc7c3bc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="casecubedimensionid-element-assl"></a>Elemento CaseCubeDimensionID (ASSL)
  Contiene el identificador (Id.) de la dimensión de cubo que relaciona la dimensión de la minería de datos con el grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataMiningMeasureGroupDimension>  
   ...  
   <CaseCubeDimensionID>...</CaseCubeDimensionID>  
   ...  
</DataMiningMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Miningmeasuregroupdimension](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que corresponde al elemento primario de **CaseCubeDimensionID** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DataMiningMeasureGroupDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
