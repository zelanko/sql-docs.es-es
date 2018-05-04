---
title: Tipo de datos StandardAction (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
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
ms.openlocfilehash: 037414a59f9fa828f67da2a6706d0c4acfa4db6a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="standardaction-data-type-assl"></a>Tipo de datos StandardAction (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos derivado que representa cualquier elemento [Action](../../../analysis-services/scripting/objects/action-element-assl.md) distinto del elemento [DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md) o del elemento [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) .  
  
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
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
