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
manager: jroth
ms.openlocfilehash: 4bdb60a6d174ab82df7529b6e26d8d5b2c031107
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703952"
---
# <a name="columns-collection-adox"></a>Colección de columnas (ADOX)
Todos los contiene [columna](../../../ado/reference/adox-api/column-object-adox.md) objetos de una tabla, índice o clave.  
  
## <a name="remarks"></a>Comentarios  
 El [Append](../../../ado/reference/adox-api/append-method-adox-columns.md) método para un **columnas** colección es único para ADOX. Puede hacer lo siguiente:  
  
-   Agregar una nueva columna a la colección con el **Append** método.  
  
 Las propiedades y métodos restantes son estándar para colecciones de ADO. Puede hacer lo siguiente:  
  
-   Acceso a una columna de la colección con el [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Devuelve el número de columnas incluidas en la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Quitar una columna de la colección con el [eliminar](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Actualizar los objetos de la colección para reflejar el esquema de la base de datos actual con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Se producirá un error al anexar un **columna** a la **columnas** colección de un [índice](../../../ado/reference/adox-api/index-object-adox.md) si el **columna** no existe en un [Tabla](../../../ado/reference/adox-api/table-object-adox.md) ya que se anexa a la [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) colección.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de columnas](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de nombre (VB), métodos Append columnas y tablas](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, ejemplo de propiedad de tipo de tabla (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append de claves, método, tipo de clave, RelatedColumn, RelatedTable y UpdateRule propiedades (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Ejemplo de propiedad SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
