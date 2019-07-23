---
title: Opciones de configuración para SQL Server en Docker
description: Explore las distintas formas de usar e interactuar con las imágenes de contenedor de vista previa SQL Server 2017 y 2019 en Docker. Esto incluye la persistencia de datos, la copia de archivos y la solución de problemas.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: d24bb3566195c71a3b62d16fab867ab5085404b7
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388377"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configuración de SQL Server imágenes de contenedor en Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar y usar la [imagen de contenedor de MSSQL-Server-Linux](https://hub.docker.com/_/microsoft-mssql-server) con Docker. Esta imagen se compone de SQL Server, que se ejecuta en un sistema Linux basado en Ubuntu 16.04. Se puede usar junto al motor de Docker 1.8 o versiones posteriores en Linux, o bien en Docker en Mac y Windows.

> [!NOTE]
> Este artículo se centra específicamente en el uso de la imagen MSSQL-Server-Linux. La imagen de Windows no está incluida, pero puede obtener más información en la [Página MSSQL-Server-Windows Docker Hub](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

Para extraer y ejecutar las imágenes de contenedor de Docker para SQL Server 2017 y SQL Server versión preliminar 2019, siga los requisitos previos y los pasos descritos en la guía de inicio rápido siguiente:

- [Ejecución de la imagen de contenedor de SQL Server 2017 con Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Ejecutar la imagen de contenedor de vista previa de SQL Server 2019 con Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

En este artículo de configuración se proporcionan escenarios de uso adicionales en las secciones siguientes.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a>Ejecutar imágenes de contenedor basadas en RHEL

Toda la documentación sobre SQL Server las imágenes de contenedor de Linux apunta a contenedores basados en Ubuntu. A partir de SQL Server vista previa de 2019, puede usar contenedores basados en Red Hat Enterprise Linux (RHEL). Cambie el repositorio de contenedores de **MCR.Microsoft.com/MSSQL/Server:2019-CTP3.1-Ubuntu** a **MCR.Microsoft.com/MSSQL/RHEL/Server:2019-CTP3.1** en todos los comandos de Docker.

Por ejemplo, el comando siguiente extrae el contenedor de vista previa SQL Server 2019 más reciente que usa RHEL:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a>Ejecutar imágenes de contenedor de producción

En la guía de inicio rápido de la sección anterior se ejecuta la edición gratuita Developer de SQL Server de Docker Hub. La mayor parte de la información sigue siendo aplicable si desea ejecutar imágenes de contenedor de producción, como las ediciones Enterprise, Standard o Web. Sin embargo, hay algunas diferencias que se describen aquí.

- Solo puede usar SQL Server en un entorno de producción si tiene una licencia válida. Puede obtener una licencia de producción gratuita SQL Server Express [aquí](https://go.microsoft.com/fwlink/?linkid=857693). Las licencias de SQL Server Standard y Enterprise Edition están disponibles a través de [licencias por volumen de Microsoft](https://www.microsoft.com/licensing/default.aspx).


- También se puede configurar la imagen de contenedor para desarrolladores para ejecutar las ediciones de producción. Siga estos pasos para ejecutar las ediciones de producción:

Revise los requisitos y ejecute los procedimientos en la guía de [Inicio rápido](quickstart-install-connect-docker.md). Debe especificar la edición de producción con la variable de entorno **MSSQL_PID** . En el ejemplo siguiente se muestra cómo ejecutar la imagen de contenedor de SQL Server 2017 más reciente para la edición Enterprise:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d store/microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "store/microsoft/mssql-server-linux:2017-latest"
 ```

> [!IMPORTANT]
> Al pasar el valor **Y** a la variable de entorno **ACCEPT_EULA** y un valor de edición a **MSSQL_PID**, está expresando que tiene una licencia válida y existente para la edición y la versión de SQL Server que piensa usar. También acepta que el uso de SQL Server software que se ejecuta en una imagen de contenedor de Docker se regirá por los términos de la licencia de SQL Server.

> [!NOTE]
> Para obtener una lista completa de los posibles valores de **MSSQL_PID**, consulte [configuración de SQL Server con variables de entorno en Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Conexión y consulta

Puede conectarse y consultar SQL Server en un contenedor desde fuera del contenedor o desde dentro del contenedor. En las siguientes secciones se explican ambos escenarios. 

### <a name="tools-outside-the-container"></a>Herramientas fuera del contenedor

Puede conectarse a la instancia de SQL Server en el equipo de Docker desde cualquier herramienta externa de Linux, Windows o macOS que admita conexiones de SQL. Algunas herramientas comunes son:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) en Windows](sql-server-linux-manage-ssms.md)

En el ejemplo siguiente se usa **sqlcmd** para conectarse a SQL Server que se ejecuta en un contenedor de Docker. La dirección IP de la cadena de conexión es la dirección IP del equipo host que ejecuta el contenedor.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Si asignó un puerto de host que no era el valor predeterminado **1433**, agréguelo a la cadena de conexión. Por ejemplo, si especificó `-p 1400:1433` en el `docker run` comando, establezca de forma explícita el puerto 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Herramientas dentro del contenedor

A partir de SQL Server vista previa de 2017, las [herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md) se incluyen en la imagen de contenedor. Si se asocia a la imagen con un símbolo del sistema interactivo, puede ejecutar las herramientas de forma local.

1. Use el comando `docker exec -it` para iniciar un shell de Bash interactivo dentro de su contenedor en ejecución. En el ejemplo `e69e056c702d` siguiente, se trata del identificador del contenedor.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > No siempre tiene que especificar el identificador completo del contenedor. Solo tiene que especificar suficientes caracteres para identificarlo de forma única. Por lo tanto, en este ejemplo, podría ser suficiente `e6` para `e69` usar o en lugar del identificador completo.

2. Una vez dentro del contenedor, conecte localmente con sqlcmd. Tenga en cuenta que SQLCMD no está en la ruta de acceso de forma predeterminada, por lo que debe especificar la ruta de acceso completa.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Cuando termine con SQLCMD, escriba `exit`.

4. Cuando termine con el símbolo del sistema interactivo, escriba `exit`. El contenedor continuará ejecutándose después de salir del shell de Bash interactivo.

## <a name="run-multiple-sql-server-containers"></a>Ejecutar varios contenedores de SQL Server

Docker proporciona una manera de ejecutar varios contenedores de SQL Server en el mismo equipo host. Este es el enfoque para los escenarios que requieren varias instancias de SQL Server en el mismo host. Cada contenedor debe exponerse en un puerto diferente.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En el ejemplo siguiente se crean dos contenedores SQL Server 2017 y se asignan a los puertos **1401** y **1402** en el equipo host.

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

En el ejemplo siguiente se crean dos contenedores de SQL Server Preview 2019 y se asignan a los puertos **1401** y **1402** en el equipo host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

Ahora hay dos instancias de SQL Server que se ejecutan en contenedores independientes. Los clientes pueden conectarse a cada instancia de SQL Server mediante la dirección IP del host de Docker y el número de puerto del contenedor.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a>Crear un contenedor personalizado

Es posible crear su propio [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) para crear un contenedor de SQL Server personalizado. Para obtener más información, vea [una demostración que combina SQL Server y una aplicación de nodo](https://github.com/twright-msft/mssql-node-docker-demo-app). Si crea su propio Dockerfile, tenga en cuenta el proceso en primer plano, ya que este proceso controla la vida del contenedor. Si se cierra, se cerrará el contenedor. Por ejemplo, si desea ejecutar un script e iniciar SQL Server, asegúrese de que el proceso de SQL Server sea el más adecuado. Todos los demás comandos se ejecutan en segundo plano. Esto se muestra en el siguiente comando dentro de un Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Si invirtió los comandos en el ejemplo anterior, el contenedor se cerrará cuando se complete el script do-my-sql-commands.sh.

## <a id="persist"></a>Conservar los datos

Los cambios de configuración de SQL Server y los archivos de base de datos se conservan en el contenedor aunque `docker stop` se `docker start`reinicie el contenedor con y. Sin embargo, si quita el contenedor con `docker rm`, se elimina todo el contenedor, incluidos SQL Server y las bases de datos. En la siguiente sección se explica cómo usar **volúmenes de datos** para conservar los archivos de base de datos incluso si se eliminan los contenedores asociados.

> [!IMPORTANT]
> Por SQL Server, es fundamental que comprenda la persistencia de los datos en Docker. Además de la explicación de esta sección, consulte la documentación de Docker sobre [Cómo administrar datos en contenedores de Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montaje de un directorio host como volumen de datos

La primera opción consiste en montar un directorio en el host como un volumen de datos en el contenedor. Para ello, use el `docker run` comando con la `-v <host directory>:/var/opt/mssql` marca. Esto permite restaurar los datos entre las ejecuciones del contenedor.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

Esta técnica también le permite compartir y ver los archivos en el host fuera de Docker.

> [!IMPORTANT]
> En este momento no se admite la asignación de volumen de host para Docker en Mac con la imagen de SQL Server en Linux. En su lugar, use contenedores de volumen de datos. Esta restricción es específica del `/var/opt/mssql` directorio. La lectura desde un directorio montado funciona correctamente. Por ejemplo, puede montar un directorio host mediante-v en Mac y restaurar una copia de seguridad desde un archivo. bak que resida en el host.

### <a name="use-data-volume-containers"></a>Uso de contenedores de volúmenes de datos

La segunda opción consiste en usar un contenedor de volúmenes de datos. Puede crear un contenedor de volúmenes de datos especificando un nombre de volumen en lugar de un directorio host con `-v` el parámetro. En el ejemplo siguiente se crea un volumen de datos compartido denominado **sqlvolume**.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

> [!NOTE]
> Esta técnica para crear de forma implícita un volumen de datos en el comando ejecutar no funciona con versiones anteriores de Docker. En ese caso, use los pasos explícitos que se describen en la documentación de Docker, [creación y montaje de un contenedor de volúmenes de datos](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Incluso si detiene y quita este contenedor, el volumen de datos persiste. Puede verlo con el `docker volume ls` comando.

```bash
docker volume ls
```

Si después crea otro contenedor con el mismo nombre de volumen, el nuevo contenedor usará el mismo SQL Server datos contenidos en el volumen.

Para quitar un contenedor de volúmenes de datos, `docker volume rm` use el comando.

> [!WARNING]
> Si elimina el contenedor de volúmenes de datos, cualquier SQL Server datos del contenedor se eliminará de *forma permanente* .

### <a name="backup-and-restore"></a>Copia de seguridad y restauración

Además de estas técnicas de contenedor, también puede usar las técnicas estándar SQL Server copias de seguridad y restauración. Puede usar archivos de copia de seguridad para proteger los datos o para trasladarlos a otra instancia de SQL Server. Para obtener más información, consulte [copia de seguridad y restauración de bases de datos de SQL Server en Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Si crea copias de seguridad, asegúrese de crear o copiar los archivos de copia de seguridad fuera del contenedor. De lo contrario, si se quita el contenedor, también se eliminan los archivos de copia de seguridad.

## <a name="execute-commands-in-a-container"></a>Ejecutar comandos en un contenedor

Si tiene un contenedor en ejecución, puede ejecutar comandos dentro del contenedor desde un terminal del host.

Para obtener el identificador de contenedor, ejecute:

```bash
docker ps
```

Para iniciar un terminal bash en el contenedor, ejecute:

```bash
docker exec -it <Container ID> /bin/bash
```

Ahora puede ejecutar comandos como si los estuviera ejecutando en el terminal dentro del contenedor. Cuando termine, escriba `exit`. Esto se cierra en la sesión de comandos interactiva, pero el contenedor continúa ejecutándose.

## <a name="copy-files-from-a-container"></a>Copiar archivos de un contenedor

Para copiar un archivo del contenedor, use el siguiente comando:

```bash
docker cp <Container ID>:<Container path> <host path>
```

**Ejemplo:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>Copiar archivos en un contenedor

Para copiar un archivo en el contenedor, use el siguiente comando:

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**Ejemplo:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a id="tz"></a>Configurar la zona horaria

Para ejecutar SQL Server en un contenedor de Linux con una zona horaria específica, configure la variable de entorno **TZ** . Para buscar el valor de zona horaria correcto, ejecute el comando **tzselect** desde un símbolo del sistema de Linux Bash:

```bash
tzselect
```

Después de seleccionar la zona horaria, **tzselect** muestra una salida similar a la siguiente:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

Puede usar esta información para establecer la misma variable de entorno en el contenedor de Linux. En el ejemplo siguiente se muestra cómo ejecutar SQL Server en un contenedor de `Americas/Los_Angeles` la zona horaria:

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
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

## <a id="tags"></a>Ejecución de una imagen de contenedor de SQL Server específica

Hay escenarios en los que es posible que no desee usar la imagen de contenedor de SQL Server más reciente. Para ejecutar una determinada imagen de contenedor de SQL Server, siga estos pasos:

1. Identifique la **etiqueta** de Docker para la versión que desea usar. Para ver las etiquetas disponibles, consulte [la página MSSQL-Server-Linux Docker Hub](https://hub.docker.com/_/microsoft-mssql-server).

2. Extraiga la imagen del contenedor de SQL Server con la etiqueta. Por ejemplo, para extraer la imagen RC1, reemplace `<image_tag>` en el siguiente comando con `rc1`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Para ejecutar un nuevo contenedor con esa imagen, especifique el nombre de la etiqueta `docker run` en el comando. En el siguiente comando, reemplace `<image_tag>` por la versión que desea ejecutar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Estos pasos también se pueden usar para degradar un contenedor existente. Por ejemplo, puede que desee revertir o degradar un contenedor en ejecución para solucionar problemas o realizar pruebas. Para degradar un contenedor en ejecución, debe usar una técnica de persistencia para la carpeta de datos. Siga los mismos pasos descritos en la [sección de actualización](#upgrade), pero especifique el nombre de etiqueta de la versión anterior al ejecutar el nuevo contenedor.

## <a id="version"></a>Comprobar la versión del contenedor

Si desea conocer la versión de SQL Server en un contenedor de Docker en ejecución, ejecute el siguiente comando para mostrarlo. Reemplazar `<Container ID or name>` por el identificador o el nombre del contenedor de destino. Reemplace `<YourStrong!Passw0rd>` por el SQL Server contraseña para el inicio de sesión de SA.

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

También puede identificar la versión de SQL Server y el número de compilación de una imagen de contenedor de Docker de destino. El siguiente comando muestra la versión de SQL Server y la información de compilación de la imagen **Microsoft/MSSQL-Server-Linux: 2017-latest** . Para ello, ejecuta un nuevo contenedor con una variable de entorno **PAL_PROGRAM_INFO = 1**. El contenedor resultante se cierra al instante y el `docker rm` comando lo quita.

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

## <a id="upgrade"></a>Actualización SQL Server en contenedores

Para actualizar la imagen de contenedor con Docker, primero identifique la etiqueta de la versión de la actualización. Extraiga esta versión del registro con el `docker pull` comando:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Esto actualiza la imagen de SQL Server para los nuevos contenedores que cree, pero no actualiza SQL Server en ningún contenedor en ejecución. Para ello, debe crear un nuevo contenedor con la imagen de contenedor de SQL Server más reciente y migrar los datos a ese nuevo contenedor.

1. Asegúrese de que usa una de las [técnicas de persistencia de datos](#persist) para el contenedor de SQL Server existente. Esto le permite iniciar un nuevo contenedor con los mismos datos.

1. Detenga el contenedor de SQL Server con `docker stop` el comando.

1. Cree un nuevo contenedor de SQL Server `docker run` con y especifique un directorio de host asignado o un contenedor de volúmenes de datos. Asegúrese de usar la etiqueta específica para la actualización de SQL Server. El nuevo contenedor usa ahora una nueva versión de SQL Server con los datos de SQL Server existentes.

   > [!IMPORTANT]
   > La actualización solo se admite entre RC1, RC2 y GA en este momento.

1. Compruebe las bases de datos y los datos en el nuevo contenedor.

1. Opcionalmente, quite el contenedor anterior con `docker rm`.

## <a id="troubleshooting"></a> Solucionar problemas

En las secciones siguientes se proporcionan sugerencias para la solución de problemas de ejecución de SQL Server en contenedores.

### <a name="docker-command-errors"></a>Errores de comando de Docker

Si obtiene errores para los `docker` comandos, asegúrese de que el servicio Docker se está ejecutando e intente ejecutar con permisos elevados.

Por ejemplo, en Linux, podría recibir el siguiente error al ejecutar `docker` comandos:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Si recibe este error en Linux, intente ejecutar los mismos comandos precedidos de `sudo`. Si se produce un error, compruebe que el servicio Docker se está ejecutando e inícielo si es necesario.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

En Windows, compruebe que está iniciando PowerShell o el símbolo del sistema como administrador.

### <a name="sql-server-container-startup-errors"></a>Errores de inicio del contenedor de SQL Server

Si no se puede ejecutar el contenedor de SQL Server, pruebe las siguientes pruebas:

- Si recibe un error como **"no se pudo crear el punto de conexión CONTAINER_NAME en el puente de red. Error al iniciar el proxy: escucha TCP 0.0.0.0:1433 enlace: la dirección ya está en uso. '** , está intentando asignar el puerto del contenedor 1433 a un puerto que ya está en uso. Esto puede ocurrir si está ejecutando SQL Server localmente en el equipo host. También puede ocurrir si inicia dos contenedores de SQL Server e intenta asignarlos al mismo puerto de host. Si esto ocurre, use el `-p` parámetro para asignar el puerto del contenedor 1433 a un puerto de host diferente. Por ejemplo: 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

::: moniker-end

- Si recibe un error como **"se denegó el permiso al intentar conectarse al socket de demonio de Docker en Unix:///var/run/Docker.sock: Obtener http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial UNIX/var/run/Docker.sock: Connect: Permission** denegado al intentar iniciar un contenedor y, a continuación, agregue el usuario al grupo de Docker en Ubuntu. Después, cierre la sesión y vuelva a iniciarla, ya que este cambio afectará a las nuevas sesiones. 

   ```bash
    usermod -aG docker $USER
    ```
- Compruebe si hay algún mensaje de error del contenedor.

    ```bash
    docker logs e69e056c702d
    ```

- Asegúrese de que cumple los requisitos mínimos de memoria y disco especificados en la sección de [requisitos previos](quickstart-install-connect-docker.md#requirements) del artículo de inicio rápido.

- Si usa software de administración de contenedores, asegúrese de que admite procesos de contenedor que se ejecutan como raíz. El proceso Sqlservr en el contenedor se ejecuta como raíz.

- Revise la [configuración de SQL Server y los registros de errores](#errorlogs).

### <a name="enable-dump-captures"></a>Habilitar capturas de volcado

Si se produce un error en el proceso de SQL Server dentro del contenedor, debe crear un nuevo contenedor con **SYS_PTRACE** habilitado. Esto agrega la capacidad de Linux para realizar el seguimiento de un proceso, que es necesario para crear un archivo de volcado de memoria en una excepción. La compatibilidad puede utilizar el archivo de volcado para ayudar a solucionar el problema. El siguiente comando de Docker Run habilita esta funcionalidad.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server errores de conexión

Si no puede conectarse a la instancia de SQL Server que se ejecuta en el contenedor, pruebe las siguientes pruebas:

- Asegúrese de que el contenedor de SQL Server se está ejecutando examinando la columna **Estado** de `docker ps -a` la salida. Si no es así `docker start <Container ID>` , use para iniciarlo.

- Si ha asignado a un puerto de host no predeterminado (no 1433), asegúrese de que está especificando el puerto en la cadena de conexión. Puede ver la asignación de puerto en la columna **puertos** de la `docker ps -a` salida. Por ejemplo, el siguiente comando conecta SQLCMD a un contenedor que escucha en el puerto 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Si usa `docker run` con un volumen de datos asignado o un contenedor de volúmenes de datos existente, SQL Server omite el `MSSQL_SA_PASSWORD`valor de. En su lugar, se usa la contraseña de usuario SA preconfigurada de los SQL Server datos del contenedor de volúmenes de datos o de volúmenes de datos. Compruebe que está utilizando la contraseña de SA asociada a los datos a los que está adjuntando.

- Revise la [configuración de SQL Server y los registros de errores](#errorlogs).

### <a name="sql-server-availability-groups"></a>SQL Server grupos de disponibilidad

Si usa Docker con SQL Server grupos de disponibilidad, hay dos requisitos adicionales.

- Asigne el puerto que se usa para la comunicación de réplica (valor predeterminado 5022). Por ejemplo, especifique `-p 5022:5022` como parte `docker run` del comando.

- Establezca explícitamente el nombre `-h YOURHOSTNAME` `docker run` de host del contenedor con el parámetro del comando. Este nombre de host se usa al configurar el grupo de disponibilidad. Si no lo especifica `-h`, el valor predeterminado es el identificador del contenedor.

### <a id="errorlogs"></a>SQL Server de la instalación y los registros de errores

Puede consultar el SQL Server la instalación y los registros de errores en **/var/opt/MSSQL/log**. Si el contenedor no se está ejecutando, primero inicie el contenedor. A continuación, use un símbolo del sistema interactivo para inspeccionar los registros.

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
> Si montó un directorio host en **/var/opt/MSSQL** al crear el contenedor, en su lugar, puede buscar en el subdirectorio de **registro** de la ruta de acceso asignada en el host.

## <a name="next-steps"></a>Pasos siguientes

Para empezar a trabajar con SQL Server 2017 imágenes de contenedor en Docker, vaya a través de la guía de [Inicio rápido](quickstart-install-connect-docker.md).

Además, consulte el [repositorio de github MSSQL-Docker](https://github.com/Microsoft/mssql-docker) para ver los recursos, comentarios y problemas conocidos.

[Explore la alta disponibilidad para contenedores de SQL Server](sql-server-linux-container-ha-overview.md)
