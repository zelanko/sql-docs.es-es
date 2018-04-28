---
title: 'Cómo: especificar los tipos de datos PHP | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b41ed92a39dc18f5c253e14ecf839ec96072ea70
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-specify-php-data-types"></a>Cómo especificar tipos de datos PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cuando se utiliza el controlador PDO_SQLSRV, puede especificar el tipo de datos PHP cuando se recuperan datos del servidor con PDOStatement::bindColumn y PDOStatement::bindParam. Vea [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) y [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) para obtener más información.  
  
En los pasos siguientes se resume cómo especificar los tipos de datos PHP cuando se recuperan datos del servidor mediante el controlador SQLSRV:  
  
1.  Configurar y ejecutar una consulta de Transact-SQL con [sqlsrv_query](../../connect/php/sqlsrv-query.md) o la combinación de [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
2.  Haga que una fila de datos esté disponible para su lectura con [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md).  
  
3.  Recupere los datos de campo de una fila devuelta mediante [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) con el tipo de datos PHP deseado especificado como el tercer parámetro opcional. Si no se especifica el tercer parámetro opcional, se devuelven datos según los tipos PHP predeterminado. Para obtener información sobre los tipos de valor devueltos de PHP predeterminado, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
    Para obtener información sobre las constantes que se usan para especificar el tipo de datos PHP, consulte la sección de PHPTYPE de [constantes &#40;Microsoft Drivers for PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se recuperan las filas de la tabla *Production.ProductReview* de la base de datos de AdventureWorks. En cada fila devuelta, el *ReviewDate* campo se recupera como una cadena y la *comentarios* campo se recupera como una secuencia. Los datos de la secuencia se muestran mediante la función PHP [fpassthru](http://php.net/manual/en/function.fpassthru.php) .  
  
El ejemplo supone que SQL Server y el [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) base de datos se instalan en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT ReviewerName,   
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
En el ejemplo, al recuperar el segundo campo (*ReviewDate*) como una cadena conserva la precisión de milisegundos del tipo de datos DATETIME de SQL Server. De forma predeterminada, el tipo de datos DATETIME de SQL Server se recupera como un objeto DateTime PHP en el que se pierde la precisión de milisegundos.  
  
Recuperación del cuarto campo (*comentarios*) como una secuencia es para fines ilustrativos. De forma predeterminada, el tipo de datos nvarchar(3850) de SQL Server se recupera como una cadena, lo que resulta aceptable en la mayoría de las situaciones.  
  
> [!NOTE]  
> La función [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) proporciona una forma de obtener información de los campos, incluidos los datos de los tipos, antes de ejecutar una consulta.  
  
## <a name="see-also"></a>Vea también  
[Recuperación de datos](../../connect/php/retrieving-data.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)

[Recuperación de parámetros de salida con el controlador SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
