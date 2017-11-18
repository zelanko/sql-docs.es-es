---
title: "Cómo: realizar transacciones | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e24f0580fc79ab07043be419a866b19a47b80f73
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-perform-transactions"></a>Cómo realizar transacciones
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

El controlador SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] proporciona 3 funciones para realizar transacciones:  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
El controlador PDO_SQLSRV proporciona 3 métodos para realizar transacciones:  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
Para ver un ejemplo, consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) .  
  
En el resto del contenido de este tema se explica y muestra cómo usar el controlador SQLSRV para realizar transacciones.  
  
## <a name="remarks"></a>Comentarios  
Los pasos para ejecutar una transacción se pueden resumir del siguiente modo:  
  
1.  Inicie la transacción con **sqlsrv_begin_transaction**.  
  
2.  Compruebe si cada consulta que forma parte de la transacción se ha realizado correctamente o no.  
  
3.  Si procede, confirme la transacción con **sqlsrv_commit**. En caso contrario, reviértala con **sqlsrv_rollback**. Después de llamar a **sqlsrv_commit** o **sqlsrv_rollback**, el controlador se devuelve al modo de confirmación automática.  
  
    De forma predeterminada, la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] está en modo de confirmación automática. Es decir, todas las consultas se confirman de forma automática cuando se realizan correctamente, salvo que se hayan designado como parte de una transacción explícita mediante **sqlsrv_begin_transaction**.  
  
    Si una transacción explícita no se confirma con **sqlsrv_commit**, se revertirá al cierre de la conexión o al término de la secuencia de comandos.  
  
    No utilice instrucciones de Transact-SQL incrustadas para realizar transacciones. Por ejemplo, para iniciar una transacción, no ejecute una instrucción con "BEGIN TRANSACTION" como consulta de Transact-SQL. No se puede garantizar que las transacciones se comporten de la forma esperada cuando se utilizan instrucciones de Transact-SQL incrustadas para realizar transacciones.  
  
    Las funciones de **sqlsrv** enumeradas anteriormente deben usarse para realizar transacciones.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Descripción  
En el ejemplo siguiente se ejecutan varias consultas como parte de una transacción. Si todas las consultas se realizan correctamente, la transacción se confirma. Si se produce un error en cualquiera de las consultas, se revierte la transacción.  
  
En el ejemplo se trata de eliminar un pedido de ventas de la tabla *Sales.SalesOrderDetail* y ajustar los niveles de inventario de productos en la tabla *Product.ProductInventory* de cada producto del pedido de ventas. Estas consultas se incluyen en una transacción, ya que todas las consultas deben realizarse correctamente con el fin de que la base de datos refleje con precisión el estado de los pedidos y la disponibilidad de los productos.  
  
En la primera consulta del ejemplo se recuperan los id. de producto y las cantidades del id. de un pedido de ventas especificado. Esta consulta no forma parte de la transacción. Sin embargo, el script se finaliza si se produce un error en esta consulta, ya que se requieren los id. de producto y las cantidades para completar las consultas que forman parte de la transacción posterior.  
  
Las consultas posteriores (eliminación del pedido de ventas y actualización de las cantidades del inventario de productos) forman parte de la transacción.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos de [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
### <a name="code"></a>código  
  
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
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>Comentarios  
Con el fin de resaltar el comportamiento de las transacciones, en el ejemplo anterior no se incluyen algunos controles de errores recomendados. En las aplicaciones de producción, se recomienda realizar la comprobación de la posible presencia de errores en todas las llamadas a una función de **sqlsrv** y controlar tales errores del modo pertinente.  
  
## <a name="see-also"></a>Vea también  
[Actualización de datos &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Transacciones (motor de base de datos)](http://go.microsoft.com/fwlink/?LinkId=105862)  
[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  

