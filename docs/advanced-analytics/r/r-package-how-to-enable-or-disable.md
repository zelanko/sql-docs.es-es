---
title: "Habilitar o deshabilitar la administración de paquetes de R para SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 35bcae1e29e9b640d2e04b9adc788e382b18b6e8
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>Habilitar o deshabilitar la administración de paquetes de R para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe una nueva característica de administración de paquetes de SQL Server de 2017, diseñado para permitir que el Administrador de base de datos controlar la instalación del paquete en la instancia mediante T-SQL, en lugar de R.

Más arde que el frature de administración de paquetes está habilitada, también puede usar comandos de R para instalar paquetes en un frm de base de datos un cliente remoto.

> [!NOTE]
> De forma predeterminada, está deshabilitada la característica de administración de paquetes externos para SQL Server, incluso si se instalaron características de aprendizaje de la máquina. 

## <a name="enable-package-management"></a>Habilitar la administración de paquetes

Para [habilitar](#bkmk_enable) esta característica es un proceso de dos pasos, que requieren un administrador de base de datos:

1.  Habilitar la administración de paquetes en la instancia de SQL Server (una vez por instancia de SQL Server)

2.  Habilitar la administración de paquetes en la base de datos SQL (una vez por base de datos SQL Server)

Para [deshabilitar](#bkmk_disable) la característica de administración de paquetes, invertir el proceso para quitar paquetes de nivel de base de datos y los permisos y, a continuación, quite los roles del servidor:

1.  Deshabilitar la administración de paquetes en cada base de datos (una vez por base de datos)

2.  Deshabilitar la administración de paquetes en la instancia de SQL Server (una vez por instancia)

## <a name="bkmk_enable"></a>Habilitar la administración de paquetes

Para habilitar o deshabilitar la administración de paquetes, use la utilidad de línea de comandos **RegisterRExt.exe**, que se incluye con la **RevoScaleR** paquete.

1. Abra un símbolo del sistema con privilegios elevados y vaya a la carpeta que contiene la utilidad, RegisterRExt.exe. La ubicación predeterminada es `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Ejecute el siguiente comando, que proporciona los argumentos apropiados para su entorno:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando crea objetos de nivel de instancia en el equipo de SQL Server que son necesarios para la administración de paquetes. También se reinicia el Launchpad de la instancia.

    Si no especifica una instancia, se utiliza la instancia predeterminada. Si no especifica un usuario, se utiliza el contexto de seguridad actual. Por ejemplo, el siguiente comando habilita la administración de paquetes en la instancia en la ruta de acceso de RegisterRExt.exe, utilizando las credenciales del usuario que abrió el símbolo del sistema:

    `REgisterRExt.exe /installpkgmgmt`

2.  Para agregar administración de paquetes a una base de datos, ejecute el comando siguiente desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando crea algunos artefactos de base de datos, incluidos los siguientes roles de base de datos que se usan para controlar los permisos de usuario: `rpkgs-users`, `rpkgs-private`, y `rpkgs-shared`.

    Por ejemplo, el siguiente comando habilita la administración de paquetes en la base de datos en la instancia donde se ejecuta RegisterRExt. Si no especifica un usuario, se utiliza el contexto de seguridad actual. 

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

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

4.  Después de que se ha habilitado la característica, puede conectarse al servidor e instalar o sincronizar los paquetes de forma remota, mediante comandos de R. Para obtener un ejemplo de cómo funciona esto, consulte [instalar paquetes adicionales en SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="bkmk_disable"></a>Deshabilitar la administración de paquetes

1.  Desde un símbolo del sistema con privilegios elevados, vuelva a ejecutar la utilidad RegisterRExt y deshabilitar la administración de paquetes en el nivel de base de datos:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita los objetos de base de datos relacionados con administración de paquetes de la base de datos especificada. También se quitan todos los paquetes que se instalaron desde la ubicación de sistema de archivos protegidos en el equipo de SQL Server.

2. Ejecute este comando una vez para cada base de datos donde se utiliza la administración de paquetes. 

3.  (Opcional) Después de que se han borrado todas las bases de datos de paquetes mediante el paso anterior, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita la característica de administración de paquetes de la instancia. Tendrá que reiniciar manualmente el servicio Launchpad una vez más para ver los cambios.

## <a name="see-also"></a>Vea también

[Administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md)
