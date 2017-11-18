---
title: "Cómo: controlar errores y advertencias con el controlador SQLSRV | Documentos de Microsoft"
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
- errors and warnings
ms.assetid: fa231d60-4c06-4137-89e8-097c28638c5d
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 09b9eea3ac7dfd6320579eda54e58bc3fdae4aa1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-handle-errors-and-warnings-using-the-sqlsrv-driver"></a>Cómo controlar errores y advertencias con el controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

De forma predeterminada, el controlador SQLSRV trata las advertencias como errores; una llamada a una función de **sqlsrv** que genera un error o una advertencia devolverá el valor **False**. En este tema se muestra cómo desactivar este comportamiento predeterminado y cómo controlar las advertencias y los errores por separado.  
  
> [!NOTE]  
> El comportamiento predeterminado de tratar las advertencias como errores cuenta con algunas excepciones. Sin embargo, las advertencias que corresponden a los valores 01000, 01001, 01003 y 01S02 de SQLSTATE nunca se tratan como errores.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo de código siguiente se usa dos funciones definidas por el usuario, **DisplayErrors** y **DisplayWarnings**, para controlar errores y advertencias. El ejemplo muestra cómo controlar errores y advertencias por separado por los siguientes medios:  
  
1.  Desactiva el comportamiento predeterminado de tratar las advertencias como errores.  
  
2.  Crea un procedimiento almacenado que actualiza las horas de vacaciones de un empleado y devuelve las horas de vacaciones restantes como un parámetro de salida. Cuando las horas de vacaciones disponibles de un empleado son inferiores a cero, el procedimiento almacenado imprime una advertencia.  
  
3.  Actualiza las horas de vacaciones de varios empleados mediante una llamada al procedimiento almacenado por cada empleado y muestra los mensajes que corresponden a las advertencias y los errores que se producen.  
  
4.  Muestra las horas de vacaciones restantes de cada empleado.  
  
Tenga en cuenta que en la primera llamada a un **sqlsrv** función ([sqlsrv_configure](../../connect/php/sqlsrv-configure.md)), las advertencias se tratan como errores. Como las advertencias se agregan a la colección de errores, no se requiere comprobar las advertencias y los errores por separado. No obstante, en las llamadas posteriores a las funciones de **sqlsrv** , las advertencias no se deben tratar como errores, por lo que debe comprobar explícitamente tanto las advertencias como los errores.  
  
Observe también que en el código de ejemplo se comprueban los errores después de cada llamada a una función de **sqlsrv** . Este es el método recomendado.  
  
En este ejemplo se da por hecho que SQL Server y la base de datos de [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos. Cuando se ejecuta el ejemplo en una nueva instalación de la base de datos de AdventureWorks, se generan 3 advertencias y 2 errores. Las dos primeras advertencias son advertencias estándar que se emiten cuando se conecta a una base de datos. La tercera se genera debido a que las horas de vacaciones disponibles de un empleado se actualizan a un valor menor que cero. Los errores se producen debido a que las horas de vacaciones disponibles de un empleado se actualizan a un valor menor que 40 horas, lo que constituye una infracción de una restricción de la tabla.  
  
```  
<?php  
/* Turn off the default behavior of treating errors as warnings.  
Note: Turning off the default behavior is done here for demonstration  
purposes only. If setting the configuration fails, display errors and  
exit the script. */  
if( sqlsrv_configure("WarningsReturnAsErrors", 0) === false)  
{  
     DisplayErrors();  
     die;  
}  
  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
/* If the connection fails, display errors and exit the script. */  
if( $conn === false )  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Drop the stored procedure if it already exists. */  
$tsql1 = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query($conn, $tsql1);  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt1 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt1 );  
  
/* Create the stored procedure. */  
$tsql2 = "CREATE PROCEDURE SubtractVacationHours  
                  @EmployeeID int,  
                  @VacationHours smallint OUTPUT  
              AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHours  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHours = (SELECT VacationHours    
                                       FROM HumanResources.Employee  
                                       WHERE EmployeeID = @EmployeeID);  
              IF @VacationHours < 0   
              BEGIN  
                PRINT 'WARNING: Vacation hours are now less than zero.'  
              END;";  
$stmt2 = sqlsrv_query( $conn, $tsql2 );  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt2 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt2 );  
  
/* Set up the array that maps employee ID to used vacation hours. */  
$emp_hrs = array (7=>4, 8=>5, 9=>8, 11=>50);  
  
/* Initialize variables that will be used as parameters. */  
$employeeId = 0;  
$vacationHrs = 0;  
  
/* Set up the parameter array. */  
$params = array(  
                 array(&$employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
                );  
  
/* Define and prepare the query to substract used vacation hours. */  
$tsql3 = "{call SubtractVacationHours(?, ?)}";  
$stmt3 = sqlsrv_prepare($conn, $tsql3, $params);  
  
/* If the statement preparation fails, display errors and exit the script. */  
if( $stmt3 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Loop through the employee=>vacation hours array. Update parameter  
 values before statement execution. */  
foreach(array_keys($emp_hrs) as $employeeId)  
{  
     $vacationHrs = $emp_hrs[$employeeId];  
     /* Execute the query.  If it fails, display the errors. */  
     if( sqlsrv_execute($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /*Move to the next result returned by the stored procedure. */  
     if( sqlsrv_next_result($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /* Display updated vacation hours. */  
     echo "EmployeeID $employeeId has $vacationHrs ";  
     echo "remaining vacation hours.\n";  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
  
/* ------------- Error Handling Functions --------------*/  
function DisplayErrors()  
{  
     $errors = sqlsrv_errors(SQLSRV_ERR_ERRORS);  
     foreach( $errors as $error )  
     {  
          echo "Error: ".$error['message']."\n";  
     }  
}  
  
function DisplayWarnings()  
{  
     $warnings = sqlsrv_errors(SQLSRV_ERR_WARNINGS);  
     if(!is_null($warnings))  
     {  
          foreach( $warnings as $warning )  
          {  
               echo "Warning: ".$warning['message']."\n";  
          }  
     }  
}  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Cómo configurar el control de errores y advertencias con el controlador SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  

