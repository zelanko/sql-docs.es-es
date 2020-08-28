---
description: Colección de usuarios (ADOX)
title: Colección de usuarios (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a1f511e637696e5b14905bcccba50cb13737d6e7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983036"
---
# <a name="users-collection-adox"></a>Colección de usuarios (ADOX)
Contiene todos los objetos de [usuario](./user-object-adox.md) almacenados de un [Catálogo](./catalog-object-adox.md) o [Grupo](./group-object-adox.md).  
  
## <a name="remarks"></a>Observaciones  
 La colección de **usuarios** de un [Catálogo](./catalog-object-adox.md) representa todos los usuarios del catálogo. La colección de **usuarios** de un [Grupo](./group-object-adox.md) representa solo los usuarios que tienen una pertenencia al grupo específico.  
  
 El método [Append](./append-method-adox-users.md) de una colección **users** es único para ADOX. Se puede hacer lo siguiente:  
  
-   Agregue un nuevo usuario a la colección mediante el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Se puede hacer lo siguiente:  
  
-   Acceder a un usuario de la colección con la propiedad [Item](../ado-api/item-property-ado.md) .  
  
-   Devuelve el número de usuarios incluidos en la colección con la propiedad [Count](../ado-api/count-property-ado.md) .  
  
-   Quitar un usuario de la colección con el método [Delete](./delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Antes de anexar un objeto de **usuario** a la colección de **usuarios** de un objeto de **Grupo** , ya debe existir un objeto de **usuario** con el mismo [nombre](./name-property-adox.md) que el que se va a anexar en la colección de **usuarios** del **Catálogo**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de usuarios](./users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos GetPermissions y SetPermissions (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)   
 [Objeto User (ADOX)](./user-object-adox.md)