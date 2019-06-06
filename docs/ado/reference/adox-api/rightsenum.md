---
title: RightsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a34cbd8ee3d274d3b3d45049611ca9cc99fa7758
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718839"
---
# <a name="rightsenum"></a>RightsEnum
Especifica los derechos o permisos para un grupo o usuario en un objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (&H4000)|El usuario o grupo tiene permiso para crear nuevos objetos de este tipo.|  
|**adRightDelete**|65536 (&H10000)|El usuario o grupo tiene permiso para eliminar datos de un objeto. Para objetos tales como **tablas**, el usuario tiene permiso para eliminar los valores de datos de registros.|  
|**adRightDrop**|256 (&H100)|El usuario o grupo tiene permiso para quitar objetos del catálogo. Por ejemplo, **tablas** se pueden eliminar mediante un comando DROP TABLE de SQL.|  
|**adRightExclusive**|512 (&H200)|El usuario o grupo tiene permiso para tener acceso al objeto de forma exclusiva.|  
|**adRightExecute**|536870912 (&H20000000)|El usuario o grupo tiene permiso para ejecutar el objeto.|  
|**adRightFull**|268435456 (&H10000000)|El usuario o grupo tiene todos los permisos en el objeto.|  
|**adRightInsert**|32768 (&H8000)|El usuario o grupo tiene permiso para insertar el objeto. Para objetos tales como **tablas**, el usuario tiene permiso para insertar datos en la tabla.|  
|**adRightMaximumAllowed**|33554432 (&H2000000)|El usuario o grupo tiene el número máximo de permisos permitidos por el proveedor. Permisos específicos dependen del proveedor.|  
|**adRightNone**|0|El usuario o grupo no tiene permisos para el objeto.|  
|**adRightRead**|-2147483648 (&H80000000)|El usuario o grupo tiene permiso para leer el objeto. Para objetos tales como [tablas](../../../ado/reference/adox-api/table-object-adox.md), el usuario tiene permiso para leer los datos en la tabla.|  
|**adRightReadDesign**|1024 (&H400)|El usuario o grupo tiene permiso para leer el diseño para el objeto.|  
|**adRightReadPermissions**|131072 (&H20000)|El usuario o grupo puede ver, pero no cambiar, los permisos específicos para un objeto en el catálogo.|  
|**adRightReference**|8192 (&H2000)|El usuario o grupo tiene permiso para hacer referencia al objeto.|  
|**adRightUpdate**|1073741824 (&H40000000)|El usuario o grupo tiene permiso para actualizar el objeto. Para objetos tales como **tablas**, el usuario tiene permiso para actualizar los datos en la tabla.|  
|**adRightWithGrant**|4096 (&H1000)|El usuario o grupo tiene permiso para conceder permisos en el objeto.|  
|**adRightWriteDesign**|2048 (&H800)|El usuario o grupo tiene permiso para modificar el diseño para el objeto.|  
|**adRightWriteOwner**|524288 (&H80000)|El usuario o grupo tiene permiso para modificar el propietario del objeto.|  
|**adRightWritePermissions**|262144 (&H40000)|El usuario o grupo puede modificar los permisos específicos para un objeto en el catálogo.|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[GetPermissions (método, ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
