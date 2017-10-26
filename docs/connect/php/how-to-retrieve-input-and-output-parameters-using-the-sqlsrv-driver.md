---
title: "Cómo: recuperar parámetros de E/S con el controlador SQLSRV | Documentos de Microsoft"
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
ms.assetid: 9a7c5f60-67f9-4968-a3a8-c256ee481da2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9278465398b033d198ec5b3304f9c601f5cb677b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver"></a>How to: Retrieve Input and Output Parameters Using the SQLSRV Driver
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se muestra cómo usar el controlador SQLSRV para llamar a un procedimiento almacenado en el que se ha definido un parámetro como parámetro de entrada/salida, y cómo recuperar los resultados. Tenga en cuenta que cuando se recupera un parámetro de salida o uno de entrada/salida, se deben utilizar todos los resultados que devuelve el procedimiento almacenado antes de que pueda accederse al valor del parámetro devuelto.  
  
> [!NOTE]  
> Las variables que se inicializan o actualizan a **Null**, **DateTime**o tipos de secuencia no se pueden usar como parámetros de salida.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se llama un procedimiento almacenado que resta las horas de vacaciones utilizadas de las horas de vacaciones disponibles de un empleado determinado. La variable que representa las horas de vacaciones utilizadas, *$vacationHrs*, se transmite al procedimiento almacenado como un parámetro de entrada. Después de actualizar las horas de vacaciones disponibles, el procedimiento almacenado usa el mismo parámetro para devolver el número de horas de vacaciones restantes.  
  
> [!NOTE]  
> Al inicializar *$vacationHrs* en 4, el valor del tipo PHPTYPE devuelto se establece como un entero. Para garantizar la integridad del tipo de datos, los parámetros de entrada/salida se deben inicializar antes de llamar al procedimiento almacenado, o bien hay que especificar el tipo PHPTYPE deseado. Para obtener información sobre cómo especificar el tipo PHPTYPE, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Dado que el procedimiento almacenado devuelve dos resultados, [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md) debe llamarse una vez se haya ejecutado el procedimiento almacenado para que esté disponible el valor del parámetro de salida. Después de llamar a **sqlsrv_next_result**, *$vacationHrs* contiene el valor del parámetro de salida devuelto por el procedimiento almacenado.  
  
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
$tsql_dropSP = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = "CREATE PROCEDURE SubtractVacationHours  
                        @EmployeeID int,  
                        @VacationHrs smallint OUTPUT  
                  AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHrs  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHrs = (SELECT VacationHours  
                                      FROM HumanResources.Employee  
                                      WHERE EmployeeID = @EmployeeID)";  
  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call SubtractVacationHours( ?, ?)}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an INOUT  
parameter. Initializing $vacationHrs to 8 sets the returned PHPTYPE to  
integer. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
  
$employeeId = 4;  
$vacationHrs = 8;  
$params = array(   
                 array($employeeId, SQLSRV_PARAM_IN),  
                 array($vacationHrs, SQLSRV_PARAM_INOUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $vacationHrs. */  
sqlsrv_next_result($stmt3);  
echo "Remaining vacation hours: ".$vacationHrs;  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Cómo especificar la dirección del parámetro con el controlador SQLSRV](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)  
[Cómo recuperar parámetros de salida con el controlador SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)  
[Recuperación de datos](../../connect/php/retrieving-data.md)  
  

