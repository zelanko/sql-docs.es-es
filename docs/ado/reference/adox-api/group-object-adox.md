---
title: Grupo (objeto) (ADOX) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Group
helpviewer_keywords: group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 906e5c6c208e4cc6aadf1d6e1d3a4f5529c3eb00
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="group-object-adox"></a>Objeto de grupo (ADOX)
Representa una cuenta de grupo que tenga permisos de acceso dentro de una base de datos protegida.  
  
## <a name="remarks"></a>Comentarios  
 El [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas las cuentas del catálogo grupo. El **grupos** colección para un [usuario](../../../ado/reference/adox-api/user-object-adox.md) representa sólo el grupo al que pertenece el usuario.  
  
 Con las propiedades, colecciones y métodos de un **grupo** de objeto, puede:  
  
-   Identificar el grupo con el [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Determinar si un grupo tiene de lectura, escritura o eliminación de permisos con la [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) y [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) métodos.  
  
-   Obtener acceso a las cuentas de usuario que tienen miembros en el grupo con el [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) colección.  
  
-   Obtener acceso a propiedades específicas del proveedor con el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Group](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
