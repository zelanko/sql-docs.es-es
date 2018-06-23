---
title: Tipo de datos DegenerateMeasureGroupDimension (ASSL) | Documentos de Microsoft
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
- DegenerateMeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DegenerateMeasureGroupDimension
helpviewer_keywords:
- DegenerateMeasureGroupDimension data type
ms.assetid: a64fe908-154d-4fea-b435-afb6ee37a6fa
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 45a3d778580c344e0251e271415ff729b61520b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106630"
---
# <a name="degeneratemeasuregroupdimension-data-type-assl"></a>Tipo de datos DegenerateMeasureGroupDimension (ASSL)
  Define un tipo de datos derivado que representa la relación entre una dimensión degenerada (es decir, una dimensión de hechos) y un grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DegenerateMeasureGroupDimension>  
   <!-- DegenerateMeasureGroupDimension does not have any elements that extend RegularMeasureGroupDimension -->  
</DegenerateMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[RegularMeasureGroupDimension](dimension-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|None|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información acerca de las dimensiones de hechos, vea [las relaciones entre dimensiones](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DegenerateMeasureGroupDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  