---
title: Colección Users (ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a9b34813f614248669b77113491c9383ef477a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="users-collection-adox"></a>Colección Users (ADOX)
Todos los contiene almacenados [usuario](../../../ado/reference/adox-api/user-object-adox.md) objetos de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) o [grupo](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Comentarios  
 El **usuarios** colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa a los usuarios de todos los del catálogo. El **usuarios** colección para un [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa sólo los usuarios que tienen una pertenencia al grupo específico.  
  
 El [anexado](../../../ado/reference/adox-api/append-method-adox-users.md) método para un **usuarios** colección es única para ADOX. Puede hacer lo siguiente:  
  
-   Agregar un nuevo usuario a la colección mediante la **anexado** método.  
  
 Las propiedades y los métodos restantes son estándar para colecciones de ADO. Puede hacer lo siguiente:  
  
-   Tener acceso a un usuario de la colección con el [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Devolver el número de usuarios contenidos en la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Quitar un usuario de la colección con el [eliminar](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Actualizar los objetos de la colección para reflejar el esquema de la base de datos actual con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Antes de anexar una **usuario** el objeto a la **usuarios** colección de un **grupo** objeto, un **usuario** objeto con el mismo [nombre ](../../../ado/reference/adox-api/name-property-adox.md) tal y como lo que se debe anexar ya debe existir en el **usuarios** colección de la **catálogo**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de usuarios](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo GetPermissions y SetPermissions métodos (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
