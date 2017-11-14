---
title: Tipo de datos StandardAction (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
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
apiname:
- StandardAction Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- StandardAction
helpviewer_keywords:
- StandardAction data type
ms.assetid: 81b574d5-06c1-4587-8bd2-0e5c5e3b1d99
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d57cf9ec56c160d49111b3301f11dbed72e383a1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="standardaction-data-type-assl"></a>Tipo de datos StandardAction (ASSL)
  Define un tipo de datos derivado que representa cualquier [acción](../../../analysis-services/scripting/objects/action-element-assl.md) elemento que no sea un [DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md) elemento o un [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<StandardAction>  
   <!-- The following elements extend Action -->  
   <Expression>...</Expression>  
</StandardAction>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Acción](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Expresión](../../../analysis-services/scripting/properties/expression-element-assl.md)|  
|Elementos derivados|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md) ([acciones](../../../analysis-services/scripting/collections/actions-element-assl.md) colección de [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) o [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

