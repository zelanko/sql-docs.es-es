---
title: ObjectTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04c7b1d1cb5d07a300b82d13a7e80158498bbd5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965653"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Especifica el tipo de objeto de base de datos para el que se van a establecer permisos o propiedad.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|El objeto es una columna.|  
|**adPermObjDatabase**|3|El objeto es una base de datos.|  
|**adPermObjProcedure**|4|El objeto es un procedimiento.|  
|**adPermObjProviderSpecific**|-1|El objeto es un tipo definido por el proveedor. Se producirá un error si el parámetro *objecttype* es **adPermObjProviderSpecific** y no se proporciona un *ObjectTypeId* .|  
|**adPermObjTable**|1|El objeto es una tabla.|  
|**adPermObjView**|5|El objeto es una vista.|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[GetObjectOwner (método, ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions (método, ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner (método)](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
