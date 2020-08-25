---
description: GetObjectOwner (método, ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c68adc866ce3ee73ca184a1e5e2851b3545329d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770514"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner (método, ADOX)
Devuelve el propietario de un objeto de un [Catálogo](./catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **cadena** que especifica el [nombre](./name-property-adox.md) del [usuario](./user-object-adox.md) o [Grupo](./group-object-adox.md) al que pertenece el objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *ObjectName*  
 Valor de **cadena** que especifica el nombre del objeto para el que se va a devolver el propietario.  
  
 *ObjectType*  
 Un valor **Long** que puede ser una de las constantes [ObjectTypeEnum](./objecttypeenum.md) , que especifica el tipo del objeto para el que se va a obtener el propietario.  
  
 *ObjectTypeId*  
 Opcional. Valor **Variant** que especifica el GUID de un tipo de objeto de proveedor no definido por la especificación de OLE DB. Este parámetro es necesario si *objecttype* está establecido en **adPermObjProviderSpecific**; de lo contrario, no se utiliza.  
  
## <a name="remarks"></a>Observaciones  
 Se producirá un error si el proveedor no admite la devolución de propietarios de objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos GetObjectOwner y SetObjectOwner (VB)](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner (método)](./setobjectowner-method.md)