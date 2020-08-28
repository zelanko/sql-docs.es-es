---
description: Colección de columnas (ADOX)
title: Colección de columnas (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: rothja
ms.author: jroth
ms.openlocfilehash: f1295aea12a1b9d60427864993630320d0f973ce
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985026"
---
# <a name="columns-collection-adox"></a>Colección de columnas (ADOX)
Contiene todos los objetos de [columna](./column-object-adox.md) de una tabla, un índice o una clave.  
  
## <a name="remarks"></a>Observaciones  
 El método [Append](./append-method-adox-columns.md) de una colección **Columns** es único para ADOX. Se puede hacer lo siguiente:  
  
-   Agregue una nueva columna a la colección con el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Se puede hacer lo siguiente:  
  
-   Obtener acceso a una columna de la colección con la propiedad [Item](../ado-api/item-property-ado.md) .  
  
-   Devuelve el número de columnas contenidas en la colección con la propiedad [Count](../ado-api/count-property-ado.md) .  
  
-   Quitar una columna de la colección con el método [Delete](./delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Se producirá un error al anexar una **columna** a la colección de **columnas** de un [Índice](./index-object-adox.md) si la **columna** no existe en una [tabla](./table-object-adox.md) que ya esté anexada a la colección de [tablas](./tables-collection-adox.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de columnas](./columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad Name, métodos Append de columnas y tablas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Ejemplo de propiedad de tipo de tabla método de cierre de conexión (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Ejemplo de la propiedad SortOrder (VB)](./sortorder-property-example-vb.md)   
 [Objeto Column (ADOX)](./column-object-adox.md)