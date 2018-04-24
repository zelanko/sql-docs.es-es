---
title: Tabla (objeto) (ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72870be3143b1b5b801f5df4feef5043f3816fe8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="table-object-adox"></a>Objeto de tabla (ADOX)
Representa una tabla de base de datos que incluye columnas, índices y claves.  
  
## <a name="remarks"></a>Comentarios  
 El siguiente código crea un nuevo **tabla**:  
  
```  
Dim obj As New Table  
```  
  
 Con las propiedades y colecciones de una **tabla** objeto, puede:  
  
-   Identifique la tabla con el [nombre de propiedad (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Determinar el tipo de tabla con el [(tabla) (ADOX) del tipo de propiedad](../../../ado/reference/adox-api/type-property-table-adox.md) propiedad.  
  
-   Acceso a las columnas de base de datos de la tabla con el [colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) colección.  
  
-   Obtener acceso a los índices de la tabla con el [colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Acceso a las claves de la tabla con el [colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Especifique el catálogo al que pertenece la tabla con el [propiedad ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) propiedad.  
  
-   Devolver información de fecha con el [propiedad DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) y [propiedad DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) propiedades.  
  
-   Obtener acceso a propiedades de tabla específicas del proveedor con el [colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
> [!NOTE]
>  Puede que su proveedor de datos no admiten todas las propiedades de **tabla** objetos. Si ha configurado un valor para una propiedad que no es compatible con el proveedor, se producirá un error. Para obtener nuevos **tabla** objetos, se producirá el error cuando el objeto se anexa a la colección. Para los objetos existentes, se producirá el error al establecer la propiedad.  
>   
>  Al crear **tabla** objetos, la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información acerca de las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Table](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedad ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Las tablas y columnas anexar métodos, ejemplo de la propiedad de nombre (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método de cierre de conexión, ejemplo de propiedad de tipo de tabla (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Anexar de teclas de método, tipo de clave, RelatedColumn, RelatedTable y ejemplo de las propiedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
