---
title: Índice (objeto) (ADOX) | Documentos de Microsoft
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
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4926adadc6343a51aa5cd359f0e253a9bb3925fd
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="index-object-adox"></a>Objeto Index (ADOX)
Representa un índice de una tabla de base de datos.  
  
## <a name="remarks"></a>Comentarios  
 El siguiente código crea un nuevo **índice**:  
  
```  
Dim obj As New Index  
```  
  
 Con las propiedades y colecciones de una **índice** objeto, puede:  
  
-   Identificar el índice con el [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Acceso a las columnas de base de datos del índice con la [columnas](../../../ado/reference/adox-api/columns-collection-adox.md) colección.  
  
-   Especificar si las claves de índice deben ser únicas con la [Unique](../../../ado/reference/adox-api/unique-property-adox.md) propiedad.  
  
-   Especificar si el índice es la clave principal de una tabla con el [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) propiedad.  
  
-   Especifique si los registros que tienen valores null en sus campos de índice tienen entradas de índice con la [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) propiedad.  
  
-   Especificar si el índice está agrupado con el [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) propiedad.  
  
-   Obtener acceso a propiedades de índice específicas del proveedor con el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
> [!NOTE]
>  Se producirá un error al anexar un [columna](../../../ado/reference/adox-api/column-object-adox.md) a la **columnas** colección de un **índice** si la **columna** no existe en un [Tabla](../../../ado/reference/adox-api/table-object-adox.md) objeto ya se anexa a la [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) colección.  
  
> [!NOTE]
>  Puede que su proveedor de datos no admiten todas las propiedades de **índice** objetos. Si ha configurado un valor para una propiedad que no es compatible con el proveedor, se producirá un error. Para obtener nuevos **índice** objetos, se producirá el error cuando el objeto se anexa a la colección. Para los objetos existentes, se producirá el error al establecer la propiedad.  
  
> [!NOTE]
>  Al crear **índice** objetos, la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información acerca de las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Índices de ejemplo de método Append (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Ejemplo de propiedad IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey y un ejemplo de propiedades únicas (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Ejemplo de propiedad SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
