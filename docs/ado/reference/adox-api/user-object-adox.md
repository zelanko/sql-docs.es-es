---
title: Objeto de usuario (ADOX) | Documentos de Microsoft
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
f1_keywords: User
helpviewer_keywords: User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7087b8d19a5f9959c15539fb9b84dd14651d2e71
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="user-object-adox"></a>Objeto de usuario (ADOX)
Representa una cuenta de usuario que tenga permisos de acceso dentro de una base de datos protegida.  
  
## <a name="remarks"></a>Comentarios  
 El [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa a los usuarios de todos los del catálogo. El **usuarios** colección para un [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa sólo los usuarios del grupo específico.  
  
 Con las propiedades, colecciones y métodos de un **usuario** objeto, puede:  
  
-   Identificar al usuario con el [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Cambiar la contraseña de un usuario con el [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) método.  
  
-   Determinar si un usuario tiene de lectura, escritura o eliminación de permisos con la [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) y [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) métodos.  
  
-   Obtener acceso a los grupos a los que pertenece el usuario con el [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) colección.  
  
-   Obtener acceso a propiedades específicas del proveedor con el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
-   Determinar la [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) para un usuario.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto User](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo GetPermissions y SetPermissions métodos (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
