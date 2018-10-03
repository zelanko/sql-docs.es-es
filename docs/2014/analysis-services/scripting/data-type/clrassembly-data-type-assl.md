---
title: Tipo de datos ClrAssembly (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ClrAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssembly
helpviewer_keywords:
- ClrAssembly data type
ms.assetid: 3f5dc5a1-ebd6-41b8-ac04-91d4de137eb4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9171832bac6653e7c1d86915ae006c65022668a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159255"
---
# <a name="clrassembly-data-type-assl"></a>Tipo de datos ClrAssembly (ASSL)
  Define un tipo de datos derivado que representa un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado asociado con un [base de datos](../objects/database-element-assl.md) o [Server](../objects/server-element-assl.md) elemento  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ClrAssembly>  
      <!-- The following elements extend Assembly -->  
   <Files>...</Files>  
      <PermissionSet>...</PermissionSet>  
</ClrAssembly>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[ensamblado](../objects/assembly-element-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno (tipo abstracto)|  
|Elementos secundarios|[Archivos](../collections/files-element-assl.md), [PermissionSet](../properties/permissionset-element-assl.md)|  
|Elementos derivados|Consulte [ensamblado](../objects/assembly-element-assl.md) ([ensamblados](../collections/assemblies-element-assl.md) colección de [base de datos](../objects/database-element-assl.md) o [Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El `ClrAssembly` elemento contiene los archivos necesarios para volver a crear un [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado, asociado con una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o con una base de datos en una instancia de [!INCLUDE[ssAS](../../../includes/ssas-md.md)], así como el permisos necesarios para ejecutar el ensamblado.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ClrAssembly>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento file &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Tipo de datos ClrAssemblyFile &#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)   
 [Elemento de datos &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [Tipo de datos DataBlock &#40;ASSL&#41;](datablock-data-type-assl.md)   
 [Bloquea el elemento &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Bloquear elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Tipo de datos ComAssembly &#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
