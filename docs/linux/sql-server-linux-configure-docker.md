---
title: "Opciones de configuración de SQL Server 2017 en Docker | Documentos de Microsoft"
description: "Explorar maneras diferentes de utilizar e interactuar con SQL Server 2017 imágenes del contenedor en Docker. Esto incluye los datos de persistencia, copiando los archivos y solución de problemas."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: f684f0168e57c5cd727af6488b2460eeaead100c
ms.openlocfilehash: 6a187e6ad238743d0643ef56b76ace7977def228
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="configure-sql-server-2017-container-images-on-docker"></a>Configurar SQL Server 2017 imágenes del contenedor en Docker

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tema se explica cómo configurar y usar el [imagen de contenedor mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) con Docker. Esta imagen se compone de SQL Server que se ejecutan en Linux en función de Ubuntu 16.04. Se puede utilizar con el motor de Docker 1.8 + en Linux o en Docker para Mac y Windows.

> [!NOTE]
> En este tema se centra específicamente en medio de la imagen mssql-server-linux. La imagen de Windows no está cubierta, pero puede obtener más información sobre la [página de Docker Hub de windows del servidor mssql](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

Para extraer y ejecutar al Docker imagen de contenedor para SQL Server 2017, siga los pasos y requisitos previos en el siguiente tutorial de inicio rápido:

- [Ejecutar la imagen de contenedor de SQL Server 2017 con Docker](quickstart-install-connect-docker.md)

En este tema de configuración proporciona conexión adicionales y escenarios de uso en las secciones siguientes.

## <a name="connect-and-query"></a>Consultar y conectarse

Puede conectarse y consultar SQL Server en un contenedor desde fuera del contenedor o desde el contenedor. Las siguientes secciones explican ambos escenarios. 

### <a name="tools-outside-the-container"></a>Herramientas fuera del contenedor

Puede conectarse a la instancia de SQL Server en el equipo de Docker desde cualquier herramienta externa de Linux, Windows o Mac OS que admite las conexiones de SQL. Algunas herramientas comunes incluyen:

- [Sqlcmd](sql-server-linux-setup-tools.md)
- [Código de Visual Studio](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) en Windows](sql-server-linux-develop-use-ssms.md)

En el ejemplo siguiente se utiliza **sqlcmd** para conectarse a SQL Server que se ejecuta en un contenedor de Docker. La dirección IP en la cadena de conexión es la dirección IP del equipo host que ejecuta el contenedor.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Si ha asignado un puerto de host que no era la predeterminada **1433**, agregue ese puerto a la cadena de conexión. Por ejemplo, si especificó `-p 1400:1433` en su `docker run` comando, a continuación, conectarse explícitamente especificar puerto 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Herramientas dentro del contenedor

A partir de SQL Server de 2017 CTP 2.0, el [herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md) se incluyen en la imagen del contenedor. Si se adjunta a la imagen con una línea de comandos interactivo, puede ejecutar las herramientas localmente.

1. Use la `docker exec -it` comando para iniciar un shell de bash interactivo dentro de su contenedor en ejecución. En el ejemplo siguiente `e69e056c702d` es el identificador del contenedor.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > No siempre tendrá que especificar el identificador del contenedor todo. Solamente debe especificar suficientes caracteres para identificar de forma exclusiva. Por lo que en este ejemplo, es posible que sea suficiente para usar `e6` o `e69` en lugar del identificador completo.

2. Una vez dentro del contenedor, conectar localmente con sqlcmd. Tenga en cuenta que sqlcmd no está en la ruta de acceso de forma predeterminada, por lo que debe especificar la ruta de acceso completa.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Cuando termine con sqlcmd, escriba `exit`.

4. Cuando termine con la línea de comandos interactiva, escriba `exit`. El contenedor continúa ejecutándose después de salir del shell de bash interactivo.

## <a name="run-multiple-sql-server-containers"></a>Ejecutar varios contenedores de SQL Server

Docker ofrece una manera de ejecutar varios contenedores de SQL Server en el mismo equipo host. Este es el enfoque para escenarios que requieren varias instancias de SQL Server en el mismo host. Cada contenedor debe exponer a sí mismo en un puerto diferente.

