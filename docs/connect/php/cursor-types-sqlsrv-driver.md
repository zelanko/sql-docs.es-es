---
title: Tipos de cursor (controlador SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac090ad8831397bf31c0911ab8a8db21486528db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015114"
---
# <a name="cursor-types-sqlsrv-driver"></a>Tipos de cursor (controlador SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

El controlador SQLSRV permite crear un conjunto de resultados con filas a las que se puede acceder en cualquier orden según el tipo de cursor.  En este tema se explican los cursores del lado cliente (almacenados en búfer) y de servidor (no almacenados en búfer).  
  
## <a name="cursor-types"></a>Tipos de cursor  
Cuando se crea un conjunto de resultados con [sqlsrv_query](../../connect/php/sqlsrv-query.md) o con [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md), se puede especificar el tipo de cursor. De forma predeterminada, se usa un cursor de solo avance, que permite desplazar una fila cada vez a partir de la primera fila del conjunto de resultados hasta llegar al final del conjunto de resultados.  
  
Puede crear un conjunto de resultados con un cursor desplazable, que le permite tener acceso a cualquier fila del conjunto de resultados, en cualquier orden. En la tabla siguiente se enumeran los valores que se pueden pasar a la opción **desplazable** en sqlsrv_query o sqlsrv_prepare.  
  
|Opción|Descripción|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|Permite desplazar una fila cada vez a partir de la primera fila del conjunto de resultados hasta llegar al final del conjunto de resultados.<br /><br />Este es el tipo de cursor predeterminado.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) devuelve un error para los conjuntos de resultados creados con este tipo de cursor.<br /><br />**Forward** es la forma abreviada de SQLSRV_CURSOR_FORWARD.|  
|SQLSRV_CURSOR_STATIC|Permite tener acceso a las filas en cualquier orden, pero no reflejará los cambios en la base de datos.<br /><br />**static** es la forma abreviada de SQLSRV_CURSOR_STATIC.|  
|SQLSRV_CURSOR_DYNAMIC|Permite tener acceso a las filas en cualquier orden y reflejará los cambios en la base de datos.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) devuelve un error para los conjuntos de resultados creados con este tipo de cursor.<br /><br />**Dynamic** es la forma abreviada de SQLSRV_CURSOR_DYNAMIC.|  
|SQLSRV_CURSOR_KEYSET|Permite acceder a las filas en cualquier orden. Pero los cursores de conjunto de claves no actualizan el recuento de filas si se elimina una fila de la tabla (las filas eliminadas se devuelven sin valores).<br /><br />**Keyset** es la forma abreviada de SQLSRV_CURSOR_KEYSET.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|Permite acceder a las filas en cualquier orden. Crea una consulta de cursor del lado cliente.<br /><br />**almacenado en búfer** es la forma abreviada de SQLSRV_CURSOR_CLIENT_BUFFERED.|  
  
Si una consulta genera varios conjuntos de resultados, la opción **desplazable** se aplica a todos los conjuntos de resultados.  
  
## <a name="selecting-rows-in-a-result-set"></a>Seleccionar filas en un conjunto de resultados  
Después de crear un conjunto de resultados, puede usar [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)o [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) para especificar una fila.  
  
En la tabla siguiente se describen los valores que se pueden especificar en el parámetro *Row* .  
  
|Parámetro|Descripción|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|Especifica la siguiente fila. Este es el valor predeterminado si no se especifica el parámetro *Row* para un conjunto de resultados desplazable.|  
|SQLSRV_SCROLL_PRIOR|Especifica la fila anterior a la fila actual.|  
|SQLSRV_SCROLL_FIRST|Especifica la primera fila del conjunto de resultados.|  
|SQLSRV_SCROLL_LAST|Especifica la última fila del conjunto de resultados.|  
|SQLSRV_SCROLL_ABSOLUTE|Especifica la fila especificada con el parámetro *offset* .|  
|SQLSRV_SCROLL_RELATIVE|Especifica la fila especificada con el parámetro *offset* de la fila actual.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>Cursores del lado servidor y el controlador SQLSRV  
En el ejemplo siguiente se muestra el efecto de los distintos cursores. En la línea 33 del ejemplo, verá la primera de tres instrucciones de consulta que especifican cursores diferentes.  Dos de las instrucciones de consulta están comentadas. Cada vez que ejecute el programa, use un tipo de cursor diferente para ver el efecto de la actualización de la base de datos en la línea 47.  
  
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
Los cursores del lado cliente son una característica agregada en la versión [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3,0 del que permite almacenar en caché un conjunto de resultados completo en la memoria. El recuento de filas está disponible después de ejecutar la consulta cuando se usa un cursor del lado cliente.  
  
Los cursores del lado cliente deben usarse para conjuntos de resultados de tamaño pequeño a mediano. Utilice cursores del lado servidor para grandes conjuntos de resultados.  
  
Una consulta devolverá FALSE si el búfer no es lo suficientemente grande como para contener todo el conjunto de resultados. Puede aumentar el tamaño del búfer hasta el límite de memoria PHP.  
  
Con el controlador SQLSRV, puede configurar el tamaño del búfer que contiene el conjunto de resultados con la configuración ClientBufferMaxKBSize para [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) devuelve el valor de ClientBufferMaxKBSize. También puede establecer el tamaño máximo del búfer en el archivo php. ini con sqlsrv. ClientBufferMaxKBSize (por ejemplo, sqlsrv. ClientBufferMaxKBSize = 1024).  
  
En el ejemplo siguiente se muestra:  
  
-   El recuento de filas siempre está disponible con un cursor del lado cliente.  
  
-   Uso de cursores del lado cliente e instrucciones por lotes.  
  
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
  
En el ejemplo siguiente se muestra un cursor del lado cliente mediante [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) y un tamaño de búfer de cliente diferente.
  
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
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
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
  
## <a name="see-also"></a>Consulte también  
[Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
