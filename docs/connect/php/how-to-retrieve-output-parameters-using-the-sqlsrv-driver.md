---
title: "Cómo: recuperar parámetros de salida con el controlador SQLSRV | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedure support
ms.assetid: 1157bab7-6ad1-4bdb-a81c-662eea3e7fcd
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 91401b79d504a140147572c5f2c1f7abc439d221
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-retrieve-output-parameters-using-the-sqlsrv-driver"></a>Cómo recuperar parámetros de salida con el controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se muestra cómo llamar a un procedimiento almacenado en el que se ha definido un parámetro como parámetro de salida. Tenga en cuenta que cuando se recupera un parámetro de salida o uno de entrada/salida, se deben utilizar todos los resultados que devuelve el procedimiento almacenado antes de que pueda accederse al valor del parámetro devuelto.  
  
> [!NOTE]  
> Las variables que se inicializan o actualizan a **Null**, **DateTime**o tipos de secuencia no se pueden usar como parámetros de salida.  
  
Puede producirse un truncamiento de datos cuando se utilizan tipos de secuencia, por ejemplo, SQLSRV_SQLTYPE_VARCHAR('max'), como parámetros de salida. No se permiten tipos de secuencia como parámetros de salida. En cuanto a los tipos que no son de secuencia, puede producirse un truncamiento de datos si no se especifica la longitud del parámetro de salida o si la longitud especificada no es suficientemente grande para el parámetro de salida.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se llama a un procedimiento almacenado que devuelve las ventas hasta la fecha que ha realizado un determinado empleado. La variable PHP *$lastName* es un parámetro de entrada y *$salesYTD* es un parámetro de salida.  
  
> [!NOTE]  
> Al inicializar *$salesYTD* en 0,0, el valor del tipo PHPTYPE devuelto se establece en **float**. Para garantizar la integridad del tipo de datos, los parámetros de salida se deben inicializar antes de llamar al procedimiento almacenado, o bien hay que especificar el tipo PHPTYPE deseado. Para obtener información sobre cómo especificar el tipo PHPTYPE, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Dado que el procedimiento almacenado solo devuelve un resultado, *$salesYTD* contiene el valor devuelto del parámetro de salida inmediatamente después de ejecutar el procedimiento almacenado.  
  
> [!NOTE]  
> Se recomienda llamar a procedimientos almacenados mediante sintaxis canónica. Para obtener más información sobre la sintaxis canónica, consulte [Llamar a un procedimiento almacenado](http://go.microsoft.com/fwlink/?linkid=119517).  
  
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
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('GetEmployeeSalesYTD', 'P') IS NOT NULL  
                DROP PROCEDURE GetEmployeeSalesYTD";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = " CREATE PROCEDURE GetEmployeeSalesYTD  
                   @SalesPerson nvarchar(50),  
                   @SalesYTD money OUTPUT  
                   AS  
                   SELECT @SalesYTD = SalesYTD  
                   FROM Sales.SalesPerson AS sp  
                   JOIN HumanResources.vEmployee AS e   
                   ON e.EmployeeID = sp.SalesPersonID  
                   WHERE LastName = @SalesPerson";  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
 the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call GetEmployeeSalesYTD( ?, ? )}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an OUTPUT  
parameter. Initializing $salesYTD to 0.0 sets the returned PHPTYPE to  
float. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
$lastName = "Blythe";  
$salesYTD = 0.0;  
$params = array(   
                 array($lastName, SQLSRV_PARAM_IN),  
                 array($salesYTD, SQLSRV_PARAM_OUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $salesYTD. */  
echo "YTD sales for ".$lastName." are ". $salesYTD. ".";  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Cómo especificar la dirección del parámetro con el controlador SQLSRV](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)  
[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
[Recuperación de datos](../../connect/php/retrieving-data.md)  
  

