---
title: Colección de procedimientos (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures
- Catalog::Procedures
helpviewer_keywords:
- Procedures collection [ADOX]
ms.assetid: dc7a38e1-93b9-4034-9af2-ff419e8fb2a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 693029bf83fe28343b450906da3e16e2665819d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965436"
---
# <a name="procedures-collection-adox"></a>Colección de procedimientos (ADOX)
Contiene todos los objetos de [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md) de un catálogo.  
  
## <a name="remarks"></a>Observaciones  
 El método [Append](../../../ado/reference/adox-api/append-method-adox-procedures.md) de una colección **Procedures** es único para ADOX. Puede:  
  
-   Agregue un nuevo procedimiento a la colección con el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Puede:  
  
-   Obtener acceso a un procedimiento de la colección con la propiedad [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Devuelve el número de procedimientos contenidos en la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Quite un procedimiento de la colección con el método [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de índices](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades Command y CommandText (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Ejemplo de propiedad de comando, colección de parámetros (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Ejemplo de método Append de procedimientos (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Ejemplo de método Delete de procedimientos (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Ejemplo de método de actualización de procedimientos (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Propiedades, métodos y eventos de la colección Procedures](../../../ado/reference/adox-api/procedures-collection-properties-methods-and-events.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)
