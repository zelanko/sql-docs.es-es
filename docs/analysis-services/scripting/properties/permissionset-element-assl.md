---
title: Elemento PermissionSet (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
apiname: PermissionSet Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: PermissionSet
helpviewer_keywords: PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7fcbdd8297d1b5f3083d61f9e2eaa02cad49bf6c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="permissionset-element-assl"></a>Elemento PermissionSet (ASSL)
  Identifica el conjunto de permisos asociado con un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ensamblado de .NET Framework.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Seguridad de*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Seguridad de*|Solo se permite el cálculo interno y el acceso a datos local. *Safe* es el conjunto de permisos más restrictivo. El código que ejecuta un ensamblado con permisos *Safe* no puede tener acceso a recursos externos del sistema, como archivos, la red, variables de entorno o el Registro.|  
|*ExternalAccess*|*Safe*, con la capacidad adicional para tener acceso a recursos externos del sistema, como archivos, redes, variables de entorno y el Registro.|  
|*Sin restricciones*|Unrestricted permite el acceso no restringido de ensamblados a los recursos, tanto dentro como fuera de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El código que se ejecuta desde dentro de un ensamblado *Unrestricted* puede llamarse código no administrado.|  
  
 La enumeración que corresponde a los valores permitidos para **PermissionSet** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PermissionSet>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ComAssembly &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Assemblies, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Elemento de la base de datos &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Elemento Server &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
