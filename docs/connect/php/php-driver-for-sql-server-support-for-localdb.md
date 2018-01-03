---
title: Controlador PHP para SQL Server Support for LocalDB | Documentos de Microsoft
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: drivers
ms.component: php
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4dcf9e36eb3928bc606053bdfda441520155864a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="php-driver-for-sql-server-support-for-localdb"></a>Controlador PHP para el soporte de SQL Server para LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

A partir de [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], una versión ligera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], denominada LocalDB, estará disponible. En este tema se describe cómo conectarse a una base de datos en una instancia de LocalDB.

## <a name="remarks"></a>Comentarios

Para obtener más información sobre LocalDB, incluido cómo instalar LocalDB y configurar la instancia de LocalDB, vea el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tema libros en pantalla en [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB.

En resumen, LocalDB permite:

-   Usar **sqllocaldb.exe i** para detectar el nombre de la instancia predeterminada.

-   Usar la palabra clave de la cadena de conexión de **AttachDBFilename** para especificar a qué el archivo de base de datos se debe adjuntar el servidor. Al utilizar **AttachDBFilename**, si no especifica el nombre de la base de datos con la palabra clave de la cadena de conexión **Database** , la base de datos se quitará de la instancia de LocalDB cuando se cierre la aplicación.

-   Especifique una instancia de LocalDB en la cadena de conexión. Por ejemplo, aquí es una cadena de conexión de ejemplo SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    A continuación es una cadena de conexión de PDO_SQLSRV de ejemplo:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Si fuera necesario, puede crear una instancia de LocalDB con sqllocaldb.exe. También puede utilizar sqlcmd.exe para agregar y modificar las bases de datos de una instancia de LocalDB. Por ejemplo, `sqlcmd -S (localdb)\v11.0`. (Cuando se ejecuta en IIS, debe ejecutar en la cuenta correcta para obtener los mismos resultados que al ejecutar la línea de comandos; vea [usar LocalDB con IIS completo, parte 2: propiedad de instancia](http://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) para obtener más información.)

Éstos son cadenas de conexión de ejemplo con el controlador SQLSRV que se conectan a una base de datos en una instancia denominada myInstance con nombre de LocalDB:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Las siguientes cadenas de conexión de ejemplo utilizando el controlador PDO_SQLSRV que se conectan a una base de datos en una instancia denominada myInstance con nombre de LocalDB son:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Puede descargar LocalDB de la [página de paquete de características de SQL Server 2012](http://go.microsoft.com/fwlink/?LinkID=236805), o desde el [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express edition. Si va a usar sqlcmd.exe para modificar datos en la instancia de LocalDB, necesitará sqlcmd de [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], que puede acceder desde la descarga de las utilidades de línea de comandos en el [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] página Feature Pack.

## <a name="see-also"></a>Vea también

[Conexión al servidor](../../connect/php/connecting-to-the-server.md)
