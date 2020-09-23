---
title: 'Procedimientos: Envío y recuperación de datos ASCII en Linux y macOS (SQL)'
description: En este tema se describe cómo enviar y recuperar datos ASCII en Linux y macOS al cuando se usan los controladores de Microsoft para PHP en SQL Server
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 015562e9a783cef79a9466778b89edecffee5fe0
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680430"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>Procedimientos: Envío y recuperación de datos ASCII en Linux y Mac OS 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este artículo se da por sentado que las configuraciones regionales ASCII (no UTF-8) se han generado o instalado en sus sistemas Linux o macOS. 

Para enviar conjuntos de caracteres ASCII al servidor o recuperarlos:  

1.  Si la configuración regional deseada no es la predeterminada del entorno del sistema, asegúrese de invocar `setlocale(LC_ALL, $locale)` antes de realizar la primera conexión. La función setlocale() PHP cambia la configuración regional solo para el script actual y, en caso de invocarse tras realizarse la primera conexión, es posible que se omita.
 
2.  Al usar el controlador SQLSRV, puede especificar `'CharacterSet' => SQLSRV_ENC_CHAR` como opción de conexión, pero este paso es opcional, ya que se trata de la codificación predeterminada.

3.  Al usar el controlador PDO_SQLSRV, hay dos maneras. En primer lugar, al establecer la conexión, establezca `PDO::SQLSRV_ATTR_ENCODING` en `PDO::SQLSRV_ENCODING_SYSTEM` (para ver un ejemplo de establecimiento de una opción de conexión, consulte [PDO:: __construct](../../connect/php/pdo-construct.md)). Como alternativa, después de conectarse correctamente, agregue esta línea `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
Al especificar la codificación de un recurso de conexión (en SQLSRV) u objeto de conexión (PDO_SQLSRV), el controlador da por sentado que las otras cadenas de opciones de conexión usan esa misma codificación. También se da por hecho que las cadenas de nombre del servidor y consulta utilizan el mismo juego de caracteres.  
  
La codificación predeterminada para el controlador PDO_SQLSRV es UTF-8 (PDO::SQLSRV_ENCODING_UTF8), a diferencia del controlador SQLSRV. Para obtener más información sobre estas constantes de PHP, vea [Constantes &#40;Controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). 
  
## <a name="example"></a>Ejemplo  
En los siguientes ejemplos se muestra cómo enviar y recuperar datos ASCII mediante los controladores para PHP para SQL Server especificando una configuración regional particular antes del realizar la conexión. A las configuraciones regionales en diversas plataformas de Linux se les puede asignar nombres distintos de los de las mismas configuraciones regionales en macOS. Por ejemplo, la configuración regional ISO-8859-1 (Latín 1) de Estados Unidos es `en_US.ISO-8859-1` en Linux, mientras que en macOS el nombre es `en_US.ISO8859-1`.
  
En los ejemplos se da por sentado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado en un servidor. Los resultados se agregan al explorador cuando se ejecuta el ejemplo en el explorador.  
  
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

## <a name="see-also"></a>Consulte también  
[Recuperación de datos](../../connect/php/retrieving-data.md)  
[Trabajo con datos UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[Actualización de datos &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Aplicación de ejemplo &#40;controlador SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
