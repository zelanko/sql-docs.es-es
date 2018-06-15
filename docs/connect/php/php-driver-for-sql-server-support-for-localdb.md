---
title: Compatibilidad con LocalDB | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 438802c4645ff3acdc1bed42af22e4e32786e1d0
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308754"
---
# <a name="support-for-localdb"></a>Compatibilidad con LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB es una versión ligera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que ha estado disponible desde [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. En este tema se describe cómo conectarse a una base de datos en una instancia de LocalDB.

## <a name="remarks"></a>Notas

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

Para obtener instrucciones acerca de cómo instalar LocalDB, vea el [LocalDB documentación](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Si usa sqlcmd.exe para modificar datos en la instancia de LocalDB, necesitará la [utilidad sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Vea también

[Conexión al servidor](../../connect/php/connecting-to-the-server.md)
