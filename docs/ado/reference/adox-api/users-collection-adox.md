---
title: Colección de usuarios (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a6146a942e572e28692ceaafd77d6958cdab9dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964951"
---
# <a name="users-collection-adox"></a>Colección de usuarios (ADOX)
Contiene todos los objetos de [usuario](../../../ado/reference/adox-api/user-object-adox.md) almacenados de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) o [Grupo](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Observaciones  
 La colección de **usuarios** de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todos los usuarios del catálogo. La colección de **usuarios** de un [Grupo](../../../ado/reference/adox-api/group-object-adox.md) representa solo los usuarios que tienen una pertenencia al grupo específico.  
  
 El método [Append](../../../ado/reference/adox-api/append-method-adox-users.md) de una colección **users** es único para ADOX. Puede realizar lo siguiente:  
  
-   Agregue un nuevo usuario a la colección mediante el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Puede realizar lo siguiente:  
  
-   Acceder a un usuario de la colección con la propiedad [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Devuelve el número de usuarios incluidos en la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Quitar un usuario de la colección con el método [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Antes de anexar un objeto de **usuario** a la colección de **usuarios** de un objeto de **Grupo** , ya debe existir un objeto de **usuario** con el mismo [nombre](../../../ado/reference/adox-api/name-property-adox.md) que el que se va a anexar en la colección de **usuarios** del **Catálogo**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de usuarios](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos GetPermissions y SetPermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
