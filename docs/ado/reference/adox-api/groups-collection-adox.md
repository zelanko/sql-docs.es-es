---
title: Colección de grupos (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: rothja
ms.author: jroth
ms.openlocfilehash: e2b6e7b7669e0976cf47e5b4d5d2c827a824f919
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764856"
---
# <a name="groups-collection-adox"></a>Colección de grupos (ADOX)
Contiene todos los objetos de [Grupo](../../../ado/reference/adox-api/group-object-adox.md) almacenados de un catálogo o usuario.  
  
## <a name="remarks"></a>Comentarios  
 La colección de **grupos** de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas las cuentas de grupo del catálogo. La colección de **grupos** para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) representa solo el grupo al que pertenece el usuario.  
  
 El método [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) de una colección **Groups** es único para ADOX. Puede:  
  
-   Agregue un nuevo grupo de seguridad a la colección con el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Puede:  
  
-   Obtener acceso a un grupo de la colección con la propiedad [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Devuelve el número de grupos incluidos en la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Quite un grupo de la colección con el método [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Antes de anexar un objeto de **Grupo** a la colección **Groups** de un objeto **User** , el objeto **Group** con el mismo [nombre](../../../ado/reference/adox-api/name-property-adox.md) que el que se va a anexar ya debe existir en la colección **Groups** del **Catálogo**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de grupos](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
