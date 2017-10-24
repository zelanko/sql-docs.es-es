---
title: Tipo de datos ComAssembly (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ComAssembly Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ComAssembly
helpviewer_keywords:
- ComAssembly data type
ms.assetid: 23c0f4b3-b6ac-4ec8-9254-74d2f84f5244
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e519b7f204e5fe258222a48161dc9032ccc826ac
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="comassembly-data-type-assl"></a>Tipo de datos ComAssembly (ASSL)
  Define un tipo de datos derivado que representa una biblioteca COM asociada con un [Server](../../../analysis-services/scripting/objects/server-element-assl.md) o [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
> [!IMPORTANT]  
>  Los ensamblados COM pueden suponer un riesgo para la seguridad. Debido a esto y a otras consideraciones, los ensamblados COM están en desuso en [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]. Es posible que este tipo de ensamblados no esté disponible en versiones futuras.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ComAssembly>  
      <!-- The following elements extend Assembly -->  
   <Source>...</Source>  
</ComAssembly>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Ensamblado](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Source](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|  
|Elementos derivados|Vea [ensamblado](../../../analysis-services/scripting/objects/assembly-element-assl.md) ([ensamblados](../../../analysis-services/scripting/collections/assemblies-element-assl.md) colección de [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) o [Server](../../../analysis-services/scripting/objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El **ComAssembly** elemento contiene una referencia (el nombre de archivo completo o el identificador de programación) a una biblioteca COM asociada con una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o con un valor concreto base de datos en una instancia de [!INCLUDE[ssAS](../../../includes/ssas-md.md)].  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ComAssembly>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ClrAssembly &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

