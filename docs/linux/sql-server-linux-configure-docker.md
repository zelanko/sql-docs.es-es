---
title: Opciones de configuración de SQL Server en Docker
description: Explore las distintas formas de usar las imágenes de contenedor de SQL Server 2017 y 2019 en Docker e interactuar con ellas. Esto incluye conservar los datos, copiar archivos y solucionar problemas.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/08/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: e97f535dedd2b6ee25abfc886d1f08272697c549
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287509"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configuración de imágenes de contenedor de SQL Server en Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar y usar la [imagen de contenedor mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) con Docker. 

Para otros escenarios de implementación, consulte:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes: clústeres de macrodatos](../big-data-cluster/deploy-get-started.md)

Esta imagen se compone de SQL Server, que se ejecuta en un sistema Linux basado en Ubuntu 16.04. Se puede usar junto al motor de Docker 1.8 o versiones posteriores en Linux, o bien en Docker en Mac y Windows.

> [!NOTE]
> En este artículo, nos centraremos específicamente en el uso de la imagen mssql-server-linux. No trataremos la imagen de Windows, pero puede obtener más información sobre ella en la [página mssql-server-windows de Docker Hub](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

> [!IMPORTANT]
> Antes de elegir la ejecución de un contenedor de SQL Server para casos de uso de producción, revise la [directiva de compatibilidad de contenedores de SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) para garantizar que se ejecuta una configuración compatible.

En este vídeo de 6 minutos se muestra una introducción a la ejecución de SQL Server en contenedores:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]


## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

Para extraer y ejecutar las imágenes de contenedor de Docker para SQL Server 2017 y SQL Server 2019, siga los requisitos previos y los pasos descritos en las siguientes guías de inicio rápido:

