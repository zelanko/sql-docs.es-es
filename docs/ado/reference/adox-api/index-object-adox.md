---
title: Índice de objeto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7bff462b7c9ffe115cdfd52d1ec1f0a810a50531
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966081"
---
# <a name="index-object-adox"></a>Objeto Index (ADOX)
Representa un índice de una tabla de base de datos.  
  
## <a name="remarks"></a>Comentarios  
 El código siguiente crea un nuevo **índice**:  
  
```  
Dim obj As New Index  
```  
  
 Con las propiedades y colecciones de una **índice** objeto, puede:  
  
-   Identificar el índice con el [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Acceso a las columnas de la base de datos del índice con el [columnas](../../../ado/reference/adox-api/columns-collection-adox.md) colección.  
  
-   Especificar si las claves de índice deben ser únicas con el [Unique](../../../ado/reference/adox-api/unique-property-adox.md) propiedad.  
  
-   Especifique si el índice es la clave principal de una tabla con el [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) propiedad.  
  
-   Especifique si los registros que tienen valores null en sus campos de índice tienen entradas de índice con el [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) propiedad.  
  
-   Especificar si el índice está agrupado con el [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) propiedad.  
  
-   Obtener acceso a propiedades de índice específicas del proveedor con el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
> [!NOTE]
>  Se producirá un error al anexar un [columna](../../../ado/reference/adox-api/column-object-adox.md) a la **columnas** colección de un **índice** si el **columna** no existe en un [Tabla](../../../ado/reference/adox-api/table-object-adox.md) objeto ya se anexa a la [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) colección.  
  
> [!NOTE]
>  El proveedor de datos puede no admitir todas las propiedades de **índice** objetos. Si ha establecido un valor para una propiedad que no es compatible con el proveedor, se producirá un error. Para el nuevo **índice** objetos, se producirá el error cuando el objeto se anexa a la colección. Para los objetos existentes, se producirá el error al establecer la propiedad.  
  
> [!NOTE]
>  Al crear **índice** objetos, la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información sobre las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Los índices de ejemplo de método Append (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Ejemplo de propiedad IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey y propiedades únicas (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Ejemplo de propiedad SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
