---
title: GetObjectOwner (método, ADOX) | Documentos de Microsoft
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
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06f3cb14603c7799e7084af407df437b12be4769
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285924"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner (método, ADOX)
Devuelve el propietario de un objeto en un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **cadena** valor que especifica la [nombre](../../../ado/reference/adox-api/name-property-adox.md) de la [usuario](../../../ado/reference/adox-api/user-object-adox.md) o [grupo](../../../ado/reference/adox-api/group-object-adox.md) que posee el objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *ObjectName*  
 A **cadena** valor que especifica el nombre del objeto para el que se va a devolver el propietario.  
  
 *ObjectType*  
 A **largo** valor que puede ser uno de los [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica el tipo de objeto para el que se va a obtener el propietario.  
  
 *Valor de ObjectTypeId*  
 Opcional. A **Variant** valor que especifica el GUID de un tipo de objeto de proveedor no definido por la especificación de OLE DB. Este parámetro es obligatorio si *ObjectType* está establecido en **adPermObjProviderSpecific**; en caso contrario, no se utiliza.  
  
## <a name="remarks"></a>Notas  
 Si el proveedor no admite devolver los propietarios de objetos, se producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo GetObjectOwner y SetObjectOwner métodos (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner (método)](../../../ado/reference/adox-api/setobjectowner-method.md)
