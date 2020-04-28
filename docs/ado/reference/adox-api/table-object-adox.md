---
title: Objeto Table (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 10f3add3cb243d54643c3294104ec2546e7737d1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965164"
---
# <a name="table-object-adox"></a>Objeto Table (ADOX)
Representa una tabla de base de datos que incluye columnas, índices y claves.  
  
## <a name="remarks"></a>Observaciones  
 En el código siguiente se crea una nueva **tabla**:  
  
```  
Dim obj As New Table  
```  
  
 Con las propiedades y las colecciones de un objeto de **tabla** , puede:  
  
-   Identifique la tabla con la propiedad [Name Property (Adox)](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Determine el tipo de tabla con la propiedad [Type (tabla) (Adox)](../../../ado/reference/adox-api/type-property-table-adox.md) .  
  
-   Obtener acceso a las columnas de base de datos de la tabla con la colección de [colecciones de columnas (Adox)](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
-   Obtener acceso a los índices de la tabla con la [colección Indexes (Adox)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Obtener acceso a las claves de la tabla con la [colección de claves (Adox)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Especifique el catálogo al que pertenece la tabla con la propiedad [ParentCatalog Property (Adox)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) .  
  
-   Devuelve información de fecha con las propiedades de la [propiedad DateCreated (Adox)](../../../ado/reference/adox-api/datecreated-property-adox.md) y de la [propiedad DateModified (Adox)](../../../ado/reference/adox-api/datemodified-property-adox.md) .  
  
-   Obtener acceso a las propiedades de tabla específicas del proveedor con la colección de [propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Es posible que el proveedor de datos no admita todas las propiedades de los objetos de **tabla** . Se producirá un error si se ha establecido un valor para una propiedad que el proveedor no admite. En el caso de los nuevos objetos de **tabla** , el error se producirá cuando el objeto se anexe a la colección. En el caso de los objetos existentes, el error se producirá al establecer la propiedad.  
>   
>  Al crear objetos de **tabla** , la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información sobre las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Table](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Ejemplo de propiedad Name, métodos Append de columnas y tablas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Ejemplo de propiedad de tipo de tabla método de cierre de conexión (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Colección Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
