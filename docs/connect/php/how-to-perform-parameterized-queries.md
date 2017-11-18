---
title: "Cómo: realizar consultas con parámetros | Documentos de Microsoft"
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
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b233b2ac8b3ca454381eb3e0782ece33d59cbc8a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-perform-parameterized-queries"></a>Cómo realizar consultas con parámetros
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se resume y muestra cómo utilizar los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para realizar una consulta con parámetros.  
  
Los pasos para realizar una consulta con parámetros se pueden resumir en cuatro:  
  
1.  Coloque los signos de interrogación (?) como marcadores de posición de parámetro en la cadena de Transact-SQL que se corresponde con la consulta que se ejecutará.  
  
2.  Inicialice o actualice las variables PHP de los marcadores de posición en la consulta de Transact-SQL.  
  
3.  Utilice las variables PHP del paso 2 para crear o actualizar una matriz de valores de parámetro que se corresponden, en orden, con los marcadores de posición de la cadena de Transact-SQL.  
  
4.  Ejecute la consulta:  
  
    -   Si está utilizando el controlado SQLSRV, use [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
    -   Si está utilizando el controlador PDO_SQLSRV, ejecute la consulta con [PDO:: Prepare](../../connect/php/pdo-prepare.md) y [pdostatement:: Execute](../../connect/php/pdostatement-execute.md). En los temas sobre [PDO::prepare](../../connect/php/pdo-prepare.md) y [PDOStatement::execute](../../connect/php/pdostatement-execute.md) se muestran ejemplos de código.  
  
En el resto del contenido de este tema se describen las consultas con parámetros que utiliza el controlador SQLSRV.  
  
> [!NOTE]  
> Los parámetros se enlazan de forma implícita mediante **sqlsrv_prepare**. Es decir, si una consulta con parámetros se prepara mediante **sqlsrv_prepare** y se actualizan los valores de la matriz de parámetros, se usarán los valores actualizados en la siguiente ejecución de la consulta. Consulte el segundo ejemplo de este tema para obtener información más detallada.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se actualiza la cantidad en un id. de producto especificado en la tabla *Production.ProductInventory* de la base de datos de AdventureWorks. La cantidad y el id. de producto son parámetros de la consulta UPDATE.  
  
Después, en el ejemplo, se realiza una consulta en la base de datos para comprobar que la cantidad se ha actualizado correctamente. El id. de producto es un parámetro de la consulta SELECT.  
  
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
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
En el ejemplo anterior se usa la función **sqlsrv_query** para ejecutar consultas. Esta función es adecuada para ejecutar consultas únicas, puesto que realiza los procesos de preparación y ejecución de la instrucción. La combinación de **sqlsrv_prepare**/**sqlsrv_execute** es mejor para volver a ejecutar una consulta con distintos valores de parámetros. A continuación, encontrará un ejemplo en el que se vuelve a ejecutar una consulta con distintos valores de parámetros.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se muestra el enlace implícito de variables cuando se usa la función **sqlsrv_prepare** . En el ejemplo se insertan varios pedidos de ventas en la tabla *Sales.SalesOrderDetail* . El *$params* matriz se enlaza a la instrucción (*$stmt*) cuando **sqlsrv_prepare** se llama. Antes de cada ejecución de una consulta que inserta un nuevo pedido de ventas en la tabla, la matriz *$params* se actualiza con los nuevos valores correspondientes a los detalles del pedido de ventas. En la siguiente ejecución de la consulta se utilizan los nuevos valores de parámetro.  
  
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
     die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Convertir tipos de datos](../../connect/php/converting-data-types.md)  
[Consideraciones de seguridad para el controlador SQL para PHP](../../connect/php/security-considerations-for-php-sql-driver.md)
[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  

