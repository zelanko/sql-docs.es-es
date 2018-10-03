---
title: Requiere los proveedores para dar forma a datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 482139f8aa3dc42bbd17593b58fcc8510f1fc9a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713843"
---
# <a name="required-providers-for-data-shaping"></a>Proveedores deseados para dar forma a datos
Normalmente, la forma de datos requiere dos proveedores. El proveedor de servicios, [servicio de forma de datos para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), proporciona la funcionalidad y un proveedor de datos, como el proveedor OLE DB para SQL Server de la forma de datos, proporciona filas de datos para rellenar la forma [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Se puede especificar el nombre del proveedor de servicios (MSDataShape) como valor de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad o la palabra clave de cadena de conexión "proveedor = MSDataShape;".  
  
 Se puede especificar el nombre del proveedor de datos como el valor de la **proveedor de datos** propiedad dinámica que se agrega a la **conexión** objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección por el servicio de forma de datos para OLE DB o la palabra clave de cadena de conexión "**proveedor de datos = *** proveedor*".  
  
 Se requiere ningún proveedor de datos si la **Recordset** no se rellena (por ejemplo, al igual que en un fabricadas **Recordset** donde las columnas se crean con la palabra clave NEW). En ese caso, especifique "**proveedor de datos =** none;".  
  
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
