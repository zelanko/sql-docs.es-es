---
title: Tipo de datos PerspectiveMeasureGroup (ASSL) | Microsoft Docs
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
- PerspectiveMeasureGroup Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveMeasureGroup
helpviewer_keywords:
- PerspectiveMeasureGroup data type
ms.assetid: 5927120d-f30e-4f87-8523-6d17012817d7
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da4817ba23f7e4be50eb11aa97a3163e48536425
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154956"
---
# <a name="perspectivemeasuregroup-data-type-assl"></a>Tipo de datos PerspectiveMeasureGroup (ASSL)
  Define un tipo de datos primitivo que representa información sobre un grupo de medida en un [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PerspectiveMeasureGroup>  
   <MeasureGroupID>...</MeasureGroupID>  
   <Measures>...</Measures>  
   <Annotations>...</Annotations>  
</PerspectiveMeasureGroup>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [MeasureGroupID](../properties/id-element-assl.md), [medidas](../collections/measures-element-assl.md)|  
|Elementos derivados|[MeasureGroup](../objects/group-element-assl.md) ([MeasureGroups](../collections/groups-element-assl.md) colección de [perspectiva](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 Un grupo de medida en una perspectiva tiene la misma estructura que un grupo de medida en el cubo subyacente.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
