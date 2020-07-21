---
title: Compatibilidad del controlador PHP con LocalDB
description: Obtenga información sobre cómo los controladores de Microsoft de PHP para SQL Server admiten conexiones con las instancias de base de datos LocalDB.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d618706cd05796079904c971cdf7b0c32485c1d4
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886292"
---
# <a name="support-for-localdb"></a>Compatibilidad con LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB es una versión ligera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha estado disponible desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. En este tema se describe cómo conectarse a una base de datos en una instancia de LocalDB.

## <a name="remarks"></a>Observaciones

Para más información sobre LocalDB, incluido cómo instalar LocalDB y configurar la instancia de LocalDB, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tema sobre Express LocalDB de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

En resumen, LocalDB permite:

-   Usar **sqllocaldb.exe i** para detectar el nombre de la instancia predeterminada.

-   Usar la palabra clave de la cadena de conexión de **AttachDBFilename** para especificar a qué el archivo de base de datos se debe adjuntar el servidor. Al utilizar **AttachDBFilename**, si no especifica el nombre de la base de datos con la palabra clave de la cadena de conexión **Database** , la base de datos se quitará de la instancia de LocalDB cuando se cierre la aplicación.

-   Especifique una instancia de LocalDB en la cadena de conexión. Por ejemplo, aquí hay una cadena de conexión SQLSRV de muestra:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Lo siguiente es una cadena de conexión PDO_SQLSRV de ejemplo:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Si fuera necesario, puede crear una instancia de LocalDB con sqllocaldb.exe. También puede utilizar sqlcmd.exe para agregar y modificar las bases de datos de una instancia de LocalDB. Por ejemplo, `sqlcmd -S (localdb)\v11.0`. (Cuando realiza la ejecución en IIS, debe hacerlo en la cuenta correcta para obtener los mismos resultados que cuando realiza la ejecución en la línea de comandos; consulte [Uso de LocalDB con Full IIS, parte 2: propiedad de instancias](/archive/blogs/sqlexpress/using-localdb-with-full-iis-part-2-instance-ownership) para más información).

Las siguientes son cadenas de conexión de ejemplo que utilizan el controlador SQLSRV que se conecta a una base de datos en una instancia con nombre de LocalDB llamada myInstance:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Las siguientes son cadenas de conexión de ejemplo que utilizan el controlador PDO_SQLSRV que se conecta a una base de datos en una instancia con nombre de LocalDB llamada myInstance:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Para instrucciones sobre la instalación de LocalDB, consulte la [documentación de LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Si usa sqlcmd.exe para modificar datos en su instancia de LocalDB, necesitará la [utilidad sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte también

[Conexión al servidor](../../connect/php/connecting-to-the-server.md)
