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
manager: jroth
ms.openlocfilehash: 48c9955733672699e16cb4a00e28fa2f59717b80
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797087"
---
# <a name="support-for-localdb"></a>Compatibilidad con LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB es una versión ligera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha estado disponible desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. En este tema se describe cómo conectarse a una base de datos en una instancia de LocalDB.

## <a name="remarks"></a>Notas

Para obtener más información sobre LocalDB, incluido cómo instalar LocalDB y configurar la instancia de LocalDB, vea el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tema de libros en pantalla en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB.

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

    A continuación es una cadena de conexión de ejemplo PDO_SQLSRV:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Si fuera necesario, puede crear una instancia de LocalDB con sqllocaldb.exe. También puede utilizar sqlcmd.exe para agregar y modificar las bases de datos de una instancia de LocalDB. Por ejemplo, `sqlcmd -S (localdb)\v11.0`. (Cuando se ejecuta en IIS, deberá ejecutar bajo la cuenta correcta para obtener los mismos resultados que al ejecutar la línea de comandos; consulte [usar LocalDB con IIS completo, parte 2: la propiedad de instancia](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) para obtener más información.)

Estas son cadenas de conexión de ejemplo con el controlador SQLSRV que se conectan a una base de datos en una instancia denominada myInstance con nombre de LocalDB:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Estas son cadenas de conexión de ejemplo mediante el controlador PDO_SQLSRV que se conectan a una base de datos en una instancia denominada myInstance con nombre de LocalDB:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Para obtener instrucciones acerca de cómo instalar LocalDB, vea el [LocalDB documentación](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Si usa sqlcmd.exe para modificar datos en la instancia de LocalDB, necesitará el [utilidad sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte también

[Conexión al servidor](../../connect/php/connecting-to-the-server.md)
