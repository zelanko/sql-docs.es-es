---
title: Tablas (colección) (ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6b97d189907d8f226867748e25e64972b8aba2b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35287214"
---
# <a name="tables-collection-adox"></a>Colección de tablas (ADOX)
Todos los contiene [tabla](../../../ado/reference/adox-api/table-object-adox.md) objetos de un catálogo.  
  
## <a name="remarks"></a>Notas  
 El [anexado](../../../ado/reference/adox-api/append-method-adox-tables.md) método para un **tablas** colección es única para ADOX. Puede hacer lo siguiente:  
  
-   Agregar una nueva tabla a la colección con el **anexado** método.  
  
 Las propiedades y los métodos restantes son estándar para colecciones de ADO. Puede hacer lo siguiente:  
  
-   Acceso a una tabla de la colección con el [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Devolver el número de tablas contenidas en la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Quitar una tabla de la colección con el [eliminar](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Actualizar los objetos de la colección para reflejar el esquema de base de datos actual con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Algunos proveedores pueden devolver otros objetos de esquema, como una vista, en la **tablas** colección. Por lo tanto, algunas colecciones ADOX pueden contener varias referencias al mismo objeto. Debe eliminar el objeto de una colección, el cambio no serán visible en otra colección que hace referencia al objeto eliminado hasta que el **actualizar** método se llama en la colección. Por ejemplo, con el proveedor OLE DB para Microsoft Jet, se devuelven vistas con la **tablas** colección. Si se quita una vista, debe actualizar el **tablas** colección antes de que la colección reflejará el cambio.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de tablas](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedad ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Las tablas y columnas anexar métodos, ejemplo de la propiedad de nombre (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método de cierre de conexión, ejemplo de propiedad de tipo de tabla (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Anexar de teclas de método, tipo de clave, RelatedColumn, RelatedTable y ejemplo de las propiedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
