---
title: Habilitar o deshabilitar la administración remota del paquete de R para el aprendizaje automático de SQL Server | Documentos de Microsoft
description: Habilitar la administración remota del paquete de R en SQL Server 2016 R Services o SQL Server de 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 997db094cb5e69e0cbf82d9a7e247cb13ec1d452
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707663"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Habilitar o deshabilitar la administración remota de paquetes de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo habilitar la administración remota de paquetes de R desde una estación de trabajo cliente o en otro servidor de aprendizaje de máquina. Cuando se ha habilitado la característica de administración de paquetes en SQL Server, puede usar los comandos de RevoScaleR en un cliente para instalar paquetes en SQL Server.

> [!NOTE]
> Actualmente se admite la administración de bibliotecas de R; compatibilidad con Python está dentro del plan.

De forma predeterminada, está deshabilitada la característica de administración de paquetes externos para SQL Server. Debe ejecutar un script independiente para habilitar la característica como se describe en la sección siguiente.

## <a name="overview-of-process-and-tools"></a>Información general del proceso y las herramientas

Para habilitar o deshabilitar la administración de paquetes en SQL Server, use la utilidad de línea de comandos **RegisterRExt.exe**, que se incluye con la **RevoScaleR** paquete.

[Habilitar](#bkmk_enable) esta característica es un proceso de dos pasos, que requieren un administrador de base de datos: habilitar la administración de paquetes en la instancia de SQL Server (una por cada instancia de SQL Server) y, a continuación, habilitar la administración de paquetes en la base de datos SQL (una por cada SQL Server base de datos).

[Deshabilitar](#bkmk_disable) la característica de administración de paquetes también requiere pasos de multipel: quitar paquetes de nivel de base de datos y permisos (una por cada base de datos) y, a continuación, quite los roles del servidor (una vez por instancia).

## <a name="bkmk_enable"></a> Habilitar la administración de paquetes

1. En SQL Server, abra un símbolo del sistema con privilegios elevados y vaya a la carpeta que contiene la utilidad, RegisterRExt.exe. La ubicación predeterminada es `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Ejecute el siguiente comando, que proporciona los argumentos apropiados para su entorno:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando crea objetos de nivel de instancia en el equipo de SQL Server que son necesarios para la administración de paquetes. También se reinicia el Launchpad de la instancia.

    Si no especifica una instancia, se utiliza la instancia predeterminada. Si no especifica un usuario, se utiliza el contexto de seguridad actual. Por ejemplo, el siguiente comando habilita la administración de paquetes en la instancia en la ruta de acceso de RegisterRExt.exe, utilizando las credenciales del usuario que abrió el símbolo del sistema:

    `REgisterRExt.exe /installpkgmgmt`

3. Para agregar administración de paquetes a una base de datos, ejecute el comando siguiente desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando crea algunos artefactos de base de datos, incluidos los siguientes roles de base de datos que se usan para controlar los permisos de usuario: `rpkgs-users`, `rpkgs-private`, y `rpkgs-shared`.

    Por ejemplo, el siguiente comando habilita la administración de paquetes en la base de datos en la instancia donde se ejecuta RegisterRExt. Si no especifica un usuario, se utiliza el contexto de seguridad actual.

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

4. Repita el comando para cada base de datos donde deben instalarse los paquetes.

5. Para comprobar que se han creado correctamente los nuevos roles, en SQL Server Management Studio, haga clic en la base de datos, expanda **seguridad**y expanda **Roles de base de datos**.

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

Después de haber habilitado esta característica, puede usar la función RevoScaleR para instalar o desinstalar paquetes desde un cliente remoto de R.

## <a name="bkmk_disable"></a> Deshabilitar la administración de paquetes

1. Desde un símbolo del sistema con privilegios elevados, vuelva a ejecutar la utilidad RegisterRExt y deshabilitar la administración de paquetes en el nivel de base de datos:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita los objetos de base de datos relacionados con administración de paquetes de la base de datos especificada. También se quitan todos los paquetes que se instalaron desde la ubicación de sistema de archivos protegidos en el equipo de SQL Server.

2. Repita este comando en cada base de datos donde se utiliza la administración de paquetes.

3.  (Opcional) Después de que se han borrado todas las bases de datos de paquetes mediante el paso anterior, ejecute el siguiente comando desde un símbolo del sistema con privilegios elevados:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando quita la característica de administración de paquetes de la instancia. Tendrá que reiniciar manualmente el servicio Launchpad una vez más para ver los cambios.

## <a name="next-steps"></a>Pasos siguientes

+ [Utilice RevoScaleR para instalar nuevos paquetes de R](use-revoscaler-to-manage-r-packages.md)
+ [Sugerencias para la instalación de paquetes de R](packages-installed-in-user-libraries.md)
+ [Paquetes predeterminados](installing-and-managing-r-packages.md)