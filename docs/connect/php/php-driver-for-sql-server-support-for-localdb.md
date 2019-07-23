---
title: Compatibilidad con LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6da7f1aed956c8b2f5c71496c9c121f6006eabb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935958"
---
# <a name="support-for-localdb"></a>Compatibilidad con LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB es una versión ligera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está disponible desde. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] En este tema se describe cómo conectarse a una base de datos en una instancia de LocalDB.

## <a name="remarks"></a>Notas

Para obtener más información acerca de LocalDB, incluido cómo instalar LocalDB y configurar la instancia de LocalDB, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vea el tema de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] los libros en pantalla de Express LocalDB.

En Resumen, LocalDB permite:

-   Usar **sqllocaldb.exe i** para detectar el nombre de la instancia predeterminada.

-   Usar la palabra clave de la cadena de conexión de **AttachDBFilename** para especificar a qué el archivo de base de datos se debe adjuntar el servidor. Al utilizar **AttachDBFilename**, si no especifica el nombre de la base de datos con la palabra clave de la cadena de conexión **Database** , la base de datos se quitará de la instancia de LocalDB cuando se cierre la aplicación.

-   Especifique una instancia de LocalDB en la cadena de conexión. Por ejemplo, este es un ejemplo de cadena de conexión SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    A continuación se muestra una cadena de conexión de PDO_SQLSRV de ejemplo:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Si fuera necesario, puede crear una instancia de LocalDB con sqllocaldb.exe. También puede utilizar sqlcmd.exe para agregar y modificar las bases de datos de una instancia de LocalDB. Por ejemplo, `sqlcmd -S (localdb)\v11.0`. (Cuando se ejecuta en IIS, debe ejecutarse en la cuenta correcta para obtener los mismos resultados que cuando se ejecuta en la línea de comandos; vea [usar LocalDB con IIS completo, parte 2: propiedad](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) de la instancia para obtener más información).

A continuación se muestran cadenas de conexión de ejemplo que usan el controlador SQLSRV que se conecta a una base de datos en una instancia con nombre de LocalDB denominada instanceof:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

A continuación se muestran cadenas de conexión de ejemplo que usan el controlador PDO_SQLSRV que se conecta a una base de datos en una instancia con nombre de LocalDB denominada instanceof:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Para obtener instrucciones sobre la instalación de LocalDB, vea la [documentación de LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Si usa sqlcmd. exe para modificar los datos de la instancia de LocalDB, necesitará la [utilidad SQLCMD](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte también

[Conexión al servidor](../../connect/php/connecting-to-the-server.md)
