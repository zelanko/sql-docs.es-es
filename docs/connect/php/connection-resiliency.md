---
title: Resistencia de conexión inactiva
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: 34d4bc2342397f5809ef16ef59ed342d6c86d421
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460380"
---
# <a name="idle-connection-resiliency"></a>Resistencia de conexión inactiva
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Resistencia de conexión](https://msdn.microsoft.com/library/dn632678.aspx) es el principio que una conexión inactiva interrumpida hacerse, dentro de determinadas restricciones. Si se produce un error en una conexión a Microsoft SQL Server, la resistencia de conexión permite al cliente intentará automáticamente restablecer la conexión. Resistencia de conexión es una propiedad del origen de datos; solo SQL Server 2014 y versiones posterior y Azure SQL Database compatible con la resistencia de conexión.

Resistencia de la conexión se implementa con dos palabras clave de conexión que se pueden agregar a cadenas de conexión: **ConnectRetryCount** y **ConnectRetryInterval**.

|Palabra clave|Valores|Valor predeterminado|Descripción|
|-|-|-|-|
|**ConnectRetryCount**| Número entero comprendido entre 0 y 255 (ambos inclusive)|1|El número máximo de intentos para restablecer una conexión interrumpida antes de desistir. De forma predeterminada, se realiza un intento único para restablecer una conexión cuando ha interrumpido. Un valor de 0 significa que no se intentará ninguna reconexión.|
|**ConnectRetryInterval**| Número entero comprendido entre 1 y 60 (inclusive)|1| El tiempo, en segundos, entre los intentos para restablecer una conexión. La aplicación intentará volver a conectarse inmediatamente al detectar una conexión interrumpida y, a continuación, esperará **ConnectRetryInterval** segundos antes de intentarlo de nuevo. Esta palabra clave se omite si **ConnectRetryCount** es igual a 0.

Si el producto de **ConnectRetryCount** multiplicado por **ConnectRetryInterval** es mayor que **LoginTimeout**, a continuación, el cliente dejará de intentar conectarse una vez  **LoginTimeout** se alcanza; en caso contrario, continuará volver a conectar hasta **ConnectRetryCount** se alcanza.

#### <a name="remarks"></a>Notas

Resistencia de la conexión se aplica cuando la conexión está inactiva. Que se produzcan durante la ejecución de una transacción, por ejemplo, no se activarán los intentos de reconexión: producirá un error como se esperaría en caso contrario. Las situaciones siguientes, que se conoce como estados de sesión no se puede recuperar, desencadenarán intentos de reconexión:

* Tablas temporales
* Cursores globales y locales
* Bloqueos de transacciones de nivel de contexto de transacción y sesión
* Bloqueos de aplicaciones
* EXECUTE AS / REVERTIR el contexto de seguridad
* Identificadores de automatización OLE
* Identificadores XML preparados
* Marcas de seguimiento

## <a name="example"></a>Ejemplo

El siguiente código se conecta a una base de datos y ejecuta una consulta. Se interrumpe la conexión mediante la eliminación de la sesión y se intenta una nueva consulta mediante la conexión rota. En este ejemplo se utiliza la base de datos de ejemplo [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx).

En este ejemplo, especificamos un cursor almacenado en búfer antes de interrumpir la conexión. Si no se especifica un cursor almacenado en búfer, ¿no se puede restablecer la conexión ya que sería un cursor de servidor activo y, por tanto, podría no estar inactiva la conexión cuando ha interrumpido. Sin embargo, en ese caso, podríamos llamar a sqlsrv_free_stmt() antes de interrumpir la conexión para que deje vacante el cursor y, ¿se puede restablecer correctamente la conexión.

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
Resultado esperado:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>Ver también
[Resistencia de conexión en el controlador Windows ODBC](https://docs.microsoft.com/sql/connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver)
