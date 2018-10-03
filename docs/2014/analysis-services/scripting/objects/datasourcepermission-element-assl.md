---
title: Elemento DataSourcePermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSourcePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSourcePermission element
ms.assetid: 6dc6fb13-034e-479a-902e-27f3fb78c33f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4130cd2a0eb83b32c8bcdf703d10ca6305af619
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087625"
---
# <a name="datasourcepermission-element-assl"></a>Elemento DataSourcePermission (ASSL)
  Define los permisos predeterminados en un [DataSource](../data-type/datasource-data-type-assl.md) tipo de datos para un determinado [rol](role-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataSourcePermissions>  
   <DataSourcePermission xsi:type="Permission">  
      <!-- No child elements other than those from Permission are defined -->  
...</DataSourcePermission>  
</DataSourcePermissions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Permiso](../data-type/permission-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: Elemento opcional que puede aparecer una vez o más.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DataSourcePermissions](../collections/datasourcepermissions-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Los objetos `DataSourcePermission` solo pueden existir para los roles que pertenecen a la base de datos y solo puede existir un objeto `DataSourcePermission` para cualquier rol.  
  
## <a name="see-also"></a>Vea también  
 [Elemento role &#40;ASSL&#41;](role-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
