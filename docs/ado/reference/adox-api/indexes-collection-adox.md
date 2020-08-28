---
description: Colección de índices (ADOX)
title: Colección Indexes (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: rothja
ms.author: jroth
ms.openlocfilehash: daea070c8bd39d6208404f119578773382078634
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984196"
---
# <a name="indexes-collection-adox"></a>Colección de índices (ADOX)
Contiene todos los objetos de [Índice](./index-object-adox.md) de una tabla.  
  
## <a name="remarks"></a>Observaciones  
 El método [Append](./append-method-adox-indexes.md) de una colección **Indexes** es único para ADOX. Se puede hacer lo siguiente:  
  
-   Agregue un nuevo índice a la colección con el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Se puede hacer lo siguiente:  
  
-   Obtener acceso a un índice de la colección con la propiedad [Item](../ado-api/item-property-ado.md) .  
  
-   Devuelve el número de índices contenidos en la colección con la propiedad [Count](../ado-api/count-property-ado.md) .  
  
-   Quitar un índice de la colección con el método [Delete](./delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de índices](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de método Append de índices (VB)](./indexes-append-method-example-vb.md)   
 [Objeto Index (ADOX)](./index-object-adox.md)