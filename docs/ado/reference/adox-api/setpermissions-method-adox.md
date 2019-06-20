---
title: SetPermissions (método, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcc44037ac746621c044bca755fd9b957356dc38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705794"
---
# <a name="setpermissions-method-adox"></a>SetPermissions (método, ADOX)
Especifica los permisos para un [grupo](../../../ado/reference/adox-api/group-object-adox.md) o [usuario](../../../ado/reference/adox-api/user-object-adox.md) en un objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Name*  
 Un **cadena** valor que especifica el nombre del objeto que se va a establecer permisos.  
  
 *ObjectType*  
 Un **largo** valor puede ser uno de los [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica el tipo del objeto que se va a obtener los permisos.  
  
 *Acción*  
 Un **largo** valor puede ser uno de los [ActionEnum](../../../ado/reference/adox-api/actionenum.md) constantes que especifica el tipo de acción que se realizará al establecer los permisos.  
  
 *Derechos*  
 Un **largo** valor que puede ser una máscara de bits de uno o varios de los [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) constantes, que indica los derechos a establecer.  
  
 *Heredar*  
 Opcional. Un **largo** valor puede ser uno de los [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) constantes, que especifica cómo los objetos heredará estos permisos. El valor predeterminado es **adInheritNone**.  
  
 *ObjectTypeId*  
 Opcional. Un **Variant** valor que especifica el GUID para un tipo de objeto de proveedor que no se define mediante la especificación de OLE DB. Este parámetro es obligatorio si *ObjectType* está establecido en **adPermObjProviderSpecific**; en caso contrario, no se utiliza.  
  
## <a name="remarks"></a>Comentarios  
 Se producirá un error si el proveedor no admite la configuración de derechos de acceso para grupos o usuarios.  
  
> [!NOTE]
>  Al llamar a **SetPermissions**, la configuración de acciones **adAccessRevoke** invalida cualquier configuración de la *derechos* parámetro. No establezca *acciones* a **adAccessRevoke** si desea que los derechos especificados en el *derechos* parámetro surta efecto.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [GetPermissions y SetPermissions métodos ejemplo (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions (método, ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name (propiedad, ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
