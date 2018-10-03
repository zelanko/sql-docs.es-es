---
title: Tipo de datos MeasureGroupHierarchy (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupHierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupHierarchy
helpviewer_keywords:
- MeasureGroupHierarchy data type
ms.assetid: 63c2fd97-d7ad-4715-8c49-24d684bc92d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d2dafbeb5f423836c444490c21134cc64a402e6c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133355"
---
# <a name="measuregrouphierarchy-data-type-assl"></a>Tipo de datos MeasureGroupHierarchy (ASSL)
  Define un tipo de datos primitivo que representa información acerca de una jerarquía de un grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroupHierarchy>  
   <HierarchyID>...</HierarchyID>  
      <Annotations>...</Annotations>  
</MeasureGroupHierarchy>  
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
|Elementos secundarios|[Annotations](../collections/annotations-element-assl.md), [HierarchyID](../properties/id-element-assl.md)|  
|Elementos derivados|[Hierarchy](../objects/hierarchy-element-assl.md) (colección[Hierarchies](../collections/hierarchies-element-assl.md) de [RegularMeasureGroupDimension](dimension-data-type-assl.md))|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
