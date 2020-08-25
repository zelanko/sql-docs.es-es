---
description: Colección de procedimientos (ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 97421c9020750627dcd27f6188ae5cda72a2d90c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769634"
---
# <a name="procedures-collection-adox"></a>Colección de procedimientos (ADOX)
Contiene todos los objetos de [procedimiento](./procedure-object-adox.md) de un catálogo.  
  
## <a name="remarks"></a>Observaciones  
 El método [Append](./append-method-adox-procedures.md) de una colección **Procedures** es único para ADOX. Puede:  
  
-   Agregue un nuevo procedimiento a la colección con el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Puede:  
  
-   Obtener acceso a un procedimiento de la colección con la propiedad [Item](../ado-api/item-property-ado.md) .  
  
-   Devuelve el número de procedimientos contenidos en la colección con la propiedad [Count](../ado-api/count-property-ado.md) .  
  
-   Quite un procedimiento de la colección con el método [Delete](./delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de índices](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades Command y CommandText (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Ejemplo de propiedad de comando, colección de parámetros (VB)](./parameters-collection-command-property-example-vb.md)   
 [Ejemplo de método Append de procedimientos (VB)](./procedures-append-method-example-vb.md)   
 [Ejemplo de método Delete de procedimientos (VB)](./procedures-delete-method-example-vb.md)   
 [Ejemplo de método de actualización de procedimientos (VB)](./procedures-refresh-method-example-vb.md)   
 [Propiedades, métodos y eventos de la colección Procedures](./procedures-collection-properties-methods-and-events.md)   
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)   
 [Objeto Procedure (ADOX)](./procedure-object-adox.md)