---
description: Objeto Table (ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 847918f13dd6c91a707e660e97d1dbc4de499442
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769304"
---
# <a name="table-object-adox"></a>Objeto Table (ADOX)
Representa una tabla de base de datos que incluye columnas, índices y claves.  
  
## <a name="remarks"></a>Observaciones  
 En el código siguiente se crea una nueva **tabla**:  
  
```  
Dim obj As New Table  
```  
  
 Con las propiedades y las colecciones de un objeto de **tabla** , puede:  
  
-   Identifique la tabla con la propiedad [Name Property (Adox)](./name-property-adox.md) .  
  
-   Determine el tipo de tabla con la propiedad [Type (tabla) (Adox)](./type-property-table-adox.md) .  
  
-   Obtener acceso a las columnas de base de datos de la tabla con la colección de [colecciones de columnas (Adox)](./columns-collection-adox.md) .  
  
-   Obtener acceso a los índices de la tabla con la [colección Indexes (Adox)](./indexes-collection-adox.md).  
  
-   Obtener acceso a las claves de la tabla con la [colección de claves (Adox)](./keys-collection-adox.md).  
  
-   Especifique el catálogo al que pertenece la tabla con la propiedad [ParentCatalog Property (Adox)](./parentcatalog-property-adox.md) .  
  
-   Devuelve información de fecha con las propiedades de la [propiedad DateCreated (Adox)](./datecreated-property-adox.md) y de la [propiedad DateModified (Adox)](./datemodified-property-adox.md) .  
  
-   Obtener acceso a las propiedades de tabla específicas del proveedor con la colección de [propiedades (ADO)](../ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Es posible que el proveedor de datos no admita todas las propiedades de los objetos de **tabla** . Se producirá un error si se ha establecido un valor para una propiedad que el proveedor no admite. En el caso de los nuevos objetos de **tabla** , el error se producirá cuando el objeto se anexe a la colección. En el caso de los objetos existentes, el error se producirá al establecer la propiedad.  
>   
>  Al crear objetos de **tabla** , la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información sobre las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Table](./table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad ActiveConnection de catálogo (VB)](./catalog-activeconnection-property-example-vb.md)   
 [Ejemplo de propiedad Name, métodos Append de columnas y tablas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Ejemplo de propiedad de tipo de tabla método de cierre de conexión (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Colección de columnas (ADOX)](./columns-collection-adox.md)   
 [Colección Indexes (ADOX)](./indexes-collection-adox.md)   
 [Colección de claves (ADOX)](./keys-collection-adox.md)   
 [Colección Properties (ADO)](../ado-api/properties-collection-ado.md)   
 [Colección de tablas (ADOX)](./tables-collection-adox.md)