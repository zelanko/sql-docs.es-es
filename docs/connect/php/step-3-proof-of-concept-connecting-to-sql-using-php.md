---
title: 'Paso 3: Conexión con SQL mediante PHP'
description: El paso 3 es una prueba de concepto, que muestra cómo puede conectarse a SQL Server mediante PHP. Los ejemplos básicos demuestran la selección e inserción de datos.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a7451a85-18e5-4fd0-bbcb-2f15a1117290
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69c8b1ec58dbb40ab6e4463d343720e02e583ac8
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528589"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-php"></a>Paso 3: Conexión de prueba de concepto a SQL mediante PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="step-1--connect"></a>Paso 1:  Conectar  
  
  
La función **OpenConnection** se llama casi al principio de todas las demás funciones siguientes.  
  
  
```php 
    function OpenConnection()  
    {  
        try  
        {  
            $serverName = "tcp:myserver.database.windows.net,1433";  
            $connectionOptions = array("Database"=>"AdventureWorks",  
                "Uid"=>"MyUser", "PWD"=>"MyPassword");  
            $conn = sqlsrv_connect($serverName, $connectionOptions);  
            if($conn == false)  
                die(FormatErrors(sqlsrv_errors()));  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
## <a name="step-2--execute-query"></a>Paso 2:  Ejecutar consulta  
  
La función [sqlsrv_query](https://php.net/manual/en/function.sqlsrv-query.php) puede usarse para recuperar un conjunto de resultados de una consulta realizada en SQL Database. Esta función acepta cualquier consulta y objeto de conexión y devuelve un conjunto de resultados que se puede iterar mediante el uso de [sqlsrv_fetch_array()](https://php.net/manual/en/function.sqlsrv-fetch-array.php).  
  
```php  
    function ReadData()  
    {  
        try  
        {  
            $conn = OpenConnection();  
            $tsql = "SELECT [CompanyName] FROM SalesLT.Customer";  
            $getProducts = sqlsrv_query($conn, $tsql);  
            if ($getProducts == FALSE)  
                die(FormatErrors(sqlsrv_errors()));  
            $productCount = 0;  
            while($row = sqlsrv_fetch_array($getProducts, SQLSRV_FETCH_ASSOC))  
            {  
                echo($row['CompanyName']);  
                echo("<br/>");  
                $productCount++;  
            }  
            sqlsrv_free_stmt($getProducts);  
            sqlsrv_close($conn);  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
  
## <a name="step-3--insert-a-row"></a>Paso 3:  Inserción de una fila  
  
En este ejemplo, verá cómo ejecutar una instrucción [INSERT](../../t-sql/statements/insert-transact-sql.md) de forma segura y pasar parámetros. Los valores de parámetro protegen la aplicación de la [inyección de código SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md).
  
```php 
    function InsertData()  
    {  
        try  
        {  
            $conn = OpenConnection();  
  
            $tsql = "INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT            INSERTED.ProductID VALUES ('SQL Server 1', 'SQL Server 2', 0, 0, getdate())";  
            //Insert query  
            $insertReview = sqlsrv_query($conn, $tsql);  
            if($insertReview == FALSE)  
                die(FormatErrors( sqlsrv_errors()));  
            echo "Product Key inserted is :";  
            while($row = sqlsrv_fetch_array($insertReview, SQLSRV_FETCH_ASSOC))  
            {     
                echo($row['ProductID']);  
            }  
            sqlsrv_free_stmt($insertReview);  
            sqlsrv_close($conn);  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
## <a name="step-4--roll-back-a-transaction"></a>Paso 4:  Reversión de una transacción  
  
  
Este ejemplo de código muestra el uso de transacciones con las que podrá realizar lo siguiente:  
  
\- Iniciar una transacción  
  
\- Insertar una fila de datos, actualizar otra fila de datos  
  
\- Confirmar la transacción si la inserción y actualización se realizaron correctamente y revertir la transacción si uno de ellos no lo ha sido  
  
  
```php 
    function Transactions()  
    {  
        try  
        {  
            $conn = OpenConnection();  
  
            if (sqlsrv_begin_transaction($conn) == FALSE)  
                die(FormatErrors(sqlsrv_errors()));  
  
            $tsql1 = "INSERT INTO SalesLT.SalesOrderDetail (SalesOrderID,OrderQty,ProductID,UnitPrice)  
            VALUES (71774, 22, 709, 33)";  
            $stmt1 = sqlsrv_query($conn, $tsql1);  
  
            /* Set up and execute the second query. */  
            $tsql2 = "UPDATE SalesLT.SalesOrderDetail SET OrderQty = (OrderQty + 1) WHERE ProductID = 709";  
            $stmt2 = sqlsrv_query( $conn, $tsql2);  
  
            /* If both queries were successful, commit the transaction. */  
            /* Otherwise, rollback the transaction. */  
            if($stmt1 && $stmt2)  
            {  
                   sqlsrv_commit($conn);  
                   echo("Transaction was commited");  
            }  
            else  
            {  
                sqlsrv_rollback($conn);  
                echo "Transaction was rolled back.\n";  
            }  
            /* Free statement and connection resources. */  
            sqlsrv_free_stmt( $stmt1);  
            sqlsrv_free_stmt( $stmt2);  
        }  
        catch(Exception $e)  
        {  
            echo("Error!");  
        }  
    }  
```  
  
## <a name="additional-examples"></a>Otros ejemplos  
  
[Aplicación de ejemplo (controlador SQLSRV)](../../connect/php/example-application-sqlsrv-driver.md)  

[Aplicación de ejemplo (controlador PDO_SQLSRV)](../../connect/php/example-application-pdo-sqlsrv-driver.md)
