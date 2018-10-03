---
title: sqlsrv_has_rows | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- API Reference, sqlsrv_has_rows
- sqlsrv_has_rows
ms.assetid: 4da7f640-cf12-409f-9e00-95b30a8d5e17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cc449b6aa47024d9d38af1870dfa370f8a59896
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772773"
---
# <a name="sqlsrvhasrows"></a>sqlsrv_has_rows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Indica si el conjunto de resultados tiene una o varias filas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_has_rows( resource $stmt )  
```  
  
#### <a name="parameters"></a>Parámetros  
*$stmt*: la instrucción ejecutada.  
  
## <a name="return-value"></a>Valor devuelto  
Si hay filas en el conjunto de resultados, se devolverá el valor **True**. Si no hay ninguna fila, o si se produce un error en la llamada de función, se devolverá el valor **False**.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
   $server = "server_name";  
   $conn = sqlsrv_connect( $server, array( 'Database' => 'Northwind' ) );  
  
   $stmt = sqlsrv_query( $conn, "select * from orders where CustomerID = 'VINET'" , array());  
  
   if ($stmt !== NULL) {  
      $rows = sqlsrv_has_rows( $stmt );  
  
      if ($rows === true)  
         echo "\nthere are rows\n";  
      else   
         echo "\nno rows\n";  
   }  
?>  
```  
  
## <a name="see-also"></a>Ver también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
