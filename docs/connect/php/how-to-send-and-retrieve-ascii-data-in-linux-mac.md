---
title: 'Cómo: enviar y recuperar datos de ASCII en Linux y macOS (SQL) | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.openlocfilehash: 6fc7e9ad59182c2dede32917b7e54cd353119826
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>Cómo: enviar y recuperar datos de ASCII en Linux y Mac OS 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este artículo se da por supuesto que se han generado las configuraciones regionales de ASCII (no UTF-8) o se ha instalado en los sistemas Linux o Mac OS. 

Para enviar o recuperar los juegos de caracteres ASCII en el servidor:  

1.  Si la configuración regional deseada no es el predeterminado en su entorno de sistema, asegúrese de que se invoca `setlocale(LC_ALL, $locale)` antes de realizar la primera conexión. La función PHP setlocale() cambia la configuración regional solo para el script actual y, si se invoca después de realizar la primera conexión, se puede hacer caso omiso.
 
2.  Cuando se utiliza el controlador SQLSRV, puede especificar `'CharacterSet' => SQLSRV_ENC_CHAR` como una conexión de opción, pero este paso es opcional porque es el valor predeterminado de codificación.

3.  Cuando se usa el controlador PDO_SQLSRV, hay dos maneras. En primer lugar, al realizar la conexión, establecer `PDO::SQLSRV_ATTR_ENCODING` a `PDO::SQLSRV_ENCODING_SYSTEM` (para obtener un ejemplo de configuración de una opción de conexión, consulte [PDO:: __construct](../../connect/php/pdo-construct.md)). O bien, una vez conectado correctamente, agregue esta línea `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
Cuando se especifica la codificación de un objeto de conexión (PDO_SQLSRV) o un recurso de conexión (en SQLSRV), el controlador da por hecho que las otras cadenas de conexión opción usan esa misma codificación. También se da por hecho que las cadenas de nombre del servidor y consulta utilizan el mismo juego de caracteres.  
  
La codificación predeterminada para el controlador PDO_SQLSRV es UTF-8 (PDO:: sqlsrv_encoding_utf8), al contrario que el controlador SQLSRV. Para obtener más información sobre estas constantes, vea [constantes &#40;Microsoft Drivers for PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). 
  
## <a name="example"></a>Ejemplo  
Los ejemplos siguientes muestran cómo enviar y recuperar datos de ASCII con los controladores de PHP para SQL Server especificando una configuración regional determinada antes de realizar la conexión. Las configuraciones regionales en distintas plataformas Linux pueden llamarse diferente de las configuraciones regionales mismo en macOS. Por ejemplo, la configuración regional nos ISO-8859-1 (Latín 1) es `en_US.ISO-8859-1` en Linux, mientras que en macOS es el nombre `en_US.ISO8859-1`.
  
Los ejemplos supone que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está instalado en un servidor. Los resultados se agregan al explorador cuando se ejecutan los ejemplos desde el explorador.  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>Vea también  
[Recuperación de datos](../../connect/php/retrieving-data.md)  
[Trabajar con datos UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[actualizar datos &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Aplicación de ejemplo &#40;controlador SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
