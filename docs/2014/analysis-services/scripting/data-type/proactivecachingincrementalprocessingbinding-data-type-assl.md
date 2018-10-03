---
title: Tipo de datos ProactiveCachingIncrementalProcessingBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCachingIncrementalProcessingBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingIncrementalProcessingBinding data type
ms.assetid: f49c0c96-4277-417b-9660-d77a4faebd00
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3abbeafe4bb3a6d9cc3a9a35e4a77b6fede11f46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216405"
---
# <a name="proactivecachingincrementalprocessingbinding-data-type-assl"></a>Tipo de datos ProactiveCachingIncrementalProcessingBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace a la [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre el estado del proceso de regeneración de la memoria caché.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProactiveCachingIncrementalProcessingBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <RefreshInterval>...</ RefreshInterval >  
   <IncrementalProcessingNotification>...</ IncrementalProcessingNotification >  
</ProactiveCachingIncrementalProcessingBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[ProactiveCachingBinding](binding-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md), [RefreshInterval](../properties/refreshinterval-element-assl.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información sobre la `ProactiveCachingBinding` tipo, incluida una tabla de la jerarquía de herencia de `ProactiveCachingBinding` tipos, vea [tipo de datos ProactiveCachingBinding &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, vea [tipo de enlace de datos &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para obtener información general de los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ProactiveCachingIncrementalProcessingBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
