---
title: Colección de claves (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a7bebc1c05ab195d3b23c5c0894d4fcce967625
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746549"
---
# <a name="keys-collection-adox"></a>Colección de claves (ADOX)
Contiene todos los objetos de [clave](../../../ado/reference/adox-api/key-object-adox.md) de una [tabla](../../../ado/reference/adox-api/table-object-adox.md).  
  
## <a name="remarks"></a>Comentarios  
 El método [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) de una [colección Keys](../../../ado/reference/adox-api/keys-collection-adox.md) es único para ADOX. Puede:  
  
-   Agregue una nueva clave a la colección con el método [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Puede:  
  
-   Obtener acceso a una clave en la colección con la propiedad [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Devuelve el número de claves contenidas en la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Quite una clave de la colección con el método [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de índices](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Propiedades, métodos y eventos de la colección Keys](../../../ado/reference/adox-api/keys-collection-properties-methods-and-events.md)   
 [Objeto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
