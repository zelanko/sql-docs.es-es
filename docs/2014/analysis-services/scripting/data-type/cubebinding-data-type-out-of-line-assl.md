---
title: Tipo de datos CubeBinding (fuera de línea) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee354905f21670a143d8ec711bb45495086dbf05
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136658"
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>Tipo de datos CubeBinding (fuera de línea) (ASSL)
  Define un tipo de datos primitivo que representa la relación entre un [cubo](../objects/cube-element-assl.md) elemento y un [DataSource](../objects/datasource-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeBinding>  
   <ID>...</ID>  
   <DataSourceID>...</DataSourceID>  
   <DataSource>...</DataSource>  
   <MeasureGroup>...</MeasureGroup>  
</CubeBinding>  
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
|Elementos secundarios|[Origen de datos](../objects/datasource-element-assl.md), [DataSourceID](../properties/id-element-assl.md), [ID](../properties/id-element-assl.md), [MeasureGroup](../objects/group-element-assl.md)|  
|Elementos derivados|[Enlace](../../xmla/xml-elements-properties/binding-element-xmla.md) ([enlaces](../../xmla/xml-elements-properties/bindings-element-xmla.md) colección de [proceso](../../xmla/xml-elements-commands/process-element-xmla.md) o [Batch](../../xmla/xml-elements-commands/batch-element-xmla.md) comandos)|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información sobre los enlaces fuera de línea, consulte [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos Binding &#40;ASSL&#41;](binding-data-type-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
