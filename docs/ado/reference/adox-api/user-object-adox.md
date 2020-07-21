---
title: Objeto user (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: rothja
ms.author: jroth
ms.openlocfilehash: 55315ab64f87c6aba1c988c752c4e21811fef35c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762716"
---
# <a name="user-object-adox"></a>Objeto User (ADOX)
Representa una cuenta de usuario que tiene permisos de acceso en una base de datos protegida.  
  
## <a name="remarks"></a>Observaciones  
 La colección de [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) de un [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todos los usuarios del catálogo. La colección de **usuarios** de un [Grupo](../../../ado/reference/adox-api/group-object-adox.md) solo representa a los usuarios del grupo específico.  
  
 Con las propiedades, colecciones y métodos de un objeto de **usuario** , puede:  
  
-   Identifique al usuario con la propiedad [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Cambiar la contraseña de un usuario con el método [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) .  
  
-   Determine si un usuario tiene permisos de lectura, escritura o eliminación con los métodos [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) y [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) .  
  
-   Acceder a los grupos a los que pertenece un usuario con la colección de [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) .  
  
-   Obtener acceso a las propiedades específicas del proveedor con la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
-   Determinar el [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) de un usuario.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto User](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de métodos GetPermissions y SetPermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
