---
title: Método GetObjectOwner (ADOX) | Microsoft Docs
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
ms.openlocfilehash: ff85491cf7ca30e3f95526aa7043f321a65cccc5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966271"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner (método, ADOX)
Devuelve el propietario de un objeto de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **cadena** que especifica el [nombre](../../../ado/reference/adox-api/name-property-adox.md) del [usuario](../../../ado/reference/adox-api/user-object-adox.md) o [Grupo](../../../ado/reference/adox-api/group-object-adox.md) al que pertenece el objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *ObjectName*  
 Valor de **cadena** que especifica el nombre del objeto para el que se va a devolver el propietario.  
  
 *Tipodeobjeto*  
 Un valor **Long** que puede ser una de las constantes [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , que especifica el tipo del objeto para el que se va a obtener el propietario.  
  
 *ObjectTypeId*  
 Opcional. Valor **Variant** que especifica el GUID de un tipo de objeto de proveedor no definido por la especificación de OLE DB. Este parámetro es necesario si *objecttype* está establecido en **adPermObjProviderSpecific**; de lo contrario, no se utiliza.  
  
## <a name="remarks"></a>Observaciones  
 Se producirá un error si el proveedor no admite la devolución de propietarios de objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos GetObjectOwner y SetObjectOwner (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner (método)](../../../ado/reference/adox-api/setobjectowner-method.md)
