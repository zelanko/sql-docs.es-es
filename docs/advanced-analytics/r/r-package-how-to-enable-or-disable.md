---
title: "Habilitar o deshabilitar la administración de paquetes de R para SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd19bc25e1e4602a54bf89e18c8959a282552f63
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>Habilitar o deshabilitar la administración de paquetes de R para SQL Server

En este artículo se describe el proceso de habilitar o deshabilitar la nueva característica de administración de paquetes en SQL Server 2017. Esta característica permite al administrador de base de datos controlar la instalación del paquete en la instancia. La característica se basa en los nuevos roles de base de datos para conceder a los usuarios la capacidad para instalar los paquetes de R necesitan o compartir paquetes con otros usuarios.

De forma predeterminada, está deshabilitada la característica de administración de paquetes externos para SQL Server, incluso si se instalaron características de aprendizaje de la máquina.

Para [habilitar](#bkmk_enable) esta característica es un proceso de dos pasos y requiere cierta ayuda de un administrador de base de datos:

1.  Habilitar la administración de paquetes en la instancia de SQL Server (una vez por instancia de SQL Server)

2.  Habilitar la administración de paquetes en la base de datos SQL (una vez por base de datos SQL Server)

Para [deshabilitar](#bkmk_disable) la característica de administración de paquetes, invertir el proceso para quitar paquetes de nivel de base de datos y los permisos y, a continuación, quite los roles del servidor:

1.  Deshabilitar la administración de paquetes en cada base de datos (una vez por base de datos)

2.  Deshabilitar la administración de paquetes en la instancia de SQL Server (una vez por instancia)

## <a name="bkmk_enable"></a>Habilitar la administración de paquetes

Para habilitar o deshabilitar la administración del paquete requiere que la utilidad de línea de comandos **RegisterRExt.exe**, que se incluye con la **RevoScaleR** paquete.

1. Abra un símbolo del sistema con privilegios elevados y vaya a la carpeta que contiene la utilidad, RegisterRExt.exe. La ubicación predeterminada es `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Ejecute el siguiente comando, proporcionar argumentos adecuado para su entorno:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando crea objetos de nivel de instancia en el equipo de SQL Server que son necesarios para la administración de paquetes. También se reinicia el Launchpad de la instancia.

    Si no especifica una instancia, se utiliza la instancia predeterminada.

    Si no especifica un usuario, se utiliza el contexto de seguridad actual.

2.  Para agregar administración de paquetes en el nivel de base de datos, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando crea algunos artefactos de base de datos, incluidos los siguientes roles de base de datos que se usan para controlar los permisos de usuario: `rpkgs-users`, `rpkgs-private`, y `rpkgs-shared`.

    Si no especifica un usuario, se utiliza el contexto de seguridad actual.

3. Repita el comando para cada base de datos donde deben instalarse los paquetes.

4.  Para comprobar que se han creado correctamente los nuevos roles, en SQL Server Management Studio, haga clic en la base de datos, expanda **seguridad**y expanda **Roles de base de datos**.

    También puede ejecutar una consulta en sys.database_principals como el siguiente:

    ```SQL
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

4.  Después de que se ha habilitado la característica, cualquier usuario con los permisos adecuados puede utilizar el [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción T-SQL para agregar paquetes. Para obtener un ejemplo de cómo funciona esto, consulte [instalar paquetes adicionales en SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="bkmk_disable"></a>Deshabilitar la administración de paquetes

1.  Desde un símbolo del sistema con privilegios elevados, ejecute el siguiente comando para deshabilitar la administración de paquetes en el nivel de base de datos:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Ejecute este comando una vez para cada base de datos donde se utiliza la administración de paquetes. Este comando quitará los objetos de base de datos relacionados con administración de paquetes de la base de datos especificada. También se quitarán todos los paquetes que se instalaron desde la ubicación de sistema de archivos protegidos en el equipo de SQL Server.

2.  (Opcional) Después de que se han borrado todas las bases de datos de paquetes mediante el paso anterior, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita la característica de administración de paquetes de la instancia.

## <a name="see-also"></a>Vea también

[Administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md)
