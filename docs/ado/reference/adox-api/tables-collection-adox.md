---
title: Tablas de la colección (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1ba06c10b3f890f08abac371346c3d03a0278aa8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705727"
---
# <a name="tables-collection-adox"></a>Colección de tablas (ADOX)
Todos los contiene [tabla](../../../ado/reference/adox-api/table-object-adox.md) objetos de un catálogo.  
  
## <a name="remarks"></a>Comentarios  
 El [Append](../../../ado/reference/adox-api/append-method-adox-tables.md) método para un **tablas** colección es único para ADOX. Puede hacer lo siguiente:  
  
-   Agregar una nueva tabla a la colección con el **Append** método.  
  
 Las propiedades y métodos restantes son estándar para colecciones de ADO. Puede hacer lo siguiente:  
  
-   Acceso a una tabla en la colección con el [elemento](../../../ado/reference/ado-api/item-property-ado.md) propiedad.  
  
-   Devuelve el número de las tablas contenidas en la colección con el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad.  
  
-   Quitar una tabla de la colección con el [eliminar](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Actualizar los objetos de la colección para reflejar el esquema de base de datos actual con el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Algunos proveedores pueden devolver otros objetos de esquema, como una vista, en el **tablas** colección. Por lo tanto, algunas colecciones ADOX pueden contener varias referencias al mismo objeto. Debe eliminar el objeto de una colección, el cambio no serán visible en otra colección que se hace referencia al objeto eliminado hasta que el **actualizar** se llama al método en la colección. Por ejemplo, con el proveedor OLE DB para Microsoft Jet, se devuelven las vistas con el **tablas** colección. Si quita una vista, debe actualizar el **tablas** colección antes de la colección reflejará el cambio.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de la colección de tablas](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedad ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Ejemplo de la propiedad de nombre (VB), métodos Append columnas y tablas](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, ejemplo de propiedad de tipo de tabla (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append de claves, método, tipo de clave, RelatedColumn, RelatedTable y UpdateRule propiedades (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
