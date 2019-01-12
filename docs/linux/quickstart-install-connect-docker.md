---
title: Empezar a trabajar con contenedores de SQL Server en Docker (que se ejecuta SQL Server en Linux)
titleSuffix: SQL Server
description: En este tutorial rápido se muestra cómo usar Docker para ejecutar el SQL Server 2017 y las imágenes de contenedor de 2019. A continuación, deberá crear una base de datos y realizar consultas en esta con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/10/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sql-linux, seodec18
ms.prod_service: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: f4e6298cb1165f75dcd9a6aa6c77a1628650c0f6
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206321"
---
# <a name="quickstart-run-sql-server-container-images-with-docker"></a>Inicio rápido: Ejecutar imágenes de contenedor de SQL Server con Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En este inicio rápido, deberá usar Docker para extraer y ejecutar la imagen de contenedor de SQL Server 2017, [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). A continuación, tendrá que conectar con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

> [!TIP]
> Si desea probar la imagen de vista previa de 2019 de SQL Server, vea el [2019 de SQL Server versión de vista previa de este artículo](quickstart-install-connect-docker.md?view=sql-server-linux-ver15).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En este tutorial, use Docker para extraer y ejecutar la imagen de contenedor de vista previa de SQL Server 2019 [mssql-server](https://hub.docker.com/r/microsoft/mssql-server). A continuación, tendrá que conectar con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

::: moniker-end

Esta imagen se compone de SQL Server, que se ejecuta en un sistema Linux basado en Ubuntu 16.04. Se puede usar junto al motor de Docker 1.8 o versiones posteriores en Linux, o bien en Docker en Mac y Windows. Esta guía de inicio rápido se centra específicamente en el uso de SQL Server en **linux** imagen. No trataremos la imagen de Windows, pero puede obtener más información sobre esta en la [página mssql-server-windows-developer de Docker Hub](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a id="requirements"></a> Requisitos previos

- Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).
- Docker **overlay2** controlador de almacenamiento. Este es el valor predeterminado para la mayoría de los usuarios. Si encuentra que no usa este proveedor de almacenamiento y necesita cambiar, consulte las instrucciones y las advertencias en el [documentación de docker para configurar overlay2](https://docs.docker.com/storage/storagedriver/overlayfs-driver/#configure-docker-with-the-overlay-or-overlay2-storage-driver).
- Mínimo de 2 GB de espacio en disco.
- Mínimo de 2 GB de RAM.
- [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

<!--The following H2 is versioned for 2017 and 2019. Much of the content is duplicated, so
any changes to one section should be duplicated in the other-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="pullandrun2017"></a> Extraer y ejecutar la imagen de contenedor

1. Extraiga la imagen de contenedor de SQL Server 2017 para Linux desde el registro de contenedor de Microsoft.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > Si desea probar la imagen de vista previa de 2019 de SQL Server, vea el [2019 de SQL Server versión de vista previa de este artículo](quickstart-install-connect-docker.md?view=sql-server-linux-ver15#pullandrun2019).

   En el comando anterior, se extrae la última imagen de contenedor de SQL Server 2017. Si quiere extraer una imagen específica, agregue dos puntos y el nombre de etiqueta (por ejemplo, `mcr.microsoft.com/mssql/server:2017-GA-ubuntu`). Para ver todas las imágenes disponibles, consulte [la página concentrador de Docker de mssql-server](https://hub.docker.com/r/microsoft/mssql-server).

   Para los comandos de bash en este artículo, `sudo` se utiliza. En MacOS, `sudo` podría no ser necesario. En Linux, si no desea usar `sudo` para ejecutar Docker, puede configurar un **docker** agrupar y agregar usuarios a ese grupo. Para obtener más información, consulte [los pasos posteriores a la instalación para Linux](https://docs.docker.com/install/linux/linux-postinstall/).

2. Para ejecutar la imagen de contenedor con Docker, puede usar el siguiente comando desde un shell de Bash (Linux y macOS), o bien una línea de comandos de PowerShell con privilegios elevados.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!NOTE]
   > La contraseña debe seguir la directiva de contraseñas predeterminada de SQL Server. En caso contrario, el contenedor no podrá instalar SQL Server y dejará de funcionar. De forma predeterminada, la contraseña debe tener al menos 8 caracteres y contener caracteres de tres de los cuatro grupos siguientes: Letras mayúsculas, letras minúsculas, dígitos de Base 10 y símbolos. Puede examinar el registro de errores ejecutando el comando [docker logs](https://docs.docker.com/engine/reference/commandline/logs/).

   > [!NOTE]
   > De forma predeterminada, se creará un contenedor con la edición para desarrolladores de SQL Server 2017. El proceso para ejecutar las ediciones de producción en contenedores es ligeramente diferente. Para obtener más información, vea [Run production container image](sql-server-linux-configure-docker.md#production) (Ejecutar imágenes de contenedor de producción).

   En la tabla siguiente, se proporciona una descripción de los parámetros del ejemplo de `docker run` anterior:

   | Parámetro | Descripción |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  Establezca la variable **ACCEPT_EULA** en cualquier valor para confirmar que acepta el [Contrato de licencia de usuario final](https://go.microsoft.com/fwlink/?LinkId=746388). Configuración requerida para la imagen de SQL Server. |
   | **-e "contraseña_sa =\<YourStrong! Passw0rd\>'** | Especifique una contraseña segura propia con al menos 8 caracteres y que cumpla los [requisitos de contraseña de SQL Server](../relational-databases/security/password-policy.md). Configuración requerida para la imagen de SQL Server. |
   | **-p 1433:1433** | Asigne un puerto TCP en el entorno de host (el primer valor) a un puerto TCP en el contenedor (el segundo valor). En este ejemplo, SQL Server está escuchando en TCP 1433 en el contenedor y se expone al puerto 1433 en el host. |
   | **--name sql1** | Especifique un nombre personalizado para el contenedor en lugar de uno generado aleatoriamente. Si ejecuta más de un contenedor, no podrá usar el mismo nombre. |
   | **MCR.Microsoft.com/MSSQL/Server:2017-Latest** | La imagen de contenedor de SQL Server 2017 para Linux. |

3. Para ver los contenedores de Docker, use el comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   Debería ver un resultado similar al de la captura de pantalla siguiente:

   ![Resultado del comando docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. Si la columna **ESTADO** muestra el estado **Activo**, esto indica que SQL Server se está ejecutando en el contenedor y que está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

El parámetro `-h` (nombre del host) también es útil, pero no se usa en este tutorial para simplificar el proceso. Esto cambia el nombre interno del contenedor a un valor personalizado. Este es el nombre que verá que se devuelve en la siguiente consulta de Transact-SQL:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Establecer `-h` y `--name` en el mismo valor es una buena manera de identificar fácilmente el contenedor de destino.

::: moniker-end
<!--End of 2017 "Pull and run" section-->

<!--This is the 2019 version of the "Pull and run" section-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="pullandrun2019"></a> Extraer y ejecutar la imagen de contenedor

1. Extraer la versión preliminar de SQL Server 2019 imagen de contenedor de Linux de Docker Hub.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   > [!TIP]
   > Este tutorial rápido usa la versión preliminar de SQL Server 2019 imagen de Docker. Si desea ejecutar la imagen de SQL Server 2017, consulte el [SQL Server 2017, versión de este artículo](quickstart-install-connect-docker.md?view=sql-server-linux-2017#pullandrun2017).

   El comando anterior, extrae la imagen de contenedor de vista previa de SQL Server 2019 más reciente basada en Ubuntu. Para usar en su lugar imágenes de contenedor basadas en RedHat, consulte [imágenes de contenedor basadas en RHEL ejecutar](sql-server-linux-configure-docker.md#rhel). Si quiere extraer una imagen específica, agregue dos puntos y el nombre de etiqueta (por ejemplo, `mcr.microsoft.com/mssql/server:2017-GA`). Para ver todas las imágenes disponibles, vea [la página mssql-server-linux de Docker Hub](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

   Para los comandos de bash en este artículo, `sudo` se utiliza. En MacOS, `sudo` podría no ser necesario. En Linux, si no desea usar `sudo` para ejecutar Docker, puede configurar un **docker** agrupar y agregar usuarios a ese grupo. Para obtener más información, consulte [los pasos posteriores a la instalación para Linux](https://docs.docker.com/install/linux/linux-postinstall/).

2. Para ejecutar la imagen de contenedor con Docker, puede usar el siguiente comando desde un shell de Bash (Linux y macOS), o bien una línea de comandos de PowerShell con privilegios elevados.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   > [!NOTE]
   > La contraseña debe seguir la directiva de contraseñas predeterminada de SQL Server. En caso contrario, el contenedor no podrá instalar SQL Server y dejará de funcionar. De forma predeterminada, la contraseña debe tener al menos 8 caracteres y contener caracteres de tres de los cuatro grupos siguientes: Letras mayúsculas, letras minúsculas, dígitos de Base 10 y símbolos. Puede examinar el registro de errores ejecutando el comando [docker logs](https://docs.docker.com/engine/reference/commandline/logs/).

   > [!NOTE]
   > De forma predeterminada, esto crea un contenedor con la edición para desarrolladores de vista previa de SQL Server 2019.

   En la tabla siguiente, se proporciona una descripción de los parámetros del ejemplo de `docker run` anterior:

   | Parámetro | Descripción |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  Establezca la variable **ACCEPT_EULA** en cualquier valor para confirmar que acepta el [Contrato de licencia de usuario final](https://go.microsoft.com/fwlink/?LinkId=746388). Configuración requerida para la imagen de SQL Server. |
   | **-e "contraseña_sa =\<YourStrong! Passw0rd\>'** | Especifique una contraseña segura propia con al menos 8 caracteres y que cumpla los [requisitos de contraseña de SQL Server](../relational-databases/security/password-policy.md). Configuración requerida para la imagen de SQL Server. |
   | **-p 1433:1433** | Asigne un puerto TCP en el entorno de host (el primer valor) a un puerto TCP en el contenedor (el segundo valor). En este ejemplo, SQL Server está escuchando en TCP 1433 en el contenedor y se expone al puerto 1433 en el host. |
   | **--name sql1** | Especifique un nombre personalizado para el contenedor en lugar de uno generado aleatoriamente. Si ejecuta más de un contenedor, no podrá usar el mismo nombre. |
   | **MCR.Microsoft.com/MSSQL/Server:2019-CTP2.2-Ubuntu** | La imagen de contenedor de SQL Server de 2019 CTP 2.2 Linux. |

3. Para ver los contenedores de Docker, use el comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   Debería ver un resultado similar al de la captura de pantalla siguiente:

   ![Resultado del comando docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. Si la columna **ESTADO** muestra el estado **Activo**, esto indica que SQL Server se está ejecutando en el contenedor y que está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

El parámetro `-h` (nombre del host) también es útil, pero no se usa en este tutorial para simplificar el proceso. Esto cambia el nombre interno del contenedor a un valor personalizado. Este es el nombre que verá que se devuelve en la siguiente consulta de Transact-SQL:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Establecer `-h` y `--name` en el mismo valor es una buena manera de identificar fácilmente el contenedor de destino.

::: moniker-end
<!--End of 2019 "Pull and run" section-->

## <a id="sapassword"></a> Cambiar la contraseña de SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

En los pasos siguientes, se usa la herramienta de línea de comandos de SQL Server, **sqlcmd**, dentro del contenedor para conectarse a SQL Server.

1. Use el comando `docker exec -it` para iniciar un shell de Bash interactivo dentro de su contenedor en ejecución. En el ejemplo siguiente, el parámetro `--name` especifica el nombre de `sql1` al crear el contenedor.

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. Una vez dentro del contenedor, conecte localmente con sqlcmd. Sqlcmd no está en la ruta de acceso de forma predeterminada, por lo que deberá especificar la ruta de acceso completa.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   > [!TIP]
   > Puede omitir la contraseña en la línea de comandos para que se le solicite escribirla.

1. Si se realiza correctamente, debe ver un símbolo de sistema de **sqlcmd**: `1>`.

## <a name="create-and-query-data"></a>Creación y consulta de datos

Las secciones siguientes le guían en el uso de **sqlcmd** y Transact-SQL para crear una base de datos, agregar datos y ejecutar una consulta simple.

### <a name="create-a-new-database"></a>Creación de una base de datos

En los pasos siguientes se crea una base de datos denominada `TestDB`.

1. En el símbolo del sistema de **sqlcmd**, pegue el comando Transact-SQL siguiente para crear una base de datos de prueba:

   ```sql
   CREATE DATABASE TestDB
   ```

1. En la línea siguiente, escriba una consulta para devolver el nombre de todas las bases de datos del servidor:

   ```sql
   SELECT Name from sys.Databases
   ```

1. Los dos comandos anteriores no se ejecutaron de inmediato. Debe escribir `GO` en una línea nueva para ejecutar los comandos anteriores:

   ```sql
   GO
   ```

### <a name="insert-data"></a>Inserción de datos

Luego cree una tabla, `Inventory`, e inserte dos filas nuevas.

1. En el símbolo del sistema de **sqlcmd**, cambie el contexto a la nueva base de datos `TestDB`:

   ```sql
   USE TestDB
   ```

1. Cree una tabla llamada `Inventory`:

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. Inserte datos en la nueva tabla:

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. Escriba `GO` para ejecutar los comandos anteriores:

   ```sql
   GO
   ```

### <a name="select-data"></a>Selección de datos

Ahora ejecute una consulta para devolver datos desde la tabla `Inventory`.

1. En el símbolo del sistema **sqlcmd**, escriba una consulta que devuelva filas desde la tabla `Inventory` donde la cantidad sea mayor que 152:

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. Ejecute el comando:

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>Salida del símbolo del sistema de sqlcmd

1. Para finalizar la sesión de **sqlcmd**, escriba `QUIT`:

   ```sql
   QUIT
   ```

1. Para salir de la línea de comandos interactiva del contenedor, escriba `exit`. El contenedor continuará ejecutándose después de salir del shell de Bash interactivo.

## <a id="connectexternal"></a> Conectarse desde fuera del contenedor

También puede conectarse a la instancia de SQL Server en la máquina de Docker desde cualquier herramienta externa de Linux, Windows o Mac OS que admita conexiones de SQL.

En los pasos siguientes, se usa **sqlcmd** fuera de su contenedor para conectarse a la instancia de SQL Server que se ejecuta en el contenedor. En estos pasos, se presupone que ya dispone de las herramientas de línea de comandos de SQL Server instaladas fuera de su contenedor. Los mismos principios se aplican al usar otras herramientas, pero el proceso de conexión es único para cada herramienta.

1. Busque la dirección IP de la máquina host de su contenedor. En Linux, use **ifconfig** o **ip addr**. En Windows, use **ipconfig**.

1. Ejecute sqlcmd especificando la dirección IP y el puerto asignado al puerto 1433 en el contenedor. En este ejemplo, es el mismo puerto, 1433, en el equipo host. Si especifica un puerto diferente asignado en el equipo host, se podría utilizar aquí.

   ```bash
   sqlcmd -S 10.3.2.4,1433 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1433 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. Ejecute los comandos Transact-SQL. Cuando termine, escriba `QUIT`.

Estas son otras herramientas de uso común para conectarse a SQL Server:

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) en Windows](sql-server-linux-manage-ssms.md)
- [Datos de Azure Studio (versión preliminar)](../azure-data-studio/what-is.md)
- [mssql-cli (versión preliminar)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

## <a name="remove-your-container"></a>Quitar el contenedor

Si quiere quitar el contenedor de SQL Server que se usa en este tutorial, ejecute los comandos siguientes:

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Al detener y quitar un contenedor, se eliminarán permanentemente los datos de SQL Server que contenga. Si tiene que conservar sus datos, [cree un archivo de copia de seguridad y cópielo en una ubicación externa al contenedor](tutorial-restore-backup-in-sql-server-container.md), o bien use una [técnica de persistencia de datos de contenedor](sql-server-linux-configure-docker.md#persist).

## <a name="docker-demo"></a>Demostración de Docker

Tras haber intentado usar la imagen de contenedor de SQL Server en Docker, puede que quiera saber cómo usar Docker para mejorar el desarrollo y las pruebas. En el vídeo siguiente se muestra cómo se puede usar Docker en un escenario de implementación e integración continuas.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>Pasos siguientes

Para ver un tutorial sobre cómo restaurar archivos de copia de seguridad de bases de datos en un contenedor, consulte [Restore a SQL Server database in a Linux Docker container](tutorial-restore-backup-in-sql-server-container.md) (Restaurar una base de datos de SQL Server en un contenedor de Docker en Linux). Para explorar otros escenarios, como la ejecución de varios contenedores, persistencia de datos y solución de problemas, consulte [imágenes de contenedor de configuración de SQL Server en Docker](sql-server-linux-configure-docker.md).

También puede consultar el [repositorio de Github mssql-docker](https://github.com/Microsoft/mssql-docker) para ver una serie de recursos, comentarios y problemas conocidos.
