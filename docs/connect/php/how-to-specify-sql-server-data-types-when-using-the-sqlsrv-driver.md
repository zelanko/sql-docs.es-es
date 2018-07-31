---
title: 'Cómo: Especificar tipos de datos de SQL Server cuando se usa el controlador SQLSRV | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: 1fcf73cb-5634-4d89-948f-9326f1dbd030
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9879edd7282beb2226593b70cab500fba4e09e4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38032979"
---
# <a name="how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver"></a>Cómo especificar tipos de datos de SQL Server cuando se utiliza el controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se muestra cómo usar el controlador SQLSRV para especificar el tipo de datos de SQL Server para los datos que se envían al servidor. Este tema no se aplica cuando se utiliza el controlador PDO_SQLSRV.  
  
Para especificar el tipo de datos de SQL Server, debe usar la matriz *$params* opcional al preparar o ejecutar una consulta que inserta o actualiza datos. Para obtener información más detallada sobre la estructura y la sintaxis de la matriz *$params* , consulte [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
En los pasos siguientes se resume cómo especificar el tipo de datos de SQL Server al enviar datos al servidor:  
  
> [!NOTE]  
> Si no se especifica ningún tipo de datos de SQL Server, se usan tipos predeterminados. Para obtener información sobre todos los tipos de datos SQL Server, consulte [Default SQL Server Data Types](../../connect/php/default-sql-server-data-types.md).  
  
1.  Defina una consulta de Transact-SQL que inserta o actualiza datos. Utilice signos de interrogación (?) como marcadores de posición para los valores de parámetro de la consulta.  
  
2.  Inicialice o actualice las variables PHP de los marcadores de posición en la consulta de Transact-SQL.  
  
3.  Cree la matriz *$params* que se utilizará al preparar o ejecutar la consulta. Tenga en cuenta que cada elemento de la matriz *$params* también debe ser una matriz cuando se especifica el tipo de datos de SQL Server.  
  
4.  Especifique el tipo de datos de SQL Server deseado mediante la constante **SQLSRV_SQLTYPE_\*** adecuada como cuarto parámetro de cada submatriz de la matriz *$params*. Para obtener una lista completa de las constantes **SQLSRV_SQLTYPE_\***, vea la sección SQLTYPE de [Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). Por ejemplo, en el código siguiente, *$changeDate*, *$rate*y *$payFrequency* se especifican respectivamente como los tipos de datos de SQL Server **datetime**, **dinero**y **tinyint** en la matriz *$params* . Como no se especifica ningún tipo de datos de SQL Server para *$employeeId* y se inicializa en un valor entero, se utiliza el tipo de SQL Server predeterminado **integer** .  
  
    ```  
    $employeeId = 5;  
    $changeDate = "2005-06-07";  
    $rate = 30;  
    $payFrequency = 2;  
    $params = array(  
                array($employeeId, null),  
                array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
                array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
                array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
              );  
    ```  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se insertan datos en la tabla *HumanResources.EmployeePayHistory* de la base de datos AdventureWorks. Se especifican tipos de datos de SQL Server para los parámetros *$changeDate*, *$rate*y *$payFrequency* . El tipo de datos de SQL Server predeterminado se utiliza para el parámetro *$employeeId* . Para comprobar que los datos se han insertado correctamente, se recuperan y muestran los mismos datos.  
  
En este ejemplo se da por hecho que SQL Server y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
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
$tsql1 = "INSERT INTO HumanResources.EmployeePayHistory (EmployeeID,  
                                                        RateChangeDate,  
                                                        Rate,  
                                                        PayFrequency)  
           VALUES (?, ?, ?, ?)";  
  
/* Construct the parameter array. */  
$employeeId = 5;  
$changeDate = "2005-06-07";  
$rate = 30;  
$payFrequency = 2;  
$params1 = array(  
               array($employeeId, null),  
               array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
               array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
               array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
           );  
  
/* Execute the INSERT query. */  
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
if( $stmt1 === false )  
{  
     echo "Error in execution of INSERT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the newly inserted data. */  
/* Define the query. */  
$tsql2 = "SELECT EmployeeID, RateChangeDate, Rate, PayFrequency  
          FROM HumanResources.EmployeePayHistory  
          WHERE EmployeeID = ? AND RateChangeDate = ?";  
  
/* Construct the parameter array. */  
$params2 = array($employeeId, $changeDate);  
  
/*Execute the SELECT query. */  
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if( $stmt2 === false )  
{  
     echo "Error in execution of SELECT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results. */  
$row = sqlsrv_fetch_array( $stmt2 );  
if( $row === false )  
{  
     echo "Error in fetching data.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
echo "EmployeeID: ".$row['EmployeeID']."\n";  
echo "Change Date: ".date_format($row['RateChangeDate'], "Y-m-d")."\n";  
echo "Rate: ".$row['Rate']."\n";  
echo "PayFrequency: ".$row['PayFrequency']."\n";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt1);  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="see-also"></a>Ver también  
[Recuperación de datos](../../connect/php/retrieving-data.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)

[Especificación de tipos de datos PHP](../../connect/php/how-to-specify-php-data-types.md)

[Conversión de tipos de datos](../../connect/php/converting-data-types.md)

[Envío y recuperación de datos UTF-8 gracias a la compatibilidad integrada con UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)  
  
