---
title: Proveedores necesarios para dar forma a datos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2dc7048ea3442a77f6aadf7d7b1868c2ac9d833
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="required-providers-for-data-shaping"></a>Proveedores deseados para dar forma a datos
Normalmente, la forma de datos requiere dos proveedores. El proveedor de servicios, [servicio de forma de datos para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), proporciona la funcionalidad y un proveedor de datos, como el proveedor OLE DB para SQL Server de forma de datos, proporciona filas de datos para rellenar la forma [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Se puede especificar el nombre del proveedor de servicios (MSDataShape) como el valor de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad o la palabra clave de cadena de conexión "proveedor = MSDataShape;".  
  
 El nombre del proveedor de datos se puede especificar como el valor de la **proveedor de datos** propiedad dinámica, que se agrega a la **conexión** objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección por el servicio de forma de datos de OLE DB o la palabra clave de cadena de conexión "**proveedor de datos =***proveedor*".  
  
 Ningún proveedor de datos es necesaria si la **Recordset** no incluirá ningún dato (por ejemplo, al igual que en un fabricadas **Recordset** donde las columnas se crean con la palabra clave NEW). En ese caso, especifique "**proveedor de datos =**none;".  
  
## <a name="example"></a>Ejemplo  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)

