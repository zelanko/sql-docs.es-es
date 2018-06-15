---
title: GetPermissions (método, ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55a5d4f9096d5a75855d4b612a202afd034b11da
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286044"
---
# <a name="getpermissions-method-adox"></a>GetPermissions (método, ADOX)
Devuelve los permisos para un [grupo](../../../ado/reference/adox-api/group-object-adox.md) o [usuario](../../../ado/reference/adox-api/user-object-adox.md) en un objeto o un contenedor de objetos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que especifica una máscara de bits que contiene los permisos que tenga el grupo o usuario en el objeto. Este valor puede ser uno o varios de los [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) constantes.  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 A **Variant** valor que especifica el nombre del objeto para el que se va a establecer permisos. Establecer *nombre* en un valor nulo si desea obtener los permisos para el contenedor de objetos.  
  
 *ObjectType*  
 A **largo** valor que puede ser uno de los [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica el tipo del objeto para el que se va a obtener permisos.  
  
 *Valor de ObjectTypeId*  
 Opcional. A **Variant** valor que especifica el GUID de un tipo de objeto de proveedor no definido por la especificación de OLE DB. Este parámetro es obligatorio si *ObjectType* está establecido en **adPermObjProviderSpecific**; en caso contrario, no se utiliza.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo GetPermissions y SetPermissions métodos (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name (propiedad, ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
