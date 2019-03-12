---
title: Opciones de configuración de SQL Server en Docker | Microsoft Docs
description: Explore distintas formas de usar e interactuar con SQL Server 2017 y 2019 imágenes de contenedor de vista previa en Docker. Esto incluye datos persistentes, copia los archivos y solución de problemas.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: sql-linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 2e7d2188c8122dfcfd8f8c8fe772ef09125eca3b
ms.sourcegitcommit: c0b3b3d969af668d19b1bba04fa0c153cc8970fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/11/2019
ms.locfileid: "57756730"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configurar imágenes de contenedor de SQL Server en Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar y usar el [imagen de contenedor mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) con Docker. Esta imagen se compone de SQL Server, que se ejecuta en un sistema Linux basado en Ubuntu 16.04. Se puede usar junto al motor de Docker 1.8 o versiones posteriores en Linux, o bien en Docker en Mac y Windows.

> [!NOTE]
> En este artículo se centra específicamente sobre el uso de la imagen mssql-server-linux. No se trata la imagen de Windows, pero puede obtener más información sobre la [página de Docker Hub mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

Para extraer y ejecutar al Docker de imágenes de contenedor para la versión preliminar de SQL Server 2017 y 2019 de SQL Server, siga los requisitos previos y los pasos descritos en el tutorial siguiente:

- [Ejecutar la imagen de contenedor de SQL Server 2017 con Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Ejecutar la imagen de contenedor de vista previa de SQL Server 2019 con Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

En este artículo de configuración proporciona escenarios de uso adicionales en las secciones siguientes.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> Ejecutar imágenes de contenedor basadas en RHEL

Toda la documentación en imágenes de contenedor de SQL Server Linux de apuntar a contenedores basados en Ubuntu. A partir de la versión preliminar de SQL Server 2019, puede usar contenedores basados en Red Hat Enterprise Linux (RHEL). Cambiar el repositorio de contenedor de **mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu** a **mcr.microsoft.com/mssql/rhel/server:2019-CTP2.3** en todos los comandos de docker.

Por ejemplo, el comando siguiente extrae el contenedor de versión preliminar más reciente de SQL Server 2019 que usa RHEL:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.3
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.3
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> Ejecutar imágenes de contenedor de producción

La Guía de inicio rápido en la sección anterior ejecuta la edición gratuita de Developer de SQL Server desde Docker Hub. La mayoría de la información sigue siendo aplicable si desea ejecutar imágenes de contenedor, como las ediciones Enterprise, Standard o Web de producción. Sin embargo, hay algunas diferencias que se mencionan aquí.

- Sólo se puede utilizar SQL Server en un entorno de producción si tiene una licencia válida. Puede obtener una licencia de producción de SQL Server Express gratuita [aquí](https://go.microsoft.com/fwlink/?linkid=857693). Las licencias de SQL Server Standard y Enterprise Edition están disponibles a través de [Microsoft Volume Licensing](https://www.microsoft.com/licensing/default.aspx).


- La imagen de contenedor de desarrollador puede configurarse para ejecutar las ediciones de producción. Use los pasos siguientes para ejecutar las ediciones de producción:

Revise los requisitos y ejecutar procedimientos en el [quickstart](quickstart-install-connect-docker.md). Debe especificar la edición de producción con el **MSSQL_PID** variable de entorno. El ejemplo siguiente muestra cómo ejecutar la imagen de contenedor de SQL Server 2017 más reciente para la edición Enterprise:

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
      > By passing the value **Y** to the environment variable **ACCEPT_EULA** and an edition value to **MSSQL_PID**, you are expressing that you have a valid and existing license for the edition and version of SQL Server that you intend to use. You also agree that your use of SQL Server software running in a Docker container image will be governed by the terms of your SQL Server license.

      > [!NOTE]
      > For a full list of possible values for **MSSQL_PID**, see [Configure SQL Server settings with environment variables on Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Conectarse y realizar consultas

Puede conectarse y realizar consultas de SQL Server en un contenedor desde fuera del contenedor o desde el contenedor. Las siguientes secciones explican ambos escenarios. 

### <a name="tools-outside-the-container"></a>Herramientas fuera del contenedor

Puede conectarse a la instancia de SQL Server en la máquina de Docker desde cualquier herramienta externa de Linux, Windows o macOS que admite las conexiones de SQL. Algunas herramientas comunes incluyen:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) en Windows](sql-server-linux-manage-ssms.md)

En el ejemplo siguiente se usa **sqlcmd** para conectarse a SQL Server que se ejecuta en un contenedor de Docker. La dirección IP en la cadena de conexión es la dirección IP del equipo host que ejecuta el contenedor.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Si ha asignado un puerto de host que no era la predeterminada **1433**, agregar ese puerto a la cadena de conexión. Por ejemplo, si especificó `-p 1400:1433` en su `docker run` comando y, después, conectarse de forma explícita por especificar puerto 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Herramientas dentro del contenedor

A partir de SQL Server 2017 preview, el [herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md) se incluyen en la imagen de contenedor. Si se adjunta a la imagen con una línea de comandos interactiva, puede ejecutar las herramientas localmente.

1. Use el comando `docker exec -it` para iniciar un shell de Bash interactivo dentro de su contenedor en ejecución. En el ejemplo siguiente `e69e056c702d` es el identificador de contenedor.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > No siempre debe especificar el identificador del contenedor completo. Solo debe especificar suficientes caracteres para identificar de forma exclusiva. Por lo que en este ejemplo, podría ser suficiente para usar `e6` o `e69` en lugar del identificador completo.

2. Una vez dentro del contenedor, conecte localmente con sqlcmd. Tenga en cuenta que sqlcmd no está en la ruta de acceso de forma predeterminada, por lo que debe especificar la ruta de acceso completa.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Cuando haya terminado con sqlcmd, escriba `exit`.

4. Cuando haya terminado con la línea de comandos interactiva, escriba `exit`. El contenedor continuará ejecutándose después de salir del shell de Bash interactivo.

## <a name="run-multiple-sql-server-containers"></a>Ejecutar varios contenedores de SQL Server

Docker ofrece una manera de ejecutar varios contenedores de SQL Server en el mismo equipo host. Este es el enfoque para escenarios que requieren varias instancias de SQL Server en el mismo host. Cada contenedor debe exponer a sí mismo en un puerto diferente.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

El ejemplo siguiente crea dos contenedores de SQL Server 2017 y los asigna a los puertos **1401** y **1402** en el equipo host.

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

En el ejemplo siguiente crea dos contenedores de vista previa de SQL Server 2019 y los asigna a los puertos **1401** y **1402** en el equipo host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

::: moniker-end

Ahora hay dos instancias de SQL Server que se ejecutan en contenedores diferentes. Los clientes pueden conectarse a cada instancia de SQL Server mediante la dirección IP del host Docker y el número de puerto para el contenedor.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> Crear un contenedor personalizado

Es posible crear sus propios [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) para crear un contenedor personalizado de SQL Server. Para obtener más información, consulte [una demostración que combina SQL Server y una aplicación Node](https://github.com/twright-msft/mssql-node-docker-demo-app). Si crea su propio Dockerfile, tener en cuenta el proceso de primer plano, porque este proceso controla la vida del contenedor. Si existe, se apagará el contenedor. Por ejemplo, si desea ejecutar un script e iniciar SQL Server, asegúrese de que el proceso de SQL Server es el comando más a la derecha. Todos los demás comandos se ejecutan en segundo plano. Esto se muestra en el siguiente comando en un archivo de Docker:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Si invierte los comandos en el ejemplo anterior, el contenedor podría cierre cuando finalice el script realice-my-sql-commands.sh.

## <a id="persist"></a> Conservar los datos

Los cambios de configuración de SQL Server y los archivos de base de datos se conservan en el contenedor, incluso si reinicia el contenedor con `docker stop` y `docker start`. Sin embargo, si quita el contenedor con `docker rm`, se elimina todo en el contenedor, incluidos SQL Server y las bases de datos. La siguiente sección explica cómo usar **volúmenes de datos** para conservar los archivos de base de datos, incluso si se eliminan los contenedores asociados.

> [!IMPORTANT]
> Para SQL Server, es fundamental comprender la persistencia de datos en Docker. Además de la explicación en esta sección, consulte la documentación de Docker en [cómo administrar datos en contenedores de Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montar un directorio de host como volumen de datos

La primera opción es montar un directorio en el host como un volumen de datos en el contenedor. Para ello, utilice el `docker run` comando con el `-v <host directory>:/var/opt/mssql` marca. Esto permite que los datos que se restaurarán entre ejecuciones del contenedor.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

::: moniker-end

Esta técnica también le permite compartir y ver los archivos en el host de Docker.

> [!IMPORTANT]
> Asignación de volumen de host de Docker en Mac con SQL Server en la imagen de Linux no se admite en este momento. Use contenedores de volúmenes de datos en su lugar. Esta restricción es específica para el `/var/opt/mssql` directory. Leer un funciona bien el directorio montado. Por ejemplo, puede montar un directorio de host mediante - v en Mac y restaurar una copia de seguridad desde el archivo .bak que reside en el host.

### <a name="use-data-volume-containers"></a>Utilizar contenedores de volúmenes de datos

La segunda opción es usar un contenedor de volúmenes de datos. Puede crear un contenedor de volúmenes de datos especificando un nombre de volumen en lugar de un directorio de host con el `-v` parámetro. En el ejemplo siguiente se crea un volumen de datos compartido denominado **sqlvolume**.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```
::: moniker-end

> [!NOTE]
> Esta técnica para crear implícitamente un volumen de datos en el comando de ejecución no funciona con versiones anteriores de Docker. En ese caso, utilice los pasos explícitos descritos en la documentación de Docker, [creación y montaje de un contenedor de volúmenes de datos](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Incluso si detener y quitar este contenedor, se conserva el volumen de datos. Puede verla en el `docker volume ls` comando.

```bash
docker volume ls
```

Si, a continuación, cree otro contenedor con el mismo nombre de volumen, el nuevo contenedor utiliza los mismos datos de SQL Server incluidos en el volumen.

Para quitar un contenedor de volúmenes de datos, use el `docker volume rm` comando.

> [!WARNING]
> Si elimina el contenedor de volúmenes de datos, los datos de SQL Server en el contenedor están *permanentemente* eliminado.

### <a name="backup-and-restore"></a>Copias de seguridad y restauración

Además de estas técnicas de contenedor, también puede usar la copia de seguridad de SQL Server estándar y técnicas de restauración. Puede usar los archivos de copia de seguridad para proteger los datos o para mover los datos a otra instancia de SQL Server. Para obtener más información, consulte [copias de seguridad y restauración de SQL Server las bases de datos en Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Si crea copias de seguridad, asegúrese de crear o copiar los archivos de copia de seguridad fuera del contenedor. En caso contrario, si se quita el contenedor, también se eliminan los archivos de copia de seguridad.

## <a name="execute-commands-in-a-container"></a>Ejecutar comandos en un contenedor

Si tiene un contenedor en ejecución, puede ejecutar comandos dentro del contenedor desde un terminal de host.

Para obtener el identificador del contenedor ejecutar:

```bash
docker ps
```

Para iniciar un terminal en el contenedor se ejecute de bash:

```bash
docker exec -ti <Container ID> /bin/bash
```

Ahora puede ejecutar comandos como si está ejecutando en el terminal dentro del contenedor. Cuando termine, escriba `exit`. Este modo se sale de la sesión interactiva de comandos, pero el contenedor continúa ejecutándose.

## <a name="copy-files-from-a-container"></a>Copiar archivos desde un contenedor

Para copiar un archivo fuera del contenedor, use el siguiente comando:

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

## <a name="copy-files-into-a-container"></a>Copie los archivos en un contenedor

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
## <a id="tz"></a> Configurar la zona horaria

Para ejecutar SQL Server en un contenedor de Linux con una zona horaria concreto, configure el **TZ** variable de entorno. Para buscar el valor de la zona horaria correcta, ejecute el **tzselect** comando desde un símbolo del sistema de bash de Linux:

```bash
tzselect
```

Después de seleccionar la zona horaria, **tzselect** muestra un resultado similar al siguiente:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

Puede usar esta información para establecer la misma variable de entorno en el contenedor de Linux. El ejemplo siguiente muestra cómo ejecutar SQL Server en un contenedor en el `Americas/Los_Angeles` zona horaria:

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
   -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```
::: moniker-end

## <a id="tags"></a> Ejecución de una imagen de contenedor de SQL Server específica

Hay escenarios donde es posible que no desea usar la imagen de contenedor más reciente de SQL Server. Para ejecutar una imagen de contenedor de SQL Server específica, use los pasos siguientes:

1. Identificar el Docker **etiqueta** para la versión que desea usar. Para ver las etiquetas disponibles, consulte [la página concentrador de Docker de mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

2. Extraiga la imagen de contenedor de SQL Server con la etiqueta. Por ejemplo, para extraer la imagen de RC1, reemplace `<image_tag>` en el siguiente comando con `rc1`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Para ejecutar un nuevo contenedor con esa imagen, especifique el nombre de etiqueta en el `docker run` comando. En el siguiente comando, reemplace `<image_tag>` con la versión que desea ejecutar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Estos pasos también pueden utilizarse para degradar un contenedor existente. Por ejemplo, es posible que desea revertir o degradar un contenedor en ejecución para solucionar problemas o las pruebas. Para degradar un contenedor en ejecución, debe usar una técnica de persistencia para la carpeta de datos. Siga los mismos pasos descritos en la [actualizar sección](#upgrade), pero especifique el nombre de etiqueta de la versión anterior al ejecutar el nuevo contenedor.

## <a id="version"></a> Comprobar la versión de contenedor

Si desea conocer la versión de SQL Server en un contenedor de docker en ejecución, ejecute el siguiente comando para que se muestre. Reemplace `<Container ID or name>` con el nombre o Id. de contenedor de destino. Reemplace `<YourStrong!Passw0rd>` con la contraseña de SQL Server para el inicio de sesión de SA.

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

También puede identificar la versión de SQL Server y el número de compilación para una imagen de contenedor de docker de destino. El comando siguiente muestra la información de versión y compilación de SQL Server para la **microsoft/mssql-server-linux:2017-última** imagen. Para ello, ejecute un nuevo contenedor con una variable de entorno **PAL_PROGRAM_INFO = 1**. El contenedor resultante se cierra al instante y el `docker rm` comando lo quita.

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

Los comandos anteriores muestran información similar a la siguiente salida de la versión:

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

## <a id="upgrade"></a> Actualizar SQL Server en contenedores

Para actualizar la imagen de contenedor con Docker, en primer lugar identifique la etiqueta para la versión para la actualización. Esta versión de incorporación de cambios desde el registro con el `docker pull` comando:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Esto actualiza la imagen de SQL Server para los nuevos contenedores que cree, pero no se actualiza SQL Server en los contenedores en ejecución. Para ello, debe crear un nuevo contenedor con la imagen de contenedor más reciente de SQL Server y migrar los datos a ese nuevo contenedor.

1. Asegúrese de que está usando uno de los [técnicas de persistencia de datos](#persist) para el contenedor de SQL Server existente. Esto le permite iniciar un nuevo contenedor con los mismos datos.

1. Detener el contenedor de SQL Server con el `docker stop` comando.

1. Crear un nuevo contenedor de SQL Server con `docker run` y especifique un directorio de host asignado o un contenedor de volúmenes de datos. Asegúrese de que se usará la etiqueta específica para la actualización de SQL Server. El nuevo contenedor ahora usa una nueva versión de SQL Server con los datos de SQL Server existentes.

   > [!IMPORTANT]
   > Solo se admite la actualización entre GA, RC1 y RC2 en este momento.

1. Compruebe las bases de datos y los datos en el nuevo contenedor.

1. Si lo desea, quite del contenedor antiguo con `docker rm`.

## <a id="troubleshooting"></a> Solucionar problemas

Las secciones siguientes proporcionan sugerencias de solución de problemas para ejecutar SQL Server en contenedores.

### <a name="docker-command-errors"></a>Errores del comando de docker

Si se producen errores de cualquier `docker` comandos, asegúrese de que el servicio docker se está ejecutando y vuelva a ejecutar con permisos elevados.

Por ejemplo, en Linux, puede aparecer el siguiente error al ejecutar `docker` comandos:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Si obtiene este error en Linux, pruebe a ejecutar los mismos comandos que comiencen por `sudo`. Si se produce un error, compruebe el servicio docker se está ejecutando e inícielo si es necesario.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

En Windows, compruebe que se están lanzando PowerShell o la línea de comandos como administrador.

### <a name="sql-server-container-startup-errors"></a>Errores de inicio del contenedor de SQL Server

Si no se puede ejecutar el contenedor de SQL Server, pruebe las siguientes pruebas:

- Si se produce un error como **' no se pudo crear el punto de conexión CONTAINER_NAME en puente de red. Error al iniciar el proxy: enlace de escucha tcp 0.0.0.0:1433: dirección ya está en uso. "** , a continuación, intenta asignar el puerto 1433 del contenedor a un puerto que ya está en uso. Esto puede ocurrir si está ejecutando SQL Server localmente en el equipo host. También puede ocurrir si inicia dos contenedores de SQL Server e intenta asignar ambos al mismo puerto de host. Si esto ocurre, utilice el `-p` parámetro para asignar el puerto 1433 del contenedor a un puerto de host diferente. Por ejemplo: 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu`.
```

::: moniker-end

- Compruebe si hay algún mensaje de error del contenedor.

    ```bash
    docker logs e69e056c702d
    ```

- Asegúrese de que cumplen los requisitos mínimos de memoria y disco especificados en el [requisitos](#requirements) sección de este artículo.

- Si usa cualquier software de administración de contenedores, asegúrese de que es compatible con procesos de contenedor que se ejecutan como raíz. El proceso sqlservr en el contenedor se ejecuta como raíz.

- Revise el [registros de errores y el programa de instalación de SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Habilitar la captura de volcado de memoria

Si se producen errores en el proceso de SQL Server dentro del contenedor, debe crear un nuevo contenedor con **SYS_PTRACE** habilitado. Esto agrega la capacidad de Linux para realizar un seguimiento de un proceso, que es necesario para crear un archivo de volcado de memoria en una excepción. El archivo de volcado puede utilizarse por soporte técnico para ayudar a solucionar el problema. El siguiente comando docker run permita esta funcionalidad.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.3-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Errores de conexión de SQL Server

Si no se puede conectar a la instancia de SQL Server que se ejecuta en el contenedor, pruebe las siguientes pruebas:

- Asegúrese de que el contenedor de SQL Server se está ejecutando examinando el **estado** columna de la `docker ps -a` salida. Si no, utilice `docker start <Container ID>` para iniciarlo.

- Si asigna a un puerto de host no predeterminado (1433 no), asegúrese de que se está especificando el puerto en la cadena de conexión. Puede ver la asignación de puertos en el **puertos** columna de la `docker ps -a` salida. Por ejemplo, el siguiente comando conecta sqlcmd en un contenedor escucha en el puerto 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Si ha usado `docker run` con un volumen de datos asignado existente o un contenedor de volúmenes de datos, SQL Server omite el valor de `MSSQL_SA_PASSWORD`. En su lugar, se usa la contraseña del usuario SA configurada previamente de los datos de SQL Server en el volumen de datos o un contenedor de volúmenes de datos. Compruebe que está usando la contraseña de SA asociada con los datos que se va a asociar.

- Revise el [registros de errores y el programa de instalación de SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Grupos de disponibilidad SQL Server

Si usa Docker con grupos de disponibilidad de SQL Server, hay dos requisitos adicionales.

- Asigne el puerto que se usa para la comunicación de réplica (el valor predeterminado es 5022). Por ejemplo, especificar `-p 5022:5022` como parte de su `docker run` comando.

- Establecer explícitamente el nombre de host de contenedor con el `-h YOURHOSTNAME` parámetro de la `docker run` comando. Este nombre de host se utiliza al configurar el grupo de disponibilidad. Si no se especifica con `-h`, el valor predeterminado es el identificador del contenedor.

### <a id="errorlogs"></a> Registros de errores y el programa de instalación de SQL Server

Puede mirar el programa de instalación de SQL Server y los registros de errores **/var/opt/mssql/log**. Si el contenedor no se está ejecutando, inicie primero el contenedor. A continuación, usar una línea de comandos interactiva para inspeccionar los registros.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

En la sesión de bash dentro del contenedor, ejecute los siguientes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Si se monta un directorio de host **/var/opt/mssql** al crear el contenedor, en su lugar, puede buscar en el **registro** subdirectorio en la ruta de acceso asignado en el host.

## <a name="next-steps"></a>Pasos siguientes

Empezar a trabajar con imágenes de contenedor de SQL Server 2017 en Docker a través de la [quickstart](quickstart-install-connect-docker.md).

Consulte también el [repositorio de GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) para recursos, comentarios y problemas conocidos.

[Explore la alta disponibilidad para los contenedores de SQL Server](sql-server-linux-container-ha-overview.md)
