---
title: Elemento PermissionSet (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2299f76822ae24eb2fee1085fc49836704ba275a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038839"
---
# <a name="permissionset-element-assl"></a>Elemento PermissionSet (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Valor predeterminado|*Seguro*|  
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
|*Seguro*|Solo se permite el cálculo interno y el acceso a datos local. *Safe* es el conjunto de permisos más restrictivo. El código que ejecuta un ensamblado con permisos *Safe* no puede tener acceso a recursos externos del sistema, como archivos, la red, variables de entorno o el Registro.|  
|*ExternalAccess*|*Safe*, con la capacidad adicional para tener acceso a recursos externos del sistema, como archivos, redes, variables de entorno y el Registro.|  
|*Sin restricciones*|Unrestricted permite el acceso no restringido de ensamblados a los recursos, tanto dentro como fuera de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El código que se ejecuta desde dentro de un ensamblado *Unrestricted* puede llamarse código no administrado.|  
  
 La enumeración que corresponde a los valores permitidos para **PermissionSet** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PermissionSet>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ComAssembly & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Elemento Assemblies &#40;ASSL&#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Elemento de la base de datos &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Elemento Server & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