- [Inicio rápido: Ejecución de imágenes de contenedor de SQL Server con Docker](quickstart-install-connect-docker.md?view=sql-server-2017) (SQL Server 2017)
- [Ejecución de imágenes de contenedor de SQL Server 2019 con Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

En este artículo de configuración se proporcionan escenarios de uso adicionales en las secciones siguientes.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="run-rhel-based-container-images"></a><a id="rhel"></a> Ejecución de imágenes de contenedor basadas en RHEL

La documentación sobre las imágenes de contenedor de SQL Server en Linux apunta a contenedores basados en Ubuntu. A partir de SQL Server 2019, puede usar contenedores basados en Red Hat Enterprise Linux (RHEL). Cambie el repositorio de contenedores de **mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04** a **mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8** en todos los comandos de Docker.

Por ejemplo, el comando siguiente extrae la actualización acumulativa 1 para el contenedor de SQL Server 2019 que usa RHEL 8:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="run-production-container-images"></a><a id="production"></a> Ejecución de imágenes de contenedor de producción

En la guía de inicio rápido de la sección anterior se ejecuta la edición para desarrolladores gratuita de SQL Server de Docker Hub. La mayor parte de la información sigue siendo aplicable si quiere ejecutar imágenes de contenedor de producción, como las ediciones Enterprise, Standard o Web. Pero hay algunas diferencias que se describen aquí.

- Solo puede usar SQL Server en un entorno de producción si tiene una licencia válida. Puede obtener una licencia de producción gratuita de SQL Server Express [aquí](https://go.microsoft.com/fwlink/?linkid=857693). Las licencias de SQL Server Standard y Enterprise Edition están disponibles a través de [licencias por volumen de Microsoft](https://www.microsoft.com/licensing/default.aspx).


- La imagen de contenedor para desarrolladores también se puede configurar para que ejecute las ediciones de producción. Siga estos pasos para ejecutar las ediciones de producción:

Revise los requisitos y ejecute los procedimientos de la [guía de inicio rápido](quickstart-install-connect-docker.md). Debe especificar la edición de producción con la variable de entorno **MSSQL_PID**. En el ejemplo siguiente se muestra cómo ejecutar la imagen de contenedor de SQL Server 2017 más reciente para la Enterprise Edition:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "mcr.microsoft.com/mssql/server:2017-latest"
```

> [!IMPORTANT]
> Al pasar el valor **Y** a la variable de entorno **ACCEPT_EULA** y un valor de edición a **MSSQL_PID**, está expresando que tiene una licencia válida y existente para la edición y la versión de SQL Server que va a utilizar. También acepta que el uso del software de SQL Server que se ejecuta en una imagen de contenedor de Docker se regirá por los términos de la licencia de SQL Server.

> [!NOTE]
> Para obtener una lista completa de los posibles valores de **MSSQL_PID**, vea [Configuración de opciones de SQL Server con variables de entorno en Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Conexión y consultas

Puede conectarse a SQL Server y realizar consultas en un contenedor desde fuera o desde dentro del contenedor. En las siguientes secciones se explican ambos escenarios. 

### <a name="tools-outside-the-container"></a>Herramientas fuera del contenedor

Puede conectarse a la instancia de SQL Server en la máquina de Docker desde cualquier herramienta externa de Linux, Windows o Mac OS que admita conexiones de SQL. Algunas herramientas comunes son:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) en Windows](sql-server-linux-manage-ssms.md)

En el ejemplo siguiente se usa **sqlcmd** para conectarse a una instancia de SQL Server que se ejecuta en un contenedor de Docker. La dirección IP de la cadena de conexión es la dirección IP del equipo host que ejecuta el contenedor.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Si asignó un puerto de host distinto del valor predeterminado **1433**, agréguelo a la cadena de conexión. Por ejemplo, si especificó `-p 1400:1433` en el comando `docker run`, establezca de forma explícita el puerto 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Herramientas dentro del contenedor

A partir de SQL Server 2017, las [herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md) se incluyen en la imagen de contenedor. Si se asocia a la imagen con un símbolo del sistema interactivo, puede ejecutar las herramientas de forma local.

1. Use el comando `docker exec -it` para iniciar un shell de Bash interactivo dentro de su contenedor en ejecución. En el ejemplo siguiente, `e69e056c702d` es el identificador del contenedor.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > No siempre tiene que especificar el identificador completo del contenedor. Solo tiene que especificar suficientes caracteres para identificarlo de forma única. Por lo tanto, en este ejemplo, podría ser suficiente usar `e6` o `e69` en lugar del identificador completo.

2. Una vez dentro del contenedor, conecte localmente con sqlcmd. Tenga en cuenta que sqlcmd no está en la ruta de acceso de forma predeterminada, por lo que deberá especificar la ruta de acceso completa.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Cuando termine con sqlcmd, escriba `exit`.

4. Cuando termine con el símbolo del sistema interactivo, escriba `exit`. El contenedor continuará ejecutándose después de salir del shell de Bash interactivo.

## <a name="run-multiple-sql-server-containers"></a>Ejecución de varios contenedores de SQL Server

Docker proporciona una manera de ejecutar varios contenedores de SQL Server en el mismo equipo host. Use este enfoque para escenarios en los que se requieran varias instancias de SQL Server en el mismo host. Cada contenedor debe exponerse en un puerto diferente.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En el ejemplo siguiente se crean dos contenedores de SQL Server 2017 y se asignan a los puertos **1401** y **1402** en el equipo host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En el ejemplo siguiente se crean dos contenedores de SQL Server 2019 y se asignan a los puertos **1401** y **1402** en el equipo host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

Ahora hay dos instancias de SQL Server que se ejecutan en contenedores independientes. Los clientes pueden conectarse a cada instancia de SQL Server mediante la dirección IP del host de Docker y el número de puerto del contenedor.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a name="create-a-customized-container"></a><a id="customcontainer"></a> Creación de un contenedor personalizado

Es posible crear su propio [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) para crear un contenedor de SQL Server personalizado. Para obtener más información, vea [una demostración que combina SQL Server y una aplicación de nodo](https://github.com/twright-msft/mssql-node-docker-demo-app). Si crea su propio Dockerfile, tenga en cuenta el proceso en primer plano, ya que este proceso controla la vida del contenedor. Si se cierra, se cerrará el contenedor. Por ejemplo, si desea ejecutar un script e iniciar SQL Server, asegúrese de que el proceso de SQL Server sea el más adecuado. Todos los demás comandos se ejecutan en segundo plano. El comando siguiente ilustra esto dentro de un Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Si invirtió los comandos en el ejemplo anterior, el contenedor se cerrará cuando se complete el script do-my-sql-commands.sh.

## <a name="persist-your-data"></a><a id="persist"></a> Conservación de los datos

Los cambios de configuración de SQL Server y los archivos de base de datos se conservan en el contenedor aunque se reinicie el contenedor con `docker stop` y `docker start`. Pero si quita el contenedor con `docker rm`, se elimina todo el contenedor, incluidos SQL Server y las bases de datos. En la siguiente sección se explica cómo usar **volúmenes de datos** para conservar los archivos de base de datos incluso si se eliminan los contenedores asociados.

> [!IMPORTANT]
> Por SQL Server, es fundamental que comprenda la persistencia de los datos en Docker. Además de la explicación de esta sección, consulte la documentación de Docker sobre [cómo administrar datos en contenedores de Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montaje de un directorio host como volumen de datos

La primera opción consiste en montar un directorio en el host como un volumen de datos en el contenedor. Para ello, use el comando `docker run` con la marca `-v <host directory>:/var/opt/mssql`. Esto permite restaurar los datos entre las ejecuciones del contenedor.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

Esta técnica también le permite compartir y ver los archivos en el host fuera de Docker.

> [!IMPORTANT]
> La asignación de volúmenes de host para **Docker en Windows** no admite actualmente la asignación del directorio completo de `/var/opt/mssql`. Pero puede asignar un subdirectorio, como `/var/opt/mssql/data`, a su equipo host.

> [!IMPORTANT]
> En este momento no se admite la asignación de volumen de host para **Docker en Mac** con la imagen de SQL Server en Linux. En su lugar, use contenedores de volúmenes de datos. Esta restricción es específica del directorio `/var/opt/mssql`. La lectura desde un directorio montado funciona correctamente. Por ejemplo, puede montar un directorio host mediante -v en Mac y restaurar una copia de seguridad desde un archivo .bak que resida en el host.

### <a name="use-data-volume-containers"></a>Uso de contenedores de volúmenes de datos

La segunda opción consiste en usar un contenedor de volúmenes de datos. Puede crear un contenedor de volúmenes de datos especificando un nombre de volumen en lugar de un directorio host con el parámetro `-v`. En el ejemplo siguiente se crea un volumen de datos compartidos denominado **sqlvolume**.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

> [!NOTE]
> Esta técnica para crear de forma implícita un volumen de datos en el comando de ejecución no funciona con versiones anteriores de Docker. En ese caso, use los pasos explícitos que se describen en la documentación de Docker, [Creación y montaje de un contenedor de volúmenes de datos](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Incluso si detiene y quita este contenedor, el volumen de datos se conserva. Puede verlo con el comando `docker volume ls`.

```bash
docker volume ls
```

Si después crea otro contenedor con el mismo nombre de volumen, el nuevo contenedor usará los mismos datos de SQL Server contenidos en el volumen.

Para quitar un contenedor de volúmenes de datos, use el comando `docker volume rm`.

> [!WARNING]
> Si elimina el contenedor de volúmenes de datos, todos los datos de SQL Server del contenedor se eliminarán *de forma permanente*.

### <a name="backup-and-restore"></a>Copia de seguridad y restauración

Además de estas técnicas de contenedor, también puede usar las técnicas estándar de copia de seguridad y restauración de SQL Server. Puede usar archivos de copia de seguridad para proteger los datos o para trasladarlos a otra instancia de SQL Server. Para obtener más información, vea [Copia de seguridad y restauración de bases de datos de SQL Server en Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Si crea copias de seguridad, asegúrese de crear o copiar los archivos de copia de seguridad fuera del contenedor. De lo contrario, si se quita el contenedor, también se eliminarán los archivos de copia de seguridad.

## <a name="execute-commands-in-a-container"></a>Ejecución de comandos en un contenedor

Si tiene un contenedor en ejecución, puede ejecutar comandos dentro del contenedor desde un terminal del host.

Para obtener el identificador de contenedor, ejecute:

```bash
docker ps
```

Para iniciar un terminal de Bash en el contenedor, ejecute:

```bash
docker exec -it <Container ID> /bin/bash
```

Ahora puede ejecutar comandos como si los estuviera ejecutando en el terminal dentro del contenedor. Cuando termine, escriba `exit`. Esto cierra la sesión de comandos interactiva, pero el contenedor continúa ejecutándose.

## <a name="copy-files-from-a-container"></a>Copia de archivos desde un contenedor

Para copiar un archivo del contenedor, use el siguiente comando:

```bash
docker cp <Container ID>:<Container path> <host path>
```

**Ejemplo**:

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>Copia de archivos en un contenedor

Para copiar un archivo en el contenedor, use el siguiente comando:

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**Ejemplo**:

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a name="configure-the-timezone"></a><a id="tz"></a> Configuración de la zona horaria

Para ejecutar SQL Server en un contenedor de Linux con una zona horaria específica, configure la variable de entorno `TZ`. Para buscar el valor de zona horaria correcto, ejecute el comando `tzselect` desde un símbolo del sistema de Bash de Linux:

```bash
tzselect
```

Después de seleccionar la zona horaria, `tzselect` muestra una salida similar a la siguiente:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

Puede usar esta información para establecer la misma variable de entorno en el contenedor de Linux. En el ejemplo siguiente se muestra cómo ejecutar SQL Server en un contenedor en la zona horaria de `Americas/Los_Angeles`:

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

## <a name="run-a-specific-sql-server-container-image"></a><a id="tags"></a> Ejecución de una imagen de contenedor de SQL Server determinada

Hay escenarios en los que es posible que no quiera usar la imagen de contenedor de SQL Server más reciente. Para ejecutar una imagen de contenedor de SQL Server determinada, siga estos pasos:

1. Identifique la **etiqueta** de Docker para la versión que quiere usar. Para ver las etiquetas disponibles, vea [la página mssql-server-linux de Docker Hub](https://hub.docker.com/_/microsoft-mssql-server).

2. Extraiga la imagen de contenedor de SQL Server con la etiqueta. Por ejemplo, para extraer la imagen RC1, reemplace `<image_tag>` en el siguiente comando por `rc1`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Para ejecutar un nuevo contenedor con esa imagen, especifique el nombre de la etiqueta en el comando `docker run`. En el siguiente comando, reemplace `<image_tag>` por la versión que quiere ejecutar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Estos pasos también se pueden usar para degradar un contenedor existente. Por ejemplo, puede que quiera revertir o degradar un contenedor en ejecución para solucionar problemas o realizar pruebas. Para degradar un contenedor en ejecución, debe usar una técnica de persistencia para la carpeta de datos. Siga los mismos pasos descritos en la [sección de actualización](#upgrade), pero especifique el nombre de etiqueta de la versión anterior al ejecutar el nuevo contenedor.

## <a name="check-the-container-version"></a><a id="version"></a> Comprobación de la versión de contenedor

Si quiere conocer la versión de SQL Server en un contenedor de Docker en ejecución, ejecute el siguiente comando para mostrarla: Reemplace `<Container ID or name>` por el identificador o el nombre del contenedor de destino. Reemplace `<YourStrong!Passw0rd>` por la contraseña de SQL Server para el inicio de sesión de SA.

```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'SELECT @@VERSION'
```

```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourStrong!Passw0rd>" `
   -Q 'SELECT @@VERSION'
```

También puede identificar la versión de SQL Server y el número de compilación de una imagen de contenedor de Docker de destino. El comando siguiente muestra la versión de SQL Server y la información de compilación de la imagen **mcr.microsoft.com/mssql/server:2017-latest**. Para ello, ejecuta un nuevo contenedor con una variable de entorno **PAL_PROGRAM_INFO=1**. El contenedor resultante se cierra al instante y el comando `docker rm` lo quita.

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti mcr.microsoft.com/mssql/server:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti mcr.microsoft.com/mssql/server:2017-latest; `
   docker rm sqlver
```

Los comandos anteriores muestran información de versión similar a la siguiente salida:

```Text
sqlservr
  Version 14.0.3029.16
  Build ID ee3d3882f1c48a7a7e590a620153012eaedc2f37143d485df945a079b9d4eeea
  Build Type release
  Git Version 65d42c4
  Built at Sat Jun 16 01:20:11 GMT 2018

PAL
  Build ID 60cfcb134bbae96d311f6a4f56aeb5a685b3809de80bcb61ec587a8f58b555eb
  Build Type release
  Git Version 21a4c11
  Built at Sat Jun 16 01:18:53 GMT 2018

Packages
  system.sfp                    6.2.9200.1,21a4c1178,
  system.common.sfp             10.0.15063.540
  system.certificates.sfp       6.2.9200.1,21a4c1178,
  system.netfx.sfp              4.6.1590.0
  secforwarderxplat.sfp         14.0.3029.16
  sqlservr.sfp                  14.0.3029.16
  sqlagent.sfp                  14.0.3029.16
```

## <a name="upgrade-sql-server-in-containers"></a><a id="upgrade"></a> Actualización de SQL Server en contenedores

Para actualizar la imagen de contenedor con Docker, primero identifique la etiqueta de la versión de la actualización. Extraiga esta versión del registro con el comando `docker pull`:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Esto actualiza la imagen de SQL Server para los nuevos contenedores que cree, pero no actualiza SQL Server en ningún contenedor en ejecución. Para ello, debe crear un nuevo contenedor con la imagen de contenedor de SQL Server más reciente y migrar los datos a ese nuevo contenedor.

1. Asegúrese de que usa una de las [técnicas de persistencia de datos](#persist) para el contenedor de SQL Server existente. Esto le permite iniciar un nuevo contenedor con los mismos datos.

1. Detenga el contenedor de SQL Server con el comando `docker stop`.

1. Cree un nuevo contenedor de SQL Server con `docker run` y especifique un directorio de host asignado o un contenedor de volúmenes de datos. Asegúrese de usar la etiqueta específica para la actualización de SQL Server. El nuevo contenedor ahora usa una nueva versión de SQL Server con los datos de SQL Server existentes.

   > [!IMPORTANT]
   > La actualización solo se admite entre RC1, RC2 y GA en este momento.

1. Compruebe las bases de datos y los datos del nuevo contenedor.

1. Opcionalmente, quite el contenedor anterior con `docker rm`.

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

Ejecute docker exec en el contenedor.
```bash
docker exec -it sql1 bash
```

Ejecute `whoami`, que devolverá el usuario que se ejecuta en el contenedor.

```bash
whoami
```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a> Ejecución del contenedor como otro usuario no raíz en el host

Para ejecutar el contenedor de SQL Server como otro usuario no raíz, agregue la marca -u al comando docker run. El contenedor no raíz tiene la restricción de que se debe ejecutar como parte del grupo raíz a menos que el volumen se monte en "/var/opt/mssql" con acceso para el usuario no raíz. El grupo raíz no concede ningún permiso de raíz adicional al usuario no raíz.

**Ejecutar como usuario con un UID 4000**

Puede iniciar SQL Server con un UID personalizado. Por ejemplo, el comando siguiente inicia SQL Server con el UID 4000:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> Asegúrese de que el contenedor de SQL Server tiene un usuario con nombre como "mssql" o "root", o SQLCMD no se podrá ejecutar dentro del contenedor. Puede comprobar si el contenedor de SQL Server se ejecuta como un usuario con nombre mediante la ejecución de `whoami` en el contenedor.

**Ejecutar el contenedor no raíz como el usuario raíz**

Puede ejecutar el contenedor no raíz como el usuario raíz si es necesario. Esto también concedería de forma automática todos los permisos de archivo al contenedor porque es un privilegio más alto.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**Ejecutar como un usuario en el equipo host**

Puede iniciar SQL Server con un usuario existente en el equipo host con el comando siguiente:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**Ejecutar como otro usuario y grupo**

Puede iniciar SQL Server con un grupo y un usuario personalizados. En este ejemplo, el volumen montado tiene permisos configurados para el usuario o grupo en el equipo host.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a> Configuración de permisos de almacenamiento persistentes para contenedores no raíz

Para permitir que el usuario no raíz acceda a los archivos de base de datos que se encuentran en volúmenes montados, asegúrese de que el usuario o grupo en el que se ejecuta el contenedor pueda acceder al almacenamiento de archivos persistente.  

Puede obtener la propiedad actual de los archivos de base de datos con este comando.

```bash
ls -ll <database file dir>
```

Ejecute uno de los comandos siguientes si SQL Server no tiene acceso a los archivos de base de datos persistentes.

**Conceder al grupo raíz acceso de lectura y escritura a los archivos de base de datos**

Conceda al grupo raíz permisos a los directorios siguientes para que el contenedor de SQL Server no raíz tenga acceso a los archivos de base de datos.

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

**Establecer el usuario no raíz como el propietario de los archivos**

Puede ser el usuario no raíz predeterminado o cualquier otro usuario no raíz que quiera especificar. En este ejemplo, se establece el UID 10001 como usuario no raíz.

```bash
chown -R 10001:0 <database file dir>
```

## <a name="change-the-default-file-location"></a><a id="changefilelocation"></a> Cambio de la ubicación predeterminada del archivo

Agregue la variable `MSSQL_DATA_DIR` para cambiar el directorio de datos en el comando `docker run` y, después, monte un volumen en esa ubicación a la que tenga acceso el usuario del contenedor.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="troubleshooting"></a><a id="troubleshooting"></a> Solucionar problemas

En las secciones siguientes se proporcionan sugerencias para la solución de problemas de ejecución de SQL Server en contenedores.

### <a name="docker-command-errors"></a>Errores de comandos de Docker

Si obtiene errores para los comandos `docker`, asegúrese de que el servicio Docker se está ejecutando e intente ejecutar con permisos elevados.

Por ejemplo, en Linux, podría recibir el siguiente error al ejecutar los comandos `docker`:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Si recibe este error en Linux, intente ejecutar los mismos comandos precedidos de `sudo`. Si se produce un error, compruebe que el servicio Docker se está ejecutando e inícielo si es necesario.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

En Windows, compruebe que está iniciando PowerShell o el símbolo del sistema como administrador.

### <a name="sql-server-container-startup-errors"></a>Errores de inicio del contenedor de SQL Server

Si no se puede ejecutar el contenedor de SQL Server, pruebe lo siguiente:

- Si recibe el error **"failed to create endpoint CONTAINER_NAME on network bridge. Error starting proxy: listen tcp 0.0.0.0:1433 bind: address already in use."** , está intentando asignar el puerto del contenedor 1433 a un puerto que ya está en uso. Esto puede ocurrir si está ejecutando SQL Server localmente en el equipo host. También puede ocurrir si inicia dos contenedores de SQL Server e intenta asignarlos al mismo puerto de host. Si esto ocurre, use el parámetro `-p` para asignar el puerto del contenedor 1433 a otro puerto de host. Por ejemplo: 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

::: moniker-end

- Si recibe el error **"Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: permission denied"** al intentar iniciar un contenedor, agregue el usuario al grupo de Docker en Ubuntu. Después, cierre la sesión y vuelva a iniciarla, ya que este cambio afectará a las nuevas sesiones. 

   ```bash
    usermod -aG docker $USER
   ```
- Compruebe si hay algún mensaje de error del contenedor.

    ```bash
    docker logs e69e056c702d
    ```

- Asegúrese de que cumple los requisitos mínimos de memoria y disco especificados en la sección de [requisitos previos](quickstart-install-connect-docker.md#requirements) del artículo de inicio rápido.

- Si usa software de administración de contenedores, asegúrese de que admite procesos de contenedor que se ejecutan como raíz. El proceso sqlservr en el contenedor se ejecuta como raíz.

- Revise la [Configuración y registros de errores de SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Habilitar capturas de volcado

Si se produce un error en el proceso de SQL Server dentro del contenedor, debe crear un contenedor nuevo con **SYS_PTRACE** habilitado. Esto agrega la capacidad de Linux para realizar el seguimiento de un proceso, que es necesario para crear un archivo de volcado de memoria en una excepción. El departamento de soporte técnico puede utilizar el archivo de volcado para ayudar a solucionar el problema. El siguiente comando de ejecución de Docker habilita esta funcionalidad.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Errores de conexión de SQL Server

Si no puede conectarse a la instancia de SQL Server que se ejecuta en el contenedor, pruebe lo siguiente:

- Asegúrese de que el contenedor de SQL Server se está ejecutando examinando la columna **STATUS** de la salida de `docker ps -a`. Si no es así, use `docker start <Container ID>` para iniciarlo.

- Si ha asignado a un puerto de host no predeterminado (no 1433), asegúrese de que está especificando el puerto en la cadena de conexión. Puede ver la asignación de puertos en la columna **PORTS** de la salida de `docker ps -a`. Por ejemplo, el siguiente comando conecta sqlcmd a un contenedor que escucha en el puerto 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Si usa `docker run` con un volumen de datos asignado o un contenedor de volúmenes de datos existentes, SQL Server ignora el valor de `MSSQL_SA_PASSWORD`. En su lugar, se usa la contraseña de usuario SA preconfigurada de los datos de SQL Server del volumen de datos o el contenedor de volúmenes de datos. Compruebe que está utilizando la contraseña de SA asociada a los datos a los que está adjuntando.

- Revise la [Configuración y registros de errores de SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Grupos de disponibilidad de SQL Server

Si usa Docker con grupos de disponibilidad de SQL Server, hay dos requisitos adicionales.

- Asignar el puerto que se usa para la comunicación de réplica (valor predeterminado 5022). Por ejemplo, especifique `-p 5022:5022` como parte del comando `docker run`.

- Establecer explícitamente el nombre de host del contenedor con el parámetro `-h YOURHOSTNAME` del comando `docker run`. Este nombre de host se usa al configurar el grupo de disponibilidad. Si no lo especifica con `-h`, el valor predeterminado es el identificador del contenedor.

### <a name="sql-server-setup-and-error-logs"></a><a id="errorlogs"></a> Configuración y registros de errores de SQL Server

Puede consultar la configuración y los registros de errores de SQL Server en **/var/opt/mssql/log**. Si el contenedor no se está ejecutando, primero inicie el contenedor. Después, use un símbolo del sistema interactivo para inspeccionar los registros.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

En la sesión de Bash dentro del contenedor, ejecute los siguientes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Si montó un directorio host en **/var/opt/mssql** al crear el contenedor, puede buscar en el subdirectorio de **registro** de la ruta de acceso asignada en el host en su lugar.

## <a name="next-steps"></a>Pasos siguientes

Para empezar a trabajar con imágenes de contenedor de SQL Server 2017 en Docker, revise la [guía de inicio rápido](quickstart-install-connect-docker.md).

También puede ver el [repositorio de GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) para ver una serie de recursos, comentarios y problemas conocidos.

[Explore la Alta disponibilidad para contenedores de SQL Server](sql-server-linux-container-ha-overview.md)
