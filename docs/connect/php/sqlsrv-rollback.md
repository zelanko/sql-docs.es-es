---
title: sqlsrv_rollback | Documentos de Microsoft
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
apiname:
- sqlsrv_rollback
apitype: NA
helpviewer_keywords:
- transaction support
- API Reference, sqlsrv_rollback
- sqlsrv_rollback
ms.assetid: 6e6bac39-45af-428c-bc32-f773482562ee
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2384548296b11428336d65600a31df0a43e90db1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvrollback"></a>sqlsrv_rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Revierte la transacción actual en la conexión especificada y devuelve la conexión al modo de confirmación automática. La transacción actual incluye todas las instrucciones de la conexión especificada que se ejecutaron después de llamar a [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md) y antes de llamar a **sqlsrv_rollback** o [sqlsrv_commit](../../connect/php/sqlsrv-commit.md).  
  
> [!NOTE]  
> El [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] está en modo de confirmación automática de forma predeterminada. Es decir, todas las consultas se confirman de forma automática cuando se realizan correctamente, salvo que se hayan designado como parte de una transacción explícita mediante **sqlsrv_begin_transaction**.  
  
> [!NOTE]  
> Si se llama a **sqlsrv_rollback** en una conexión que no se encuentre en una transacción activa y que se inició con **sqlsrv_begin_transaction**, la llamada devuelve el valor **False** y se agrega un error *No en la transacción* a la colección de errores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_rollback( resource $conn)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$conn*: la conexión en la que la transacción está activa.  
  
## <a name="return-value"></a>Valor devuelto  
Se revierte un valor booleano **True** si la transacción se ha confirmado correctamente. De lo contrario, se devuelve el valor **False**.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se ejecutan dos consultas como parte de una transacción. Si las dos son correctas, se confirma la transacción. Si se produce un error en una de las consultas (o en ambas), se revierte la transacción.  
  
La primera consulta del ejemplo inserta un nuevo pedido de ventas en la tabla *Sales.SalesOrderDetail* de la base de datos de AdventureWorks. El pedido corresponde a 5 unidades del producto con el id. de producto 709. La segunda consulta reduce en 5 unidades la cantidad de inventario del id. de producto 709. Estas consultas se incluyen en una transacción, ya que ambas deben realizarse correctamente para que la base de datos refleje con precisión el estado de los pedidos y la disponibilidad de los productos.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos de [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
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
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initiate transaction. */  
/* Exit script if transaction cannot be initiated. */  
if ( sqlsrv_begin_transaction( $conn) === false )  
{  
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initialize parameter values. */  
$orderId = 43659; $qty = 5; $productId = 709;  
$offerId = 1; $price = 5.70;  
  
/* Set up and execute the first query. */  
$tsql1 = "INSERT INTO Sales.SalesOrderDetail   
                     (SalesOrderID,   
                      OrderQty,   
                      ProductID,   
                      SpecialOfferID,   
                      UnitPrice)  
          VALUES (?, ?, ?, ?, ?)";  
$params1 = array( $orderId, $qty, $productId, $offerId, $price);  
$stmt1 = sqlsrv_query( $conn, $tsql1, $params1 );  
  
/* Set up and executee the second query. */  
$tsql2 = "UPDATE Production.ProductInventory   
          SET Quantity = (Quantity - ?)   
          WHERE ProductID = ?";  
$params2 = array($qty, $productId);  
$stmt2 = sqlsrv_query( $conn, $tsql2, $params2 );  
  
/* If both queries were successful, commit the transaction. */  
/* Otherwise, rollback the transaction. */  
if( $stmt1 && $stmt2 )  
{  
     sqlsrv_commit( $conn );  
     echo "Transaction was committed.\n";  
}  
else  
{  
     sqlsrv_rollback( $conn );  
     echo "Transaction was rolled back.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
Con el fin de resaltar el comportamiento de las transacciones, en el ejemplo anterior no se incluyen algunos controles de errores recomendados. En las aplicaciones de producción, se recomienda realizar la comprobación de la posible presencia de errores en todas las llamadas a una función de **sqlsrv** y controlar tales errores del modo pertinente.  
  
> [!NOTE]  
> No utilice instrucciones de Transact-SQL incrustadas para realizar transacciones. Por ejemplo, para iniciar una transacción, no ejecute una instrucción con "BEGIN TRANSACTION" como consulta de Transact-SQL. No se puede garantizar el comportamiento transaccional esperado cuando se usa Transact-SQL incrustadas para realizar transacciones.  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Cómo realizar transacciones](../../connect/php/how-to-perform-transactions.md)  
[Información general sobre el controlador SQL para PHP](../../connect/php/overview-of-the-php-sql-driver.md) 
  

