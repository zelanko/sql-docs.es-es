---
title: 'Procedimientos: Envío y recuperación de datos UTF-8 gracias a la compatibilidad integrada con UTF-8'
description: Obtenga información sobre cómo enviar y recuperar datos con codificación UTF-8 mediante la compatibilidad con UTF-8 integrada en los controladores para PHP.
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, UTF-8 encoded data
- converting data types
- updating data
ms.assetid: 366c57cf-352f-4202-8074-6ddce44880d1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7c914306258394bde91d64e5cb84665d62ab2b4
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081404"
---
# <a name="how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support"></a>Procedimientos: Envío y recuperación de datos UTF-8 gracias a la compatibilidad integrada con UTF-8
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Si está utilizando el controlador PDO_SQLSRV, puede especificar la codificación con el atributo PDO::SQLSRV_ATTR_ENCODING. Para obtener más información, vea [Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
En el resto del contenido de este tema, se habla sobre la codificación con el controlador SQLSRV.  
  
Para enviar o recuperar datos codificados UTF-8 en el servidor, haga lo siguiente:  
  
1.  Asegúrese de que la columna de origen o destino es de tipo **nchar** o **nvarchar**.  
  
2.  Especifique el tipo PHP como `SQLSRV_PHPTYPE_STRING('UTF-8')` en la matriz de parámetros. También puede especificar `"CharacterSet" => "UTF-8"` como una opción de conexión.  
  
    Al especificar un juego de caracteres como parte de las opciones de conexión, el controlador da por hecho que las otras cadenas de conexión opción usan ese mismo juego de caracteres. También se da por hecho que las cadenas de nombre del servidor y consulta utilizan el mismo juego de caracteres.  
  
Puede transmitir UTF-8 o SQLSRV_ENC_CHAR a **CharacterSet**,pero no se puede transmitir SQLSRV_ENC_BINARY. La codificación predeterminada es SQLSRV_ENC_CHAR.  
  
## <a name="connection-example"></a>Ejemplo de conexión  
En el ejemplo siguiente se muestra cómo enviar y recuperar datos con codificación UTF-8 especificando el juego de caracteres UTF-8 al realizar la conexión. En el ejemplo se actualiza la columna Comentarios de la tabla Production.ProductReview para un id. de revisión especificado. En el ejemplo también se recuperan los datos actualizados recientemente y los muestra. Tenga en cuenta que la columna Comentarios es del tipo **nvarchar(3850).** Recuerde también que antes de enviar los datos al servidor se convierten a la codificación UTF-8 mediante la función PHP **utf8_encode**. Esta operación se realiza únicamente con fines de demostración. En un escenario real de aplicaciones, comenzaría con datos codificados en UTF-8.  
  
En el ejemplo se da por hecho que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan al explorador cuando se ejecuta el ejemplo en el explorador.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "CharacterSet" => "UTF-8");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing 1, 2, 3, 4.  Testing.");  
$params1 = array(  
                  array( $comments, null ),  
                  array( $reviewID, null )  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field( $stmt2, 0 );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
Para obtener información sobre cómo almacenar datos Unicode, consulte [Trabajar con datos Unicode](/previous-versions/sql/sql-server-2008-r2/ms175180(v=sql.105)).  
  
## <a name="column-example"></a>Ejemplo de columna  
El ejemplo siguiente es similar al primero, pero en lugar de especificar el juego de caracteres UTF-8 en la conexión, muestra cómo especificar el juego de caracteres UTF-8 en la columna.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing");  
$params1 = array(  
                  array($comments,  
                        SQLSRV_PARAM_IN,  
                        SQLSRV_PHPTYPE_STRING('UTF-8')  
                  ),  
                  array($reviewID)  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field($stmt2,   
                            0,   
                            SQLSRV_PHPTYPE_STRING('UTF-8')  
                           );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Recuperación de datos](../../connect/php/retrieving-data.md)

[Envío y recuperación de datos ASCII en Linux y Mac OS](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)

[Actualización de datos &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Aplicación de ejemplo &#40;controlador SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
