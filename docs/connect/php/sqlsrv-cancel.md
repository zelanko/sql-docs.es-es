---
title: sqlsrv_cancel | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: sqlsrv_cancel
apitype: NA
helpviewer_keywords:
- sqlsrv_cancel
- API Reference, sqlsrv_cancel
ms.assetid: 75798c9b-f711-445d-9b8f-ba4d405ca50a
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d16a6d3407f6533cbf9a0b3ed9ad440a8ad2ab1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="sqlsrvcancel"></a>sqlsrv_cancel
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cancela una instrucción. Esto significa que se descarta cualquier resultado pendiente de la instrucción. Después de llama a esta función, se puede volver a ejecutar la instrucción si se ha preparado con [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). No resulta necesario llamar a esta función si se han consumido todos los resultados asociados con la instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_cancel( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$stmt*: la instrucción que se va a cancelar.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve un valor booleano **True** si la operación se realiza correctamente. De lo contrario, se devuelve el valor **False**.  
  
## <a name="example"></a>Ejemplo  
En el siguiente ejemplo se ejecuta una consulta en la base de datos de [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) y, después, se usan y cuentan los resultados hasta que la variable *$salesTotal* alcanza una cantidad especificada. Luego se descartan los resultados restantes de la consulta. En el ejemplo se da por hecho que SQL Server y la base de datos de AdventureWorks están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Prepare and execute the query. */  
$tsql = "SELECT OrderQty, UnitPrice FROM Sales.SalesOrderDetail";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
if( sqlsrv_execute( $stmt ) === false)  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Initialize tracking variables. */  
$salesTotal = 0;  
$count = 0;  
  
/* Count and display the number of sales that produce revenue  
of $100,000. */  
while( ($row = sqlsrv_fetch_array( $stmt)) && $salesTotal <=100000)  
{  
     $qty = $row[0];  
     $price = $row[1];  
     $salesTotal += ( $price * $qty);  
     $count++;  
}  
echo "$count sales accounted for the first $$salesTotal in revenue.\n";  
  
/* Cancel the pending results. The statement can be reused. */  
sqlsrv_cancel( $stmt);  
?>  
```  
  
## <a name="comments"></a>Comentarios  
Una instrucción preparada y ejecutada mediante la combinación de [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) y [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) puede volver a ejecutar con **sqlsrv_execute** después de llamar a **sqlsrv_cancel**. Una instrucción que se ejecuta con [sqlsrv_query](../../connect/php/sqlsrv-query.md) no se puede volver a ejecutar después de llamar a **sqlsrv_cancel**.  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Conexión al servidor](../../connect/php/connecting-to-the-server.md)  
[Recuperación de datos](../../connect/php/retrieving-data.md)  
[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)  
  
