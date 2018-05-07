---
title: Tipo de datos ClrAssembly (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1c8b137cdcfd4cadb65fa5ffae195c2cf111d7e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="clrassembly-data-type-assl"></a>Tipo de datos ClrAssembly (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos derivado que representa un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado asociado a un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) o [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento  
  
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
|Tipos de datos base|[Ensamblado](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno (tipo abstracto)|  
|Elementos secundarios|[Archivos](../../../analysis-services/scripting/collections/files-element-assl.md), [PermissionSet](../../../analysis-services/scripting/properties/permissionset-element-assl.md)|  
|Elementos derivados|Vea [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) (colección[Assemblies](../../../analysis-services/scripting/collections/assemblies-element-assl.md) de [Database](../../../analysis-services/scripting/objects/database-element-assl.md) o [Server](../../../analysis-services/scripting/objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El **ClrAssembly** elemento contiene los archivos necesarios para volver a crear un [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado, asociado con una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o con una base de datos en una instancia de [!INCLUDE[ssAS](../../../includes/ssas-md.md)], así como los permisos necesarios para ejecutar el ensamblado.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ClrAssembly>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento File & #40; ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [Tipo de datos ClrAssemblyFile & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [Elemento de datos & #40; ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [Tipo de datos DataBlock & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Elemento Blocks & #40; ASSL & #41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Bloquear elemento & #40; ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [Tipo de datos ComAssembly & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
