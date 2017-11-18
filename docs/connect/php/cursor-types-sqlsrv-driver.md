---
title: Tipos de cursor (controlador SQLSRV) | Documentos de Microsoft
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
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92fa89c2f477b867930d1b53da7e6fa318a3d39d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-types-sqlsrv-driver"></a>Tipos de cursor (controlador SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

El controlador SQLSRV le permite crear un conjunto de resultados con filas que se pueden acceder en cualquier orden, según el tipo de cursor.  En este tema se tratará (almacenado en búfer) en el lado de cliente y servidor (no almacenar en búfer) cursores.  
  
## <a name="cursor-types"></a>Tipos de cursor  
Cuando se crea un conjunto de resultados con [sqlsrv_query](../../connect/php/sqlsrv-query.md) o con [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md), puede especificar el tipo de cursor. De forma predeterminada, se utiliza un cursor de solo avance, que le permite mover una fila en un momento a partir de la primera fila del conjunto de resultados hasta alcanzar el final del conjunto de resultados.  
  
Puede crear un conjunto de resultados con un cursor desplazable, que permite obtener acceso a cualquier fila del conjunto de resultados, en cualquier orden. En la tabla siguiente enumera los valores que pueden pasarse a la **Scrollable** opción en sqlsrv_query o sqlsrv_prepare.  
  
|Opción|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|Permite mover una fila en un momento a partir de la primera fila del conjunto de resultados hasta alcanzar el final del conjunto de resultados.<br /><br />Este es el tipo de cursor predeterminado.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) devuelve un error para conjuntos de resultados creados con este tipo de cursor.<br /><br />**reenviar** es la forma abreviada de SQLSRV_CURSOR_FORWARD.|  
|SQLSRV_CURSOR_STATIC|Permite acceder a las filas en cualquier orden, pero no reflejará los cambios en la base de datos.<br /><br />**estática** es la forma abreviada de SQLSRV_CURSOR_STATIC.|  
|SQLSRV_CURSOR_DYNAMIC|Permite acceder a las filas en cualquier orden y reflejará los cambios en la base de datos.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) devuelve un error para conjuntos de resultados creados con este tipo de cursor.<br /><br />**dinámica** es la forma abreviada de SQLSRV_CURSOR_DYNAMIC.|  
|SQLSRV_CURSOR_KEYSET|Permite obtener acceso a filas en cualquier orden. Sin embargo, un cursor de conjunto de claves no actualiza el recuento de filas si se elimina una fila de la tabla (una fila eliminada se devuelve sin valores).<br /><br />**conjunto de claves** es la forma abreviada de SQLSRV_CURSOR_KEYSET.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|Permite obtener acceso a filas en cualquier orden. Crea una consulta de cursor de cliente.<br /><br />**almacenamiento en búfer** es la forma abreviada de SQLSRV_CURSOR_CLIENT_BUFFERED.|  
  
Si una consulta genera varios conjuntos de resultados, el **Scrollable** opción se aplica a todos los conjuntos de resultados.  
  
## <a name="selecting-rows-in-a-result-set"></a>Selección de filas en un conjunto de resultados  
Después de crear un conjunto de resultados, puede usar [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md), o [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) para especificar una fila.  
  
En la tabla siguiente se describe los valores que se puede especificar en el *fila* parámetro.  
  
|Parámetro|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|Especifica la fila siguiente. Este es el valor predeterminado, si no se especifica la *fila* parámetro para un conjunto de resultados desplazables.|  
|SQLSRV_SCROLL_PRIOR|Especifica la fila antes de la fila actual.|  
|SQLSRV_SCROLL_FIRST|Especifica la primera fila del conjunto de resultados.|  
|SQLSRV_SCROLL_LAST|Especifica la última fila del conjunto de resultados.|  
|SQLSRV_SCROLL_ABSOLUTE|Especifica la fila especificada con el *desplazamiento* parámetro.|  
|SQLSRV_SCROLL_RELATIVE|Especifica la fila especificada con el *desplazamiento* parámetro de la fila actual.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>Cursores de servidor y el controlador SQLSRV  
En el ejemplo siguiente se muestra el efecto de los distintos cursores. En línea 33 del ejemplo, verá el primero de tres instrucciones de consulta que especifique los cursores diferentes.  Dos de las instrucciones de consulta se incluyen comentarios. Cada vez que ejecute el programa, use un tipo de cursor diferente para ver el efecto de la actualización de la base de datos en línea 47.  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>Cursores del lado cliente y el controlador SQLSRV  
Cursores del lado cliente son una característica agregada en la versión 3.0 de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] que permite almacenar en caché un completo conjunto de resultados en memoria. Recuento de filas está disponible después de la consulta se ejecuta cuando se utiliza un cursor de cliente.  
  
Los cursores de cliente deben usarse para conjuntos de resultados pequeño a mediano. Usar cursores de servidor para grandes conjuntos de resultados.  
  
Una consulta devolverá false si el búfer no es lo suficientemente grande como para contener el conjunto de resultados completo. Puede aumentar el tamaño del búfer hasta el límite de memoria PHP.  
  
Con el controlador SQLSRV, puede configurar el tamaño de búfer que contiene el conjunto de resultados con la configuración de ClientBufferMaxKBSize de [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) devuelve el valor de ClientBufferMaxKBSize. También puede establecer el tamaño máximo del búfer en el archivo php.ini con sqlsrv. ClientBufferMaxKBSize (por ejemplo, sqlsrv. ClientBufferMaxKBSize = 1024).  
  
El ejemplo siguiente se muestra:  
  
-   Recuento de filas siempre está disponible con un cursor de cliente.  
  
-   Uso de cursores de cliente y las instrucciones del lote.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
El ejemplo siguiente muestra un cursor de cliente utilizando [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable"=>SQLSRV_CURSOR_CLIENT_BUFFERED));  
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  

