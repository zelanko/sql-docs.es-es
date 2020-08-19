---
description: Objeto Index (ADOX)
title: Objeto index (ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 81f0bf8d07bbb89105a0ceab421d8433d52f1672
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439947"
---
# <a name="index-object-adox"></a>Objeto Index (ADOX)
Representa un índice de una tabla de base de datos.  
  
## <a name="remarks"></a>Observaciones  
 En el código siguiente se crea un nuevo **Índice**:  
  
```  
Dim obj As New Index  
```  
  
 Con las propiedades y las colecciones de un objeto **index** , puede:  
  
-   Identifique el índice con la propiedad [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Obtener acceso a las columnas de base de datos del índice con la colección de [columnas](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
-   Especifique si las claves de índice deben ser únicas con la propiedad [Unique](../../../ado/reference/adox-api/unique-property-adox.md) .  
  
-   Especifique si el índice es la clave principal de una tabla con la propiedad [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) .  
  
-   Especifique si los registros que tienen valores NULL en sus campos de índice tienen entradas de índice con la propiedad [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) .  
  
-   Especifique si el índice está agrupado con la propiedad [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) .  
  
-   Obtener acceso a las propiedades de índice específicas del proveedor con la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Se producirá un error al anexar una [columna](../../../ado/reference/adox-api/column-object-adox.md) a la colección de **columnas** de un **Índice** si la **columna** no existe en un objeto de [tabla](../../../ado/reference/adox-api/table-object-adox.md) ya anexado a la colección de [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
> [!NOTE]
>  Es posible que el proveedor de datos no admita todas las propiedades de los objetos de **Índice** . Se producirá un error si se ha establecido un valor para una propiedad que no es compatible con el proveedor. En el caso de los nuevos objetos **index** , el error se producirá cuando el objeto se anexe a la colección. En el caso de los objetos existentes, el error se producirá al establecer la propiedad.  
  
> [!NOTE]
>  Al crear objetos de **Índice** , la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información sobre las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de método Append de índices (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Ejemplo de propiedad IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [Ejemplo de propiedades PrimaryKey y Unique (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Ejemplo de la propiedad SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
