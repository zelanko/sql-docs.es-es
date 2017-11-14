---
title: ObjectTypeEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8eb88d7f3df60d8c54782d20af73e3fd5e917db3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Especifica el tipo de objeto de base de datos para el que se establecerán permisos o propiedad.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|El objeto es una columna.|  
|**adPermObjDatabase**|3|El objeto es una base de datos.|  
|**adPermObjProcedure**|4|El objeto es un procedimiento.|  
|**adPermObjProviderSpecific**|-1|El objeto es un tipo definido por el proveedor. Se producirá un error si la *ObjectType* parámetro es **adPermObjProviderSpecific** y *valor de ObjectTypeId* no se proporciona.|  
|**adPermObjTable**|1|El objeto es una tabla.|  
|**adPermObjView**|5|El objeto es una vista.|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[GetObjectOwner (método, ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions (método, ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner (método)](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|

