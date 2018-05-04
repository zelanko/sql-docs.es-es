---
title: Tipo de datos PerspectiveMeasure (ASSL) | Documentos de Microsoft
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
- PerspectiveMeasure Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PerspectiveMeasure
helpviewer_keywords:
- PerspectiveMeasure data type
ms.assetid: 8622ad67-3dcf-48e2-ad4a-c5f0a086eec3
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c0c80655d52597339d658eb6fdeb754c109e4e27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="perspectivemeasure-data-type-assl"></a>Tipo de datos PerspectiveMeasure (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo que representa información acerca de una medida en un elemento [PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PerspectiveMeasure>  
   <MeasureID>...</MeasureID>  
   <Annotations>...</Annotations>  
</PerspectiveMeasure>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [MeasureID](../../../analysis-services/scripting/properties/measureid-element-assl.md)|  
|Elementos derivados|[Measure](../../../analysis-services/scripting/objects/measure-element-assl.md) (colección[Measures](../../../analysis-services/scripting/collections/measures-element-assl.md) de [PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.PerspectiveMeasure>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
