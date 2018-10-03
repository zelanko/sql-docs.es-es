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
manager: craigg
ms.openlocfilehash: 8dc465261748c1efd340e78ddc2f3e12d601e931
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678573"
---
# <a name="users-collection-adox"></a>Colección de usuarios (ADOX)
Todos los contiene almacenan [usuario](../../../ado/reference/adox-api/user-object-adox.md) objetos de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) o [grupo](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Comentarios  
 El **usuarios** colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas las de los usuarios del catálogo. El **usuarios** colección para un [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa sólo los usuarios que tienen una pertenencia al grupo específico.  
  
 El [Append](../../../ado/reference/adox-api/append-method-adox-users.md) método para un **usuarios** colección es único para ADOX. Puede hacer lo siguiente:  
  
-   Agregar un nuevo usuario a la colección mediante el **Append** método.  
  
 Las propiedades y métodos restantes son estándar para colecciones de ADO. Puede hacer lo siguiente:  
  
-   Obtener acceso a un usuario de la colección con el [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Devuelve el número de usuarios incluidos en la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Quitar un usuario de la colección con el [eliminar](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Actualizar los objetos de la colección para reflejar el esquema de la base de datos actual con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Antes de anexar una **usuario** de objeto para el **usuarios** colección de un **grupo** objeto, un **usuario** objeto con el mismo [nombre ](../../../ado/reference/adox-api/name-property-adox.md) ya debe existir en lo que se debe anexar el **usuarios** colección de la **catálogo**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de usuarios](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [GetPermissions y SetPermissions métodos ejemplo (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
