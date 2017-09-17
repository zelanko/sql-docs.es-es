---
title: "Colección de columnas (ADOX) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 21bf59bef5782c63a272fb16ba1a07889c6fad67
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="columns-collection-adox"></a>Colección de columnas (ADOX)
Todos los contiene [columna](../../../ado/reference/adox-api/column-object-adox.md) objetos de una tabla, índice o clave.  
  
## <a name="remarks"></a>Comentarios  
 El [anexado](../../../ado/reference/adox-api/append-method-adox-columns.md) método para un **columnas** colección es única para ADOX. Puede hacer lo siguiente:  
  
-   Agregar una nueva columna a la colección con el **anexado** método.  
  
 Las propiedades y los métodos restantes son estándar para colecciones de ADO. Puede hacer lo siguiente:  
  
-   Acceso a una columna de la colección con el [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Devolver el número de columnas contenidas en la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Quitar una columna de la colección con el [eliminar](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Actualizar los objetos de la colección para reflejar el esquema de la base de datos actual con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Se producirá un error al anexar un **columna** a la **columnas** colección de un [índice](../../../ado/reference/adox-api/index-object-adox.md) si la **columna** no existe en un [Tabla](../../../ado/reference/adox-api/table-object-adox.md) ya que se anexa a la [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) colección.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de columnas](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Las tablas y columnas anexar métodos, ejemplo de la propiedad de nombre (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método de cierre de conexión, ejemplo de propiedad de tipo de tabla (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Anexar de teclas de método, tipo de clave, RelatedColumn, RelatedTable y ejemplo de las propiedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Ejemplo de propiedad SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
