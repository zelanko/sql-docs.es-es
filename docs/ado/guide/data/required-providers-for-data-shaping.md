---
title: Proveedores necesarios para el modelado de datos | Microsoft Docs
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
ms.openlocfilehash: 732563fc2c4e1cc93beac8712d845b960ae56aaf
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661278"
---
# <a name="required-providers-for-data-shaping"></a>Proveedores deseados para dar forma a datos
La forma de los datos normalmente requiere dos proveedores. El proveedor de servicios, el [servicio de forma de datos para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), proporciona la funcionalidad de forma de datos y un proveedor de datos, como el proveedor de OLE DB para SQL Server, proporciona filas de datos para rellenar el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)con forma.  
  
 El nombre del proveedor de servicios (MSDataShape) se puede especificar como el valor de la propiedad del [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) de objetos de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o la palabra clave de cadena de conexión "Provider = MSDataShape;".  
  
 El nombre del proveedor de datos se puede especificar como el valor de la propiedad dinámica del **proveedor de datos** , que el servicio de forma de datos agrega a la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) del objeto de **conexión** para OLE DB, o la palabra clave de cadena de conexión " **Proveedor de datos =** _proveedor_".  
  
 No se requiere ningún proveedor de datos si el **conjunto de registros** no está rellenado (por ejemplo, como en un **conjunto de registros** fabricado donde las columnas se crean con la palabra clave New). En ese caso, especifique "**Data Provider =** none;".  
  
## <a name="example"></a>Ejemplo  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
