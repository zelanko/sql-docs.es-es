---
title: Agrupación de conexiones (controladores de Microsoft para PHP para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02db1d891f02dce9912d4cdcf78ca0166eab9c32
ms.sourcegitcommit: ef7f2540ba731cc6a648005f2773d759df5c6405
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39415484"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>Agrupación de conexiones (controladores de Microsoft para PHP para SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

A continuación, se muestran consideraciones importantes que hay tener cuenta sobre la agrupación de conexiones en los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]:  
  
-   Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] utilizan la agrupación de conexiones ODBC.  
  
-   De forma predeterminada, la agrupación de conexiones está habilitada en Windows. En Linux y macOS, las conexiones se agrupan solo si está habilitada la agrupación de conexiones para ODBC (consulte [agrupación de conexiones de habilitación o deshabilitación](#enablingdisabling-connection-pooling)). Cuando está habilitada la agrupación de conexiones y conectarse a un servidor, el controlador intenta usar una conexión agrupada antes de crear uno nuevo. Si no encuentra una conexión equivalente en el grupo, se crea una nueva conexión y se agrega al grupo. El controlador determina si las conexiones son equivalentes según una comparación de las cadenas de conexión.  
  
-   Cuando se utiliza una conexión del grupo, se restablece el estado de conexión.  
  
-   Al cerrar la conexión, la conexión vuelve al grupo.  
  
Para obtener más información sobre la agrupación de conexiones, consulte [Agrupación de conexiones de administrador de controladores](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="enablingdisabling-connection-pooling"></a>Agrupación de conexiones de habilitar/deshabilitar
### <a name="windows"></a>Windows
Puede forzar a que el controlador cree una nueva conexión en lugar de buscar una equivalente en la agrupación de conexiones mediante el establecimiento del valor del atributo *ConnectionPooling* de la cadena de conexión en **false** (o 0).  
  
Si el atributo *ConnectionPooling* se omite de la cadena de conexión, o si se establece en **True** (o 1), el controlador solo crea una nueva conexión en el caso de que no exista una equivalente en la agrupación de conexiones.  
  
Para obtener información sobre otros atributos de conexión, consulte [Connection Options](../../connect/php/connection-options.md).  
### <a name="linux-and-macos"></a>Linux y macOS
El *ConnectionPooling* atributo no puede utilizarse para habilitar o deshabilitar la agrupación de conexiones. 

Agrupación de conexiones puede habilitarse o deshabilitarse, edite el archivo de configuración de odbcinst.ini. Debe volver a cargar el controlador para que los cambios surtan efecto.

Establecer `Pooling` a `Yes` y un positivo `CPTimeout` valor en el archivo odbcinst.ini habilita la agrupación de conexiones. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
Como mínimo, el archivo odbcinst.ini debe tener un aspecto similar a este ejemplo:

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

Establecer `Pooling` a `No` en el odbcinst.ini archivo obliga al controlador para crear una nueva conexión.
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Notas
- En Linux o macOS, todas las conexiones se va a agrupar si está habilitada la agrupación en el archivo odbcinst.ini. Esto significa que la opción de conexión ConnectionPooling no tiene ningún efecto. Para deshabilitar la agrupación, conjunto Pooling = No en el archivo odbcinst.ini y volver a cargar los controladores.
  - unixODBC < = 2.3.4 (Linux y macOS) no puede devolver información de diagnóstico adecuada, como los mensajes de error, advertencias y mensajes informativos
  - por este motivo, es posible que los controladores de SQLSRV y PDO_SQLSRV no pueda recuperar correctamente datos largos (por ejemplo, xml, binario) como cadenas. Datos largos se pueden recuperar como secuencias como una solución alternativa. Consulte el ejemplo siguiente para obtener más información sobre SQLSRV.

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>Ver también  
[Conexión mediante la autenticación de Windows](../../connect/php/how-to-connect-using-windows-authentication.md)

[Conexión mediante la autenticación de SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
