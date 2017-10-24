---
title: "Grupos de colección (ADOX) | Documentos de Microsoft"
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
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3dfb8a9e2f75fb11caf64b06e34016474d7b9fa7
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="groups-collection-adox"></a>Colección de grupos (ADOX)
Todos los contiene almacenados [grupo](../../../ado/reference/adox-api/group-object-adox.md) objetos de un catálogo o un usuario.  
  
## <a name="remarks"></a>Comentarios  
 El **grupos** colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) todas las cuentas de grupo del catálogo representa. El **grupos** colección para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) representa sólo el grupo al que pertenece el usuario.  
  
 El [anexado](../../../ado/reference/adox-api/append-method-adox-groups.md) método para un **grupos** colección es única para ADOX. Puede hacer lo siguiente:  
  
-   Agregar un nuevo grupo de seguridad a la colección con el **anexado** método.  
  
 Las propiedades y los métodos restantes son estándar para colecciones de ADO. Puede hacer lo siguiente:  
  
-   Acceder a un grupo de la colección con el [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Devolver el número de grupos incluidos en la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Quitar un grupo de la colección con el [eliminar](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Actualizar los objetos de la colección para reflejar el esquema de base de datos actual con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Antes de anexar una **grupo** el objeto a la **grupos** colección de un **usuario** objeto, un **grupo** objeto con el mismo [ Nombre](../../../ado/reference/adox-api/name-property-adox.md) tal y como lo que se debe anexar ya debe existir en el **grupos** colección de la **catálogo**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades de la colección de grupos, métodos y eventos](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto de grupo (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)

