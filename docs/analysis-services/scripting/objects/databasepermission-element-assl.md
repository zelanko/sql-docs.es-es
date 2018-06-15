---
title: Elemento DatabasePermission (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 855c632b78beb3a5ba75ff7acf31b72fff229e95
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035176"
---
# <a name="databasepermission-element-assl"></a>Elemento DatabasePermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define los permisos predeterminados en un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) (elemento) para un determinado [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DatabasePermissions>  
      <DatabasePermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <Administer>...</Administer>  
...</DatabasePermission>  
</DatabasePermissions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Permiso](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Valor predeterminado|False|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DatabasePermissions](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|  
|Elementos secundarios|[Administrar](../../../analysis-services/scripting/properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Los objetos**DatabasePermission** solo pueden existir para los roles que pertenecen a la base de datos y solo puede existir un objeto **DatabasePermission** para cualquier rol.  
  
 Este elemento tiene las validaciones siguientes en el valor 2 (modelos tabulares) de DeploymentMode.  
  
-   El valor predeterminado del atributo de*Administer* se establece en **False**, salvo cuando el usuario dispone de privilegios de administrador. Para los usuarios con privilegios de administrador, el valor del atributo se establece en **True**.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento role & #40; ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
