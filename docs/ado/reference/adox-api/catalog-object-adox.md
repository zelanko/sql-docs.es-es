---
title: Objeto Catalog (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
author: rothja
ms.author: jroth
ms.openlocfilehash: f13533ce9d14a650e409507e646eb536bad14e4d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763946"
---
# <a name="catalog-object-adox"></a>Objeto Catalog (ADOX)
Contiene colecciones ([tablas](../../../ado/reference/adox-api/tables-collection-adox.md), [vistas](../../../ado/reference/adox-api/views-collection-adox.md), [usuarios](../../../ado/reference/adox-api/users-collection-adox.md), [grupos](../../../ado/reference/adox-api/groups-collection-adox.md)y [procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md)) que describen el catálogo de esquemas de un origen de datos.  
  
## <a name="remarks"></a>Comentarios  
 Puede modificar el objeto de **Catálogo** agregando o quitando objetos, o modificando los objetos existentes. Es posible que algunos proveedores no admitan todos los objetos de **Catálogo** o que solo admitan ver la información de esquema.  
  
 Con las propiedades y los métodos de un objeto de **Catálogo** , puede:  
  
-   Abra el catálogo estableciendo la propiedad [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) en un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) ADO o en una cadena de conexión válida.  
  
-   Cree un nuevo catálogo con el método [Create](../../../ado/reference/adox-api/create-method-adox.md) .  
  
-   Determine los propietarios de los objetos de un **Catálogo** con los métodos [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) y [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) .  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Catalog](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Ejemplo de propiedades Command y CommandText (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Ejemplo de propiedad de tipo de tabla método de cierre de conexión (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Ejemplo del método Create (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad de comando, colección de parámetros (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Ejemplo de método Append de procedimientos (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Ejemplo de método Delete de procedimientos (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Ejemplo de método de actualización de procedimientos (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Ejemplo de colecciones y campos de vistas (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Ejemplo del método Append de vistas (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Colección views, ejemplo de propiedad CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Ejemplo de método Delete de vistas (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Ejemplo del método de actualización de vistas (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Colección Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
