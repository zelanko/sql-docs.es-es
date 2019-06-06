---
title: Objeto (ADOX) de tabla | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 43679897bf49e9a2505dad1540f3b494b66f180d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705854"
---
# <a name="table-object-adox"></a>Objeto Table (ADOX)
Representa una tabla de base de datos como columnas, índices y claves.  
  
## <a name="remarks"></a>Comentarios  
 El código siguiente crea un nuevo **tabla**:  
  
```  
Dim obj As New Table  
```  
  
 Con las propiedades y colecciones de una **tabla** objeto, puede:  
  
-   Identifique la tabla con el [nombre de propiedad (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) propiedad.  
  
-   Determinar el tipo de tabla con el [(tabla) (ADOX) del tipo de propiedad](../../../ado/reference/adox-api/type-property-table-adox.md) propiedad.  
  
-   Acceso a las columnas de la base de datos de la tabla con el [colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) colección.  
  
-   Obtener acceso a los índices de la tabla con el [colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Acceso a las claves de la tabla con el [colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Especifique el catálogo que pertenece la tabla con el [propiedad ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) propiedad.  
  
-   Devolver información de fecha con el [propiedad DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) y [propiedad DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) propiedades.  
  
-   Obtener acceso a propiedades de tabla específicas del proveedor con el [colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
> [!NOTE]
>  El proveedor de datos puede no admitir todas las propiedades de **tabla** objetos. Si ha establecido un valor para una propiedad que no es compatible con el proveedor, se producirá un error. Para el nuevo **tabla** objetos, se producirá el error cuando el objeto se anexa a la colección. Para los objetos existentes, se producirá el error al establecer la propiedad.  
>   
>  Al crear **tabla** objetos, la existencia de un valor predeterminado adecuado para una propiedad opcional no garantiza que el proveedor admita la propiedad. Para obtener más información sobre las propiedades que admite el proveedor, consulte la documentación del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Table](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedad ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Ejemplo de la propiedad de nombre (VB), métodos Append columnas y tablas](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, ejemplo de propiedad de tipo de tabla (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append de claves, método, tipo de clave, RelatedColumn, RelatedTable y UpdateRule propiedades (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
