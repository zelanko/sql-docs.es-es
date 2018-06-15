---
title: Recibir varios conjuntos de registros | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73bf5b086b82f1accdcb34f4e75c4101e324e532
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272264"
---
# <a name="receiving-multiple-recordsets"></a>Recibir varios conjuntos de registros
El [proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) admite devolver varios **Recordset** objetos de un comando único que contiene varias instrucciones SQL, una **Recordset**por la instrucción SQL. El orden en que el **Recordset**se devolverán sigue el orden en que las instrucciones SQL se colocan en el texto del comando.  
  
 El proveedor Microsoft OLE DB para SQL Server también devuelve varios conjuntos de resultados a ADO cuando el comando contiene una cláusula COMPUTE. Por ejemplo, un comando que contiene la instrucción SQL siguiente devolverá los resultados en dos **Recordset** objetos: uno para el conjunto de filas de (*ProductID*, *ProductName*, *UnitPrice*) y otro para el precio medio de todos los productos de la tabla.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 Puede usar el **Recordset.NextRecordset** método para enumerar los dos objetos.  
  
 Para obtener más información, consulte [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).
