---
title: "Método SetObjectOwner | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33226468d9d1f556d2cf7ec3edac37375b0c8d84
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setobjectowner-method"></a>SetObjectOwner (método)
Especifica el propietario de un objeto en un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ObjectName*  
 A **cadena** valor que especifica el nombre del objeto para el que se especifique el propietario.  
  
 *ObjectType*  
 A **largo** valor que puede ser uno de los [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes que especifica el tipo de propietario.  
  
 *OwnerName*  
 A **cadena** valor que especifica la [nombre](../../../ado/reference/adox-api/name-property-adox.md) de la [usuario](../../../ado/reference/adox-api/user-object-adox.md) o [grupo](../../../ado/reference/adox-api/group-object-adox.md) al propietario del objeto.  
  
 *Valor de ObjectTypeId*  
 Opcional. A **Variant** valor que especifica el GUID de un tipo de objeto de proveedor que no está definido por la especificación de OLE DB. Este parámetro es obligatorio si *ObjectType* está establecido en **adPermObjProviderSpecific**; en caso contrario, no se utiliza.  
  
## <a name="remarks"></a>Comentarios  
 Si el proveedor no admite la especificación de los propietarios de objetos, se producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo GetObjectOwner y SetObjectOwner métodos (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [GetObjectOwner (método, ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)

