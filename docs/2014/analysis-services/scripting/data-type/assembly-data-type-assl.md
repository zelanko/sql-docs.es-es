---
title: Tipo de datos Assembly (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Assembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Assembly data type
ms.assetid: 0a381322-9509-4579-a754-c6cdd0a70cc9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb02963baa8a7fca296abe89801d89c1f7ea19fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209654"
---
# <a name="assembly-data-type-assl"></a>Tipo de datos Assembly (ASSL)
  Define un tipo de datos primitivo abstracto que representa un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado o una biblioteca de vínculos dinámicos COM (DLL) asociada con un [Server](../objects/server-element-assl.md) o [base de datos](../objects/database-element-assl.md) elemento.  
  
> [!IMPORTANT]  
>  Los ensamblados COM pueden suponer un riesgo para la seguridad. Debido a esto y a otras consideraciones, los ensamblados COM están en desuso en [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]. Es posible que este tipo de ensamblados no esté disponible en versiones futuras.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Assembly>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Annotations>...</Annotations>  
</Assembly>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|[ClrAssembly](assembly-data-type-assl.md), [ComAssembly](comassembly-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descripción](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [ImpersonationInfo](../properties/impersonationinfo-element-assl.md), [ LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [nombre](../properties/name-element-assl.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentarios  
 El tipo de datos `Assembly` actúa como el tipo de datos base para el elemento `ComAssembly`, que representa las bibliotecas COM asociadas a la instancia o base de datos y el elemento `ClrAssembly`, que representa los ensamblados [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] asociados a la instancia o base de datos. Para obtener más información acerca de los ensamblados, vea [administración de los ensamblados de modelos multidimensionales](../../multidimensional-models/multidimensional-model-assemblies-management.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Assembly>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Server &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Elemento de la base de datos &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
