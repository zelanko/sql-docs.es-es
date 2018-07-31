---
title: sqlsrv_fetch_array | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_fetch_array
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_array
- retrieving data, as an array
- API Reference, sqlsrv_fetch_array
ms.assetid: 69270b9e-0791-42f4-856d-412da39dea63
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aab41821d2f4eb1eb3f92ce998fe440593567d0a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979718"
---
# <a name="sqlsrvfetcharray"></a>sqlsrv_fetch_array
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera la siguiente fila de datos como una matriz indizada numéricamente, una matriz asociativa o ambas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_fetch_array( resource $stmt[, int $fetchType [, row[, ]offset]])  
```  
  
#### <a name="parameters"></a>Parámetros  
*$stmt*: un recurso de instrucción correspondiente a una instrucción ejecutada.  
  
*$fetchType* [OPCIONAL]: constante predefinida. Este parámetro puede tomar uno de los valores que se muestran en la siguiente tabla:  
  
|Valor|Descripción|  
|---------|---------------|  
|SQLSRV_FETCH_NUMERIC|La siguiente fila de datos se devuelve como una matriz numérica.|  
|SQLSRV_FETCH_ASSOC|La siguiente fila de datos se devuelve como una matriz asociativa. Las claves de matriz son los nombres de columna del conjunto de resultados.|  
|SQLSRV_FETCH_BOTH|La siguiente fila de datos se devuelve como una matriz numérica y una matriz asociativa. Este es el valor predeterminado.|  
  
*row* [OPCIONAL]: se ha agregado en la versión 1.1. Uno de los siguientes valores; sirve para especificar la fila a la que se accederá en un conjunto de resultados que utilice un cursor desplazable (Si se especifica *row*, se tiene que especificar explícitamente *fetchtype*, aunque se especifique el valor predeterminado).  
  
-   SQLSRV_SCROLL_NEXT  
-   SQLSRV_SCROLL_PRIOR  
-   SQLSRV_SCROLL_FIRST  
-   SQLSRV_SCROLL_LAST  
-   SQLSRV_SCROLL_ABSOLUTE  
-   SQLSRV_SCROLL_RELATIVE  
  
Para obtener más información sobre estos valores, vea [Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md). Se ha agregado compatibilidad con los cursores desplazables en la versión 1.1 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
*offset* [OPCIONAL]: se usa con SQLSRV_SCROLL_ABSOLUTE y SQLSRV_SCROLL_RELATIVE para especificar la fila que se va a recuperar. El primer registro del conjunto de resultados es 0.  
  
## <a name="return-value"></a>Valor devuelto  
Si se recupera una fila de datos, se devuelve una **matriz** . Si no hay más filas para recuperar, se devolverá el valor **Null** . Si se produce un error, se devuelve el valor **False** .  
  
En función del valor del parámetro *$fetchType* , la **matriz** que se devuelve puede ser una **matriz**indizada numéricamente, una **matriz**asociativa o ambas. De forma predeterminada, se devuelve una **matriz** con claves numérica y asociativas. El tipo de datos de un valor de la matriz devuelta será el tipo de datos PHP predeterminados. Para obtener información sobre los tipos de datos PHP predeterminados, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="remarks"></a>Notas  
Si se devuelve una columna sin nombre, la clave del elemento de la matriz asociativa será una cadena vacía (""). Por ejemplo, observe esta instrucción de Transact-SQL que inserta un valor en una tabla de base de datos y recupera la clave principal generada por el servidor:  
  
```
INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()
```
  
Si el conjunto de resultados que devuelve la parte `SELECT SCOPE_IDENTITY()` de esta instrucción se recupera como una matriz asociativa, la clave del valor devuelto será una cadena vacía ("") debido a que la columna devuelta no tiene nombre. Para evitar esto, puede recuperar el resultado como una matriz numérica o especificar un nombre para la columna devuelta en la instrucción de Transact-SQL. A continuación, se muestra una forma de especificar un nombre de columna en Transact-SQL:  
  
```
SELECT SCOPE_IDENTITY() AS PictureID
```
  
Si un conjunto de resultados contiene varias columnas sin nombre, se asignará el valor de la última columna sin nombre a clave de la cadena vacía ("").  
  
## <a name="example"></a>Ejemplo  
En el siguiente ejemplo se recupera cada fila de un conjunto de resultados como una **matriz**asociativa. En el ejemplo se da por hecho que SQL Server y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as an associative array and display the results.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_ASSOC))  
{  
      echo $row['LastName'].", ".$row['FirstName']."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Ejemplo  
En el siguiente ejemplo se recupera cada fila de un conjunto de resultados como una matriz indizada numéricamente.  
  
En el ejemplo se recupera información de producto de la tabla *Purchasing.PurchaseOrderDetail* de la base de datos AdventureWorks de productos que tienen una fecha especificada y una cantidad con existencias (*StockQty*) inferior a un valor determinado.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
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
  
/* Define the query. */  
$tsql = "SELECT ProductID,  
                UnitPrice,  
                StockedQty   
         FROM Purchasing.PurchaseOrderDetail  
         WHERE StockedQty < 3   
         AND DueDate='2002-01-29'";  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set printing a row of data upon each  
iteration.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC))  
{  
     echo "ProdID: ".$row[0]."\n";  
     echo "UnitPrice: ".$row[1]."\n";  
     echo "StockedQty: ".$row[2]."\n";  
     echo "-----------------\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
La función **sqlsrv_fetch_array** siempre devuelve datos según los [Default PHP Data Types](../../connect/php/default-php-data-types.md). Para obtener información sobre cómo especificar el tipo de datos PHP, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Si se recupera un campo sin nombre, la clave asociativa del elemento de matriz asociativa será una cadena vacía (""). Para obtener más información, vea [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
## <a name="see-also"></a>Ver también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Recuperación de datos](../../connect/php/retrieving-data.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
