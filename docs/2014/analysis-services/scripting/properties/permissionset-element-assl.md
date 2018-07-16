---
title: Elemento PermissionSet (ASSL) | Microsoft Docs
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
- PermissionSet Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 471ef43aea9fadcca7ab8a4a36870a3bdddee22f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263471"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Safe*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Safe*|Solo se permite el cálculo interno y el acceso a datos local. *Safe* es el conjunto de permisos más restrictivo. El código que ejecuta un ensamblado con permisos *Safe* no puede tener acceso a recursos externos del sistema, como archivos, la red, variables de entorno o el Registro.|  
|*ExternalAccess*|*Safe*, con la capacidad adicional para tener acceso a recursos externos del sistema, como archivos, redes, variables de entorno y el Registro.|  
|*Sin restricciones*|Unrestricted permite el acceso no restringido de ensamblados a los recursos, tanto dentro como fuera de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El código que se ejecuta desde dentro de un ensamblado *Unrestricted* puede llamarse código no administrado.|  
  
 La enumeración que corresponde a los valores permitidos para `PermissionSet` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PermissionSet>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ComAssembly &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Elemento Assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Elemento de la base de datos &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Elemento Server &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
