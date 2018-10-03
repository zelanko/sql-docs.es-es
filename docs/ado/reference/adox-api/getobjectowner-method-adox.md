---
title: GetObjectOwner (método, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b2c967ac293ed59fde6494e12c2afc2c5b6de90
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687213"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner (método, ADOX)
Devuelve el propietario de un objeto en un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **cadena** valor que especifica el [nombre](../../../ado/reference/adox-api/name-property-adox.md) de la [usuario](../../../ado/reference/adox-api/user-object-adox.md) o [grupo](../../../ado/reference/adox-api/group-object-adox.md) que posee el objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *ObjectName*  
 Un **cadena** valor que especifica el nombre del objeto que se va a devolver el propietario.  
  
 *ObjectType*  
 Un **largo** valor puede ser uno de los [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica el tipo del objeto que se va a obtener el propietario.  
  
 *Valor de ObjectTypeId*  
 Opcional. Un **Variant** valor que especifica el GUID para un tipo de objeto de proveedor no definido por la especificación de OLE DB. Este parámetro es obligatorio si *ObjectType* está establecido en **adPermObjProviderSpecific**; en caso contrario, no se utiliza.  
  
## <a name="remarks"></a>Comentarios  
 Si el proveedor no admite devolver los propietarios de objetos, se producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [GetObjectOwner y SetObjectOwner métodos (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner (método)](../../../ado/reference/adox-api/setobjectowner-method.md)
