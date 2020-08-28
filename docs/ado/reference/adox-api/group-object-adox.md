---
description: Objeto Group (ADOX)
title: Objeto Group (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 21514bbcbe91e1320a4a2806e545d5f7b40df8d3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984436"
---
# <a name="group-object-adox"></a>Objeto Group (ADOX)
Representa una cuenta de grupo que tiene permisos de acceso en una base de datos protegida.  
  
## <a name="remarks"></a>Observaciones  
 La colección de [grupos](./groups-collection-adox.md) de un [Catálogo](./catalog-object-adox.md) representa todas las cuentas de grupo del catálogo. La colección de **grupos** para un [usuario](./user-object-adox.md) representa solo el grupo al que pertenece el usuario.  
  
 Con las propiedades, colecciones y métodos de un objeto de **Grupo** , puede:  
  
-   Identifique el grupo con la propiedad [Name](./name-property-adox.md) .  
  
-   Determine si un grupo tiene permisos de lectura, escritura o eliminación con los métodos [GetPermissions](./getpermissions-method-adox.md) y [SetPermissions](./setpermissions-method-adox.md) .  
  
-   Obtenga acceso a las cuentas de usuario que tienen pertenencias al grupo con la colección [usuarios](./users-collection-adox.md) .  
  
-   Obtener acceso a las propiedades específicas del proveedor con la colección [Properties](../ado-api/properties-collection-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Group](./group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Colección de grupos (ADOX)](./groups-collection-adox.md)   
 [Colección de usuarios (ADOX)](./users-collection-adox.md)