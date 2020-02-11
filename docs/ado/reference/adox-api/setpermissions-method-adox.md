---
title: SetPermissions (método) (ADOX) | Microsoft Docs
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
ms.openlocfilehash: 50a609d0cebe70ea5127ed448e57a70881e35097
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965225"
---
# <a name="setpermissions-method-adox"></a>SetPermissions (método, ADOX)
Especifica los permisos para un [Grupo](../../../ado/reference/adox-api/group-object-adox.md) o [usuario](../../../ado/reference/adox-api/user-object-adox.md) en un objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 Valor de **cadena** que especifica el nombre del objeto para el que se van a establecer los permisos.  
  
 *Tipodeobjeto*  
 Un valor **Long** que puede ser una de las constantes [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , que especifica el tipo del objeto para el que se van a obtener permisos.  
  
 *Acción*  
 Un valor **Long** que puede ser una de las constantes [ActionEnum](../../../ado/reference/adox-api/actionenum.md) que especifica el tipo de acción que se debe realizar al establecer los permisos.  
  
 *Necesarios*  
 Un valor **largo** que puede ser una máscara de máscara de una o varias de las constantes [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) , que indica los derechos que se van a establecer.  
  
 *Adopta*  
 Opcional. Un valor **Long** que puede ser una de las constantes de [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) , que especifica cómo heredarán estos permisos los objetos. El valor predeterminado es **adInheritNone**.  
  
 *ObjectTypeId*  
 Opcional. Valor **Variant** que especifica el GUID de un tipo de objeto de proveedor que no está definido por la especificación OLE DB. Este parámetro es necesario si *objecttype* está establecido en **adPermObjProviderSpecific**; de lo contrario, no se utiliza.  
  
## <a name="remarks"></a>Observaciones  
 Se producirá un error si el proveedor no admite la configuración de derechos de acceso para grupos o usuarios.  
  
> [!NOTE]
>  Al llamar a **SetPermissions**, al establecer Actions en **adAccessRevoke** se invalida cualquier configuración del parámetro *Rights* . No establezca *acciones* en **adAccessRevoke** si quiere que los derechos especificados en el parámetro *Rights* surtan efecto.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos GetPermissions y SetPermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions (método) (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name (propiedad, ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
