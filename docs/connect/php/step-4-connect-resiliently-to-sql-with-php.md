---
title: 'Paso 4: Conectar de forma resistente a SQL con PHP | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8013474f-48e9-43d5-ab89-7b0504044468
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f81efd8241edcf1ff437570713f6bb05ca8103f8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-connect-resiliently-to-sql-with-php"></a>Step 4: Connect resiliently to SQL with PHP (Paso 4: conectarse con resistencia a SQL con PHP)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  
El programa de demostración está diseñado para que un error transitorio durante un intento de conexión lleve a un reintento. Pero un error transitorio durante el comando de consulta hace que el programa descartar la conexión y cree una nueva conexión, antes de reintentar el comando de consulta. No se recomienda ni elegir este diseño. El programa de demostración muestra la flexibilidad de diseño que está a su disposición.  
  
La longitud de este ejemplo de código es debe principalmente a la lógica de excepción catch.   
  
Es el método Main en Program.cs. La pila de llamadas se ejecuta como sigue:  
* Main llama ConnectAndQuery.  
* Llamadas a ConnectAndQuery EstablishConnection.  
* Llamadas a EstablishConnection IssueQueryCommand.  
  
El [sqlsrv_query()](http://php.net/manual/en/function.sqlsrv-query.php) función puede utilizarse para recuperar un conjunto de resultados de una consulta en base de datos de SQL. Esta función básicamente acepta cualquier consulta y el objeto de conexión y devuelve un conjunto de resultados que puede ser recorre en iteración mediante el uso de [sqlsrv_fetch_array()](http://php.net/manual/en/function.sqlsrv-fetch-array.php).  
  
```php

    <?php  
        // Variables to tune the retry logic.    
        $connectionTimeoutSeconds = 30;  // Default of 15 seconds is too short over the Internet, sometimes.  
        $maxCountTriesConnectAndQuery = 3;  // You can adjust the various retry count values.  
        $secondsBetweenRetries = 4;  // Simple retry strategy.  
        $errNo = 0;  
        $serverName = "tcp:yourdatabase.database.windows.net,1433";  
        $connectionOptions = array("Database"=>"AdventureWorks",  
           "Uid"=>"yourusername", "PWD"=>"yourpassword", "LoginTimeout" => $connectionTimeoutSeconds);  
        $conn;  
        $errorArr = array();  
        for ($cc = 1; $cc <= $maxCountTriesConnectAndQuery; $cc++)  
        {  
            $errorArr = array();  
            $ctr = 0;  
            // [A.2] Connect, which proceeds to issue a query command.  
            $conn = sqlsrv_connect($serverName, $connectionOptions);    
            if( $conn == true)  
            {  
                echo "Connection was established";  
                echo "<br>";  
  
                $tsql = "SELECT [CompanyName] FROM SalesLT.Customer";  
                $getProducts = sqlsrv_query($conn, $tsql);  
                if ($getProducts == FALSE)  
                    die(FormatErrors(sqlsrv_errors()));  
                $productCount = 0;  
                $ctr = 0;  
                while($row = sqlsrv_fetch_array($getProducts, SQLSRV_FETCH_ASSOC))  
                {     
                    $ctr++;  
                    echo($row['CompanyName']);  
                    echo("<br/>");  
                    $productCount++;  
                    if($ctr>10)  
                        break;  
                }  
                sqlsrv_free_stmt($getProducts);  
                break;  
            }  
            // Adds any the error codes from the SQL Exception to an array.  
            else {    
                if( ($errors = sqlsrv_errors() ) != null) {  
                    foreach( $errors as $error ) {  
                        $errorArr[$ctr] = $error['code'];  
                        $ctr = $ctr + 1;  
                    }  
                }  
                $isTransientError = TRUE;  
                // [A.4] Check whether sqlExc.Number is on the whitelist of transients.  
                $isTransientError = IsTransientStatic($errorArr);  
                if ($isTransientError == TRUE)  // Is a static persistent error...  
                {  
                    echo("Persistent error suffered, SqlException.Number==". $errorArr[0].". Program Will terminate.");  
                    echo "<br>";  
                    // [A.5] Either the connection attempt or the query command attempt suffered a persistent SqlException.  
                    // Break the loop, let the hopeless program end.  
                    exit(0);  
                }  
                // [A.6] The SqlException identified a transient error from an attempt to issue a query command.  
                // So let this method reloop and try again. However, we recommend that the new query  
                // attempt should start at the beginning and establish a new connection.  
                if ($cc >= $maxCountTriesConnectAndQuery)  
                {  
                    echo "Transient errors suffered in too many retries - " . $cc ." Program will terminate.";  
                    echo "<br>";  
                    exit(0);  
                }  
                echo("Transient error encountered.  SqlException.Number==". $errorArr[0]. " . Program might retry by itself.");    
                echo "<br>";  
                echo $cc . " Attempts so far. Might retry.";  
                echo "<br>";  
                // A very simple retry strategy, a brief pause before looping. This could be changed to exponential if you want.  
                sleep(1*$secondsBetweenRetries);  
            }  
            // [A.3] All has gone well, so let the program end.  
        }  
        function IsTransientStatic($errorArr) {  
            $arrayOfTransientErrorNumbers = array(4060, 10928, 10929, 40197, 40501, 40613);  
            $result = array_intersect($arrayOfTransientErrorNumber, $errorArr);  
            $count = count($result);  
            if($count >= 0) //change to > 0 later.  
                return TRUE;  
        }  
    ?>
```
