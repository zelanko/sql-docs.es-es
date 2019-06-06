---
title: Objeto Column (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7dcec7e665fec8ea1eb1e1dff8d08bb59ee92133
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708014"
---
# <a name="column-object-adox"></a>Objeto Column (ADOX)
Representa una columna de una tabla, índice o clave.  
  
## <a name="remarks"></a>Comentarios  
 El código siguiente crea un nuevo **columna**:  
  
 `Dim obj As New Column`  
  
 Con las propiedades y colecciones de una **columna** objeto, puede:  
  
-   Identificar la columna con el [nombre de propiedad (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Especificar el tipo de datos de la columna con el [(clave) (ADOX) del tipo de propiedad](../../../ado/reference/adox-api/type-property-key-adox.md) propiedad.  
  
-   Determinar si la columna es de longitud fija o si puede contener valores null con el [atributos de propiedad (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) propiedad.  
  
-   Especifique el tamaño máximo de la columna con el [propiedad DefinedSize (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) propiedad.  
  
-   Para los valores de datos numéricos, especifique la escala con el [propiedad NumericScale (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) propiedad.  
  
-   Para los valores de datos numéricos, especificar la precisión máxima con la [propiedad Precision (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) propiedad.  
  
-   Especifique el [objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) que contiene la columna con el [propiedad ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) propiedad.  
  
-   Para las columnas de clave, especifique el nombre de la columna relacionada en la tabla relacionada con la [propiedad RelatedColumn (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) propiedad.  
  
-   Para las columnas de índice, especificar si el criterio de ordenación es ascendente o descendente con la [propiedad SortOrder (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) propiedad.  
  
-   Obtener acceso a propiedades específicas del proveedor con el [colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
> [!NOTE]
>  No todas las propiedades de **columna** objetos pueden admitir el proveedor de datos. Si ha establecido un valor para una propiedad que no es compatible con el proveedor, se producirá un error. Para el nuevo **columna** objetos, se producirá el error cuando el objeto se anexa a la colección. Para los objetos existentes, se producirá el error al establecer la propiedad.  
>   
>  Al crear **columna** objetos, la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información sobre las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Column](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de nombre (VB), métodos Append columnas y tablas](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, ejemplo de propiedad de tipo de tabla (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append de claves, método, tipo de clave, RelatedColumn, RelatedTable y UpdateRule propiedades (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de código ADOX: NumericScale y Precision propiedades (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Ejemplo de propiedad SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
