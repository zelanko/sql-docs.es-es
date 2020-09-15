---
title: Protección de contenedores de Docker de SQL Server
description: Comprenda las distintas formas de proteger contenedores de Docker de SQL Server y cómo puede ejecutar contenedores como otro usuario no raíz en el host
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 10d2eb061a4ee6d9ff9c8d0594561667dd882dc9
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511617"
---
# <a name="secure-sql-server-docker-containers"></a>Protección de contenedores de Docker de SQL Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

De forma predeterminada, los contenedores de SQL Server 2017 se inician como el usuario raíz. Esto puede dar lugar a problemas de seguridad. En este artículo se describen las opciones de seguridad que tiene al ejecutar contenedores de Docker de SQL Server y cómo crear un contenedor de SQL Server como un usuario no raíz.

## <a name="build-and-run-non-root-sql-server-2017-containers"></a><a id="buildnonrootcontainer"></a> Compilación y ejecución de contenedores no raíz de SQL Server 2017

Siga los pasos siguientes para compilar un contenedor de SQL Server 2017 que se inicie como el usuario `mssql` (no raíz).

> [!NOTE]
> Los contenedores de SQL Server 2019 se inician automáticamente como no raíz, por lo que los siguientes pasos solo se aplican a los contenedores de SQL Server 2017, que se inician como raíz de forma predeterminada.

1. Descargue el [dockerfile de ejemplo para el contenedor de SQL Server no raíz](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile) y guárdelo como `dockerfile`.

2. Ejecute el comando siguiente en el contexto del directorio del dockerfile para compilar el contenedor de SQL Server no raíz:

    ```bash
    cd <path to dockerfile>
    docker build -t 2017-latest-non-root .
    ```

3. Inicie el contenedor.

    ```bash
    docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
    ```

    > [!NOTE]
    > La marca `--cap-add SYS_PTRACE` es obligatoria para que los contenedores de SQL Server no raíz generen volcados con fines de solución de problemas.

4. Compruebe que el contenedor se ejecuta como usuario no raíz:

    ```bash
    docker exec -it sql1 bash
    ```

    Ejecute `whoami`, que devolverá el usuario que se ejecuta en el contenedor.
    
    ```bash
    whoami
    ```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a> Ejecución del contenedor como otro usuario no raíz en el host

Para ejecutar el contenedor de SQL Server como otro usuario no raíz, agregue la marca -u al comando docker run. El contenedor no raíz tiene la restricción de que se debe ejecutar como parte del grupo raíz a menos que el volumen se monte en `/var/opt/mssql` con acceso para el usuario no raíz. El grupo raíz no concede ningún permiso de raíz adicional al usuario no raíz.

#### <a name="run-as-a-user-with-a-uid-4000"></a>Ejecutar como usuario con un UID 4000

Puede iniciar SQL Server con un UID personalizado. Por ejemplo, el comando siguiente inicia SQL Server con el UID 4000:

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> Asegúrese de que el contenedor de SQL Server tiene un usuario con nombre como "mssql" o "root", o SQLCMD no se podrá ejecutar dentro del contenedor. Puede comprobar si el contenedor de SQL Server se ejecuta como un usuario con nombre mediante la ejecución de `whoami` en el contenedor.

#### <a name="run-the-non-root-container-as-the-root-user"></a>Ejecutar el contenedor no raíz como el usuario raíz

Si es necesario, puede ejecutar el contenedor no raíz como el usuario raíz. Esto también concedería de forma automática todos los permisos de archivo al contenedor porque tiene un privilegio más alto.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-user-on-your-host-machine"></a>Ejecutar como un usuario en el equipo host

Puede iniciar SQL Server con un usuario existente en el equipo host con el comando siguiente:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-different-user-and-group"></a>Ejecutar como otro usuario y grupo

Puede iniciar SQL Server con un grupo y un usuario personalizados. En este ejemplo, el volumen montado tiene permisos configurados para el usuario o grupo en el equipo host.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a> Configuración de permisos de almacenamiento persistentes para contenedores no raíz

Para permitir que el usuario no raíz acceda a los archivos de base de datos que se encuentran en volúmenes montados, asegúrese de que el usuario o grupo en el que se ejecuta el contenedor pueda leer o escribir en el almacenamiento de archivos persistente.  

Puede obtener la propiedad actual de los archivos de base de datos con este comando.

```bash
ls -ll <database file dir>
```

Ejecute uno de los comandos siguientes si SQL Server no tiene acceso a los archivos de base de datos persistentes.

#### <a name="grant-the-root-group-rw-access-to-the-db-files"></a>Conceder al grupo raíz acceso de lectura y escritura a los archivos de base de datos

Conceda al grupo raíz permisos a los directorios siguientes para que el contenedor de SQL Server no raíz tenga acceso a los archivos de base de datos.

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

#### <a name="set-the-non-root-user-as-the-owner-of-the-files"></a>Establecimiento del usuario no raíz como el propietario de los archivos

Puede ser el usuario no raíz predeterminado o cualquier otro usuario no raíz que quiera especificar. En este ejemplo, se establece el UID 10001 como usuario no raíz.

```bash
chown -R 10001:0 <database file dir>
```

## <a name="next-steps"></a>Pasos siguientes

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- Para empezar a trabajar con imágenes de contenedor de SQL Server 2017 en Docker, revise el [inicio rápido](quickstart-install-connect-docker.md?view=sql-server-2017)

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- Para empezar a trabajar con imágenes de contenedor de SQL Server 2019 en Docker, revise el [inicio rápido](quickstart-install-connect-docker.md?view=sql-server-ver15)

::: moniker-end

- [Implementación y conexión a contenedores de Docker de SQL Server](sql-server-linux-docker-container-deployment.md)

- [Referencia de la configuración y personalización adicionales para contenedores de Docker](sql-server-linux-docker-container-configure.md)

- [Solución de problemas de contenedores de Docker de SQL Server](sql-server-linux-docker-container-troubleshooting.md)