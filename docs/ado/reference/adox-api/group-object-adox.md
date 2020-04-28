---
title: Objeto Group (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b4b3de5f445ddd09bf7d069b0b93d82c6f8de978
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966213"
---
# <a name="group-object-adox"></a>Objeto Group (ADOX)
Representa una cuenta de grupo que tiene permisos de acceso en una base de datos protegida.  
  
## <a name="remarks"></a>Observaciones  
 La colección de [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas las cuentas de grupo del catálogo. La colección de **grupos** para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) representa solo el grupo al que pertenece el usuario.  
  
 Con las propiedades, colecciones y métodos de un objeto de **Grupo** , puede:  
  
-   Identifique el grupo con la propiedad [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Determine si un grupo tiene permisos de lectura, escritura o eliminación con los métodos [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) y [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) .  
  
-   Obtenga acceso a las cuentas de usuario que tienen pertenencias al grupo con la colección [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) .  
  
-   Obtener acceso a las propiedades específicas del proveedor con la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Group](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
