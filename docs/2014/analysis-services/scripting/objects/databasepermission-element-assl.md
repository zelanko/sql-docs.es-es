---
title: Elemento DatabasePermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DatabasePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a904f12b86d6449c11f354a790503dc1bd93ffbe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106665"
---
# <a name="databasepermission-element-assl"></a>Elemento DatabasePermission (ASSL)
  Define los permisos predeterminados en un [base de datos](database-element-assl.md) (elemento) para un determinado [rol](role-element-assl.md) elemento.  
  
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
|Tipo y longitud de los datos|[Permiso](../data-type/permission-data-type-assl.md)|  
|Valor predeterminado|False|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DatabasePermissions](../collections/databasepermissions-element-assl.md)|  
|Elementos secundarios|[Administrar](../properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Los objetos `DatabasePermission` solo pueden existir para los roles que pertenecen a la base de datos y solo puede existir un objeto `DatabasePermission` para cualquier rol.  
  
 Este elemento tiene las validaciones siguientes en el valor 2 (modelos tabulares) de DeploymentMode.  
  
-   *Administrar* valor predeterminado del atributo se establece en `False`, excepto cuando el usuario tiene privilegios administrativos. Para los usuarios con privilegios de administrador, el valor del atributo se establece en `True`.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento role &#40;ASSL&#41;](role-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
