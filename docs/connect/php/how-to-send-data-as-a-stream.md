---
title: 'Cómo: enviar datos como una secuencia | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data
- streaming data
ms.assetid: ab6b95d6-b6e6-4bd7-a18c-50f2918f7532
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10e4c00840658ac4cb74707d0a5dfdc49d448c34
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-send-data-as-a-stream"></a>Cómo enviar datos como una secuencia
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] aprovechan las secuencias de PHP para enviar objetos de gran tamaño al servidor. En los ejemplos de este tema se muestra cómo enviar datos como una secuencia. En el primer ejemplo se utiliza el controlador SQLSRV para mostrar el comportamiento predeterminado, que consiste en enviar todos los datos de secuencia en el momento de ejecución de la consulta. El segundo ejemplo usa el controlador SQLSRV para demostrar cómo enviar hasta ocho kilobytes (8 kB) de datos de secuencia a la vez en el servidor.  
  
En el tercer ejemplo se muestra cómo enviar datos de secuencia al servidor con el controlador PDO_SQLSRV.  
  
## <a name="example-sending-stream-data-at-execution"></a>Ejemplo: Enviar datos de secuencia en ejecución
En el ejemplo siguiente se inserta una fila en la tabla *Production.ProductReview* de la base de datos de AdventureWorks. Los comentarios del cliente (*$comments*) se abren como una secuencia con PHP [fopen](http://php.net/manual/en/function.fopen.php) función y, a continuación, se transmiten al servidor tras la ejecución de la consulta.  
  
El ejemplo supone que SQL Server y el [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) base de datos se instalan en el equipo local. Todos los resultados se agregan a la consola.  
  
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
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Execute the query. All stream data is sent upon execution.*/  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
else  
{  
     echo "The query was successfully executed.";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example-sending-stream-data-using-sqlsrvsendstreamdata"></a>Ejemplo: Envío de flujo de datos mediante sqlsrv_send_stream_data
El ejemplo siguiente es el mismo que el ejemplo anterior, pero se ha desactivado el comportamiento predeterminado de enviar todos los datos de la secuencia en ejecución. En este ejemplo se utiliza [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md) para enviar datos de secuencia al servidor. Se envía hasta ocho kilobytes (8 kB) de datos con cada llamada a **sqlsrv_send_stream_data**. El script cuenta el número de llamadas realizadas por **sqlsrv_send_stream_data** y muestra el recuento en la consola.  
  
El ejemplo supone que SQL Server y el [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) base de datos se instalan en el equipo local. Todos los resultados se agregan a la consola.  
  
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
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Turn off the default behavior of sending all stream data at  
execution. */  
$options = array("SendStreamParamsAtExec" => 0);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params, $options);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Send up to 8K of parameter data to the server with each call to  
sqlsrv_send_stream_data. Count the calls. */  
$i = 1;  
while( sqlsrv_send_stream_data( $stmt))   
{  
     echo "$i call(s) made.\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Aunque los ejemplos de este tema envían datos de caracteres al servidor, pueden enviarse datos en cualquier formato como una secuencia. Por ejemplo, también puede utilizar las técnicas que se muestran en este tema para enviar imágenes en formato binario como secuencias.  
  
## <a name="example-sending-an-image-as-a-stream"></a>Ejemplo: Enviar una imagen como una secuencia 
  
```  
<?php  
   $server = "(local)";   
   $database = "Test";  
   $conn = new PDO( "sqlsrv:server=$server;Database = $database", "", "");  
  
   $binary_source = fopen( "data://text/plain,", "r");  
  
   $stmt = $conn->prepare("insert into binaries (imagedata) values (?)");  
   $stmt->bindParam(1, $binary_source, PDO::PARAM_LOB);   
  
   $conn->beginTransaction();  
   $stmt->execute();  
   $conn->commit();  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Actualización de datos &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Recuperación de datos como una secuencia con el controlador SQLSRV](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