El siguiente ejemplo crea dos contenedores de SQL Server y los asigna a los puertos **1401** y **1402** en el equipo host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d microsoft/mssql-server-linux
```

Ahora hay dos instancias de SQL Server en contenedores diferentes. Los clientes pueden conectarse a cada instancia de SQL Server mediante la dirección IP del host de Docker y el número de puerto para el contenedor.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="persist"></a>Conservar los datos

Los cambios de configuración de SQL Server y los archivos de base de datos se conservan en el contenedor, incluso si reinicia el contenedor con `docker stop` y `docker start`. Sin embargo, si quita el contenedor con `docker rm`, se eliminará todo en el contenedor, incluidos SQL Server y las bases de datos. En la siguiente sección se explica cómo usar **volúmenes de datos** para conservar los archivos de base de datos, incluso si se eliminan los contenedores asociados.

> [!IMPORTANT]
> Para SQL Server, es fundamental que comprenda la persistencia de los datos en Docker. Además de la explicación en esta sección, vea la documentación de Docker en [cómo administrar datos en contenedores de Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montar un directorio de host como volumen de datos

La primera opción consiste en montar un directorio en el host como un volumen de datos en su contenedor. Para ello, utilice la `docker run` comando con el `-v <host directory>:/var/opt/mssql` marca. Esto permite que los datos que se restaurarán entre ejecuciones de contenedor.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

Esta técnica también le permite compartir y ver los archivos en el host fuera de Docker.

> [!IMPORTANT]
> Asignación de volúmenes de host de Docker en Mac con SQL Server en la imagen de Linux no se admite en este momento. Utilice contenedores de volúmenes de datos en su lugar. Esta restricción es específica de la `/var/opt/mssql` directory. Leer un funciona directorio montado correctamente. Por ejemplo, puede montar un directorio de host mediante – v Mac y restaurar una copia de seguridad de un archivo .bak que reside en el host.

### <a name="use-data-volume-containers"></a>Utilizar contenedores de volúmenes de datos

La segunda opción es usar un contenedor de volúmenes de datos. Puede crear un contenedor de volúmenes de datos especificando un nombre de volumen en lugar de un directorio de host con el `-v` parámetro. En el ejemplo siguiente se crea un volumen de datos compartido denominado **sqlvolume**.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

> [!NOTE]
> Esta técnica para crear un volumen de datos implícitamente en el comando de ejecución no funciona con versiones anteriores de Docker. En ese caso, use los pasos explícitos que se describen en la documentación de Docker, [crear y montar un contenedor de volúmenes de datos](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Aunque detenga y quite este contenedor, se conserva el volumen de datos. Puede ver con el `docker volume ls` comando.

```bash
docker volume ls
```

Si, a continuación, crea otro contenedor con el mismo nombre de volumen, el nuevo contenedor utiliza los mismos datos de SQL Server incluidos en el volumen.

Para quitar un contenedor de volúmenes de datos, use la `docker volume rm` comando.

> [!WARNING]
> Si elimina el contenedor de volúmenes de datos, los datos de SQL Server en el contenedor están *permanentemente* eliminado.

### <a name="backup-and-restore"></a>Copias de seguridad y restauración

Además de estas técnicas de contenedor, también puede utilizar la copia de seguridad de SQL Server estándar y técnicas de restauración. Puede usar archivos de copia de seguridad para proteger los datos o para mover los datos a otra instancia de SQL Server. Para obtener más información, consulte [copias de seguridad y restauración de SQL Server las bases de datos en Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Si crea copias de seguridad, asegúrese de crear o copiar los archivos de copia de seguridad fuera del contenedor. En caso contrario, si se quita el contenedor, también se eliminan los archivos de copia de seguridad.

## <a name="execute-commands-in-a-container"></a>Ejecutar comandos en un contenedor

Si tiene un contenedor en ejecución, puede ejecutar comandos dentro del contenedor de un host de terminal.

Para obtener el identificador del contenedor ejecutar:

```bash
docker ps
```

Para iniciar una terminal en el contenedor de ejecución intensiva de errores:

```bash
docker exec -ti <Container ID> /bin/bash
```

Ahora puede ejecutar comandos como si está ejecutando en el terminal dentro del contenedor. Cuando termine, escriba `exit`. Este modo se sale de la sesión interactiva de comandos, pero el contenedor continúa ejecutándose.

## <a name="copy-files-from-a-container"></a>Copiar archivos desde un contenedor

Para copiar un archivo fuera del contenedor, use el comando siguiente:

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

Para copiar un archivo en el contenedor, use el comando siguiente:

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

## <a id="upgrade"></a>Actualizar SQL Server en contenedores

Para actualizar la imagen del contenedor con Docker, extraer la versión más reciente desde el registro. Use la `docker pull` comando:

```bash
docker pull microsoft/mssql-server-linux:latest
```

Esto actualiza la imagen de SQL Server para los nuevos contenedores que se crea, pero no actualiza SQL Server en los contenedores en ejecución. Para ello, debe crear un nuevo contenedor con la última imagen de contenedor de SQL Server y migrar los datos a un nuevo contenedor.

1. En primer lugar, obtenga la última imagen de contenedor de SQL Server.

   ```bash
   docker pull microsoft/mssql-server-linux:latest
   ```

1. Asegúrese de que está usando uno de los [técnicas de persistencia de datos](#persist) para el contenedor de SQL Server existente. Esto le permite iniciar un nuevo contenedor con los mismos datos.

1. Detenga el contenedor de SQL Server con el `docker stop` comando.

1. Crear un nuevo contenedor de SQL Server con `docker run` y especifique un directorio de host asignado o un contenedor de volúmenes de datos. El nuevo contenedor usa ahora una nueva versión de SQL Server con los datos de SQL Server existentes.

   > [!IMPORTANT]
   > Solo se admite la actualización entre RC1 y RC2 en este momento.

1. Compruebe las bases de datos y los datos en el nuevo contenedor.

1. Si lo desea, quite del contenedor antiguo con `docker rm`.

## <a name="run-a-specific-sql-server-container-image"></a>Ejecutar una imagen de contenedor específica de SQL Server

Existen escenarios donde no desea usar la imagen de contenedor más reciente de SQL Server. Para ejecutar una imagen de contenedor de SQL Server específica, utilice los pasos siguientes:

1. Identificar la Docker **etiqueta** para la versión que desea usar. Para ver las etiquetas disponibles, vea [la página del concentrador mssql-server-linux Docker](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Extraiga la imagen de contenedor de SQL Server con la etiqueta. Por ejemplo, para extraer la imagen de RC1, reemplace `<image_tag>` en el siguiente comando con `rc1`.

   ```bash
   docker pull microsoft/mssql-server-linux:<image_tag>
   ```

1. Para ejecutar un nuevo contenedor con esa imagen, especifique el nombre de etiqueta en el `docker run` comando. En el siguiente comando, reemplace `<image_tag>` con la versión que desea ejecutar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

Estos pasos también se pueden utilizar para degradar un contenedor existente. Por ejemplo, podría desea deshacer o degradar un contenedor en ejecución para la solución de problemas o las pruebas. Para degradar un contenedor en ejecución, debe utilizar una técnica de persistencia de la carpeta de datos. Siga los mismos pasos que se describen en la [actualizar sección](#upgrade), pero especifica el nombre de etiqueta de la versión más antigua cuando se ejecuta el nuevo contenedor.

> [!IMPORTANT]
> Actualización y degradación solo se admiten entre RC1 y RC2 en este momento.

## <a id="troubleshooting"></a>Solución de problemas

Las secciones siguientes proporcionan sugerencias para solucionar problemas para ejecutar SQL Server en contenedores.

### <a name="docker-command-errors"></a>Errores de comando de docker

Si se producen errores para cualquier `docker` comandos, asegúrese de que se está ejecutando el servicio de docker y vuelva a intentar con permisos elevados.

Por ejemplo, en Linux, podría obtener el siguiente error al ejecutar `docker` comandos:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Si se produce este error en Linux, pruebe a ejecutar los mismos comandos que se prologa con `sudo`. Si se produce un error, compruebe el servicio docker está ejecutando e inícielo si es necesario.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

En Windows, compruebe que se inicie PowerShell o la línea de comandos como administrador.

### <a name="sql-server-container-startup-errors"></a>Errores de inicio del contenedor de SQL Server

Si no se puede ejecutar el contenedor de SQL Server, pruebe las siguientes pruebas:

- Si se produce un error como **' no se pudo crear el punto de conexión CONTAINER_NAME en el puente de red. Error al iniciar el proxy: enlace de escucha tcp 0.0.0.0:1433: dirección ya está en uso. " **, a continuación, intenta asignar el puerto 1433 de contenedor a un puerto que ya está en uso. Esto puede ocurrir si está ejecutando SQL Server localmente en el equipo host. También puede ocurrir si inicia dos contenedores de SQL Server e intenta asignar ambos en el mismo puerto de host. Si esto ocurre, use la `-p` un parámetro para asignar el puerto 1433 de contenedor a un puerto de host diferente. Por ejemplo: 

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

- Compruebe si hay algún mensaje de error del contenedor.

    ```bash
    docker logs e69e056c702d
    ```

- Asegúrese de que se cumplen los requisitos mínimos de memoria y disco especificados en el [requisitos](#requirements) sección de este tema.

- Si está utilizando ningún software de administración de contenedor, asegúrese de es compatible con procesos de contenedor que se ejecutan como raíz. El proceso de sqlservr en el contenedor se ejecuta como raíz.

- Revise el [registros de errores y el programa de instalación de SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Habilitar la captura de volcado de memoria

Si se producen errores en el proceso de SQL Server dentro del contenedor, debe crear un nuevo contenedor con **SYS_PTRACE** habilitado. Esto agrega la capacidad de Linux para realizar el seguimiento de un proceso, que es necesario para crear un archivo de volcado de memoria en una excepción. El archivo de volcado de memoria puede utilizarse por el soporte técnico para ayudar a solucionar el problema. El siguiente comando docker run habilita esta funcionalidad.

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
```

