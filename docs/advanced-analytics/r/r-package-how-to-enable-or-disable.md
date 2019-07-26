---
title: Habilitar o deshabilitar la administración remota de paquetes de R
description: Habilitar la administración remota de paquetes de R en SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (in-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9cc08b1227751559ea509838fe8fc3a446296770
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470025"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Habilitar o deshabilitar la administración remota de paquetes para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo habilitar la administración remota de paquetes de R desde una estación de trabajo cliente o una Machine Learning Server diferente. Una vez habilitada la característica de administración de paquetes en SQL Server, puede usar comandos de RevoScaleR en un cliente para instalar paquetes en SQL Server.

> [!NOTE]
> Actualmente se admite la administración de bibliotecas de R; la compatibilidad con Python está en el mapa de ruta.

De forma predeterminada, la característica de administración de paquetes externos para SQL Server está deshabilitada. Debe ejecutar un script independiente para habilitar la característica como se describe en la sección siguiente.

## <a name="overview-of-process-and-tools"></a>Información general sobre el proceso y las herramientas

Para habilitar o deshabilitar la administración de paquetes en SQL Server, use la utilidad de línea de comandos **RegisterRExt. exe**, que se incluye con el paquete **RevoScaleR** .

La [habilitación](#bkmk_enable) de esta característica es un proceso de dos pasos, que requiere un administrador de base de datos: habilite la administración de paquetes en la instancia de SQL Server (una vez por instancia de SQL Server) y, a continuación, habilite la administración de paquetes en la base de datos SQL (una vez por SQL Server base de datos ).

[Deshabilitar](#bkmk_disable) la característica de administración de paquetes también requiere pasos de multipel: se quitan los paquetes y permisos de nivel de base de datos (una vez por base de datos) y, a continuación, se quitan los roles del servidor (una vez por instancia).

## <a name="bkmk_enable"></a>Habilitar la administración de paquetes

1. En SQL Server, abra un símbolo del sistema con privilegios elevados y navegue hasta la carpeta que contiene la utilidad RegisterRExt. exe. La ubicación predeterminada es `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Ejecute el siguiente comando y proporcione los argumentos adecuados para su entorno:

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando crea objetos de nivel de instancia en el SQL Server equipo que son necesarios para la administración de paquetes. También reinicia Launchpad para la instancia.

    Si no especifica una instancia, se usa la instancia predeterminada. Si no especifica un usuario, se usa el contexto de seguridad actual. Por ejemplo, el siguiente comando habilita la administración de paquetes en la instancia de en la ruta de acceso de RegisterRExt. exe, con las credenciales del usuario que abrió el símbolo del sistema:

    `REgisterRExt.exe /install pkgmgmt`

3. Para agregar administración de paquetes a una base de datos específica, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando crea algunos artefactos de base de datos, incluidos los siguientes roles de base de datos que se `rpkgs-users`usan `rpkgs-private`para controlar `rpkgs-shared`los permisos de usuario:, y.

    Por ejemplo, el siguiente comando habilita la administración de paquetes en la base de datos, en la instancia donde se ejecuta RegisterRExt. Si no especifica un usuario, se usa el contexto de seguridad actual.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. Repita el comando para cada base de datos en la que se deben instalar los paquetes.

5. Para comprobar que los nuevos roles se han creado correctamente, en SQL Server Management Studio, haga clic en la base de datos, expanda **seguridad**y, a continuación, expanda **roles de base de datos**.

    También puede ejecutar una consulta en sys. database_principals como la siguiente:

    ```sql
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

Después de habilitar esta característica, puede usar la función RevoScaleR para instalar o desinstalar paquetes desde un cliente remoto de R.

## <a name="bkmk_disable"></a>Deshabilitar la administración de paquetes

1. Desde un símbolo del sistema con privilegios elevados, vuelva a ejecutar la utilidad RegisterRExt y deshabilite la administración de paquetes en el nivel de base de datos:

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita los objetos de base de datos relacionados con la administración de paquetes de la base de datos especificada. También quita todos los paquetes que se instalaron desde la ubicación del sistema de archivos protegida en el equipo SQL Server.

2. Repita este comando en cada base de datos donde se usó la administración de paquetes.

3.  Opta Una vez que se han desactivado todas las bases de datos de los paquetes que usan el paso anterior, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita la característica de administración de paquetes de la instancia de. Es posible que tenga que reiniciar manualmente el servicio Launchpad una vez más para ver los cambios.

## <a name="next-steps"></a>Pasos siguientes

+ [Uso de RevoScaleR para instalar nuevos paquetes de R](use-revoscaler-to-manage-r-packages.md)
+ [Sugerencias para la instalación de paquetes de R](packages-installed-in-user-libraries.md)
+ [Paquetes predeterminados](../package-management/default-packages.md)
