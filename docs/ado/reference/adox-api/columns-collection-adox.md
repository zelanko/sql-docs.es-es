---
title: Colección de columnas (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc3686ac69d7afeeebec14939a42e073f796b1ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966842"
---
# <a name="columns-collection-adox"></a>Colección de columnas (ADOX)
Contiene todos los objetos de [columna](../../../ado/reference/adox-api/column-object-adox.md) de una tabla, un índice o una clave.  
  
## <a name="remarks"></a>Observaciones  
 El método [Append](../../../ado/reference/adox-api/append-method-adox-columns.md) de una colección **Columns** es único para ADOX. Puede:  
  
-   Agregue una nueva columna a la colección con el método **Append** .  
  
 Las propiedades y los métodos restantes son estándar para las colecciones de ADO. Puede:  
  
-   Obtener acceso a una columna de la colección con la propiedad [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Devuelve el número de columnas contenidas en la colección con la propiedad [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Quitar una columna de la colección con el método [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Actualice los objetos de la colección para que reflejen el esquema de la base de datos actual con el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Se producirá un error al anexar una **columna** a la colección de **columnas** de un [Índice](../../../ado/reference/adox-api/index-object-adox.md) si la **columna** no existe en una [tabla](../../../ado/reference/adox-api/table-object-adox.md) que ya esté anexada a la colección de [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de columnas](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad Name, métodos Append de columnas y tablas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Ejemplo de propiedad de tipo de tabla método de cierre de conexión (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Ejemplo de la propiedad SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