### <a name="sql-server-connection-failures"></a>Errores de conexión de SQL Server

Si no se puede conectar con la instancia de SQL Server que se ejecuta en el contenedor, pruebe las siguientes pruebas:

- Asegúrese de que el contenedor de SQL Server se está ejecutando examinando el **estado** columna de la `docker ps -a` salida. Si no es así, utilice `docker start <Container ID>` para iniciarlo.

- Si ha asignado a un puerto de host no es el predeterminado (1433 no), asegúrese de que está especificando el puerto en la cadena de conexión. Puede ver la asignación de puertos en el **puertos** columna de la `docker ps -a` salida. Por ejemplo, el siguiente comando conecta sqlcmd en un contenedor que escucha en el puerto 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Si ha usado `docker run` con un volumen de datos asignado existente o un contenedor de volúmenes de datos, SQL Server omite el valor de `MSSQL_SA_PASSWORD`. En su lugar, se utiliza la contraseña del usuario administrador configurada previamente de los datos de SQL Server en el volumen de datos o el contenedor de volúmenes de datos. Compruebe que está usando la contraseña del administrador asociada con los datos a que lo está adjuntando.

- Revise el [registros de errores y el programa de instalación de SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Grupos de disponibilidad SQL Server

Si usas Docker con grupos de disponibilidad de SQL Server, existen dos requisitos adicionales.

- Asigne el puerto que se utiliza para la comunicación de réplica (el valor predeterminado es 5022). Por ejemplo, especificar `-p 5022:5022` como parte de su `docker run` comando.

- Establecer explícitamente el nombre de host de contenedor con el `-h YOURHOSTNAME` parámetro de la `docker run` comando. Este nombre de host se usa cuando se configura el grupo de disponibilidad. Si no se especifica con `-h`, el valor predeterminado es el identificador del contenedor.

### <a id="errorlogs"></a>Registros de errores y el programa de instalación de SQL Server

También puede buscar en el programa de instalación de SQL Server y los registros de errores **/var/opt/mssql/log**. Si el contenedor no se está ejecutando, inicie primero el contenedor. A continuación, usar un aviso de comando interactivo para inspeccionar los registros.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Desde la sesión intensiva de errores dentro de su contenedor, ejecute los siguientes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Si ha montado un directorio de host **/var/opt/mssql** al crear el contenedor, en su lugar, puede buscar en el **registro** subdirectorio en la ruta de acceso asignada en el host.

## <a name="next-steps"></a>Pasos siguientes

Empezar a trabajar con imágenes de contenedores de 2017 de SQL Server en Docker, vaya a través de la [tutorial de inicio rápido](quickstart-install-connect-docker.md).

Consulte también la [repositorio de GitHub de docker mssql](https://github.com/Microsoft/mssql-docker) para los recursos, comentarios y problemas conocidos.

