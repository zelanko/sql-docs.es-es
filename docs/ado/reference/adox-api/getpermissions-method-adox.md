---
title: GetPermissions (método) (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9a2bbb889bc0277ab01f29896d4f60eebd8236cb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759171"
---
# <a name="getpermissions-method-adox"></a>GetPermissions (método, ADOX)
Devuelve los permisos de un [Grupo](../../../ado/reference/adox-api/group-object-adox.md) o [usuario](../../../ado/reference/adox-api/user-object-adox.md) en un contenedor de objetos o objetos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **tipo Long** que especifica una máscara de caracteres que contiene los permisos que el grupo o el usuario tiene en el objeto. Este valor puede ser una o varias de las constantes [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) .  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 Valor **Variant** que especifica el nombre del objeto para el que se van a establecer los permisos. Establezca *nombre* en un valor nulo si desea obtener los permisos para el contenedor de objetos.  
  
 *Tipodeobjeto*  
 Un valor **Long** que puede ser una de las constantes [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , que especifica el tipo del objeto para el que se van a obtener permisos.  
  
 *ObjectTypeId*  
 Opcional. Valor **Variant** que especifica el GUID de un tipo de objeto de proveedor no definido por la especificación de OLE DB. Este parámetro es necesario si *objecttype* está establecido en **adPermObjProviderSpecific**; de lo contrario, no se utiliza.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos GetPermissions y SetPermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name (propiedad, ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
