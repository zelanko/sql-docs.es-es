---
title: Tipo de datos ComAssembly (ASSL) | Documentos de Microsoft
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
- ComAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ComAssembly
helpviewer_keywords:
- ComAssembly data type
ms.assetid: 23c0f4b3-b6ac-4ec8-9254-74d2f84f5244
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bfe3a7791d02d97b4283b63a1aedd3b6702fe563
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201019"
---
# <a name="comassembly-data-type-assl"></a>Tipo de datos ComAssembly (ASSL)
  Define un tipo de datos derivado que representa una biblioteca COM asociada con un [Server](../objects/server-element-assl.md) o [base de datos](../objects/database-element-assl.md) elemento.  
  
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
|Tipos de datos base|[ensamblado](../objects/assembly-element-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Source](../properties/source-element-comassembly-assl.md)|  
|Elementos derivados|Vea [ensamblado](../objects/assembly-element-assl.md) ([ensamblados](../collections/assemblies-element-assl.md) colección de [base de datos](../objects/database-element-assl.md) o [Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El `ComAssembly` elemento contiene una referencia (el nombre de archivo completo o el identificador de programación) a una biblioteca COM asociada con una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o con una base de datos en una instancia de [!INCLUDE[ssAS](../../../includes/ssas-md.md)].  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ComAssembly>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ClrAssembly &#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  