---
title: "Introducción a SQL Server 2017 en Docker | Documentos de Microsoft"
description: "Este tutorial rápido muestra cómo usar Docker para ejecutar la imagen de contenedor de 2017 de SQL Server. A continuación, crear y consultar una base de datos con sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.workload: Active
ms.openlocfilehash: 0fcd5cefc02359d407b1799e4cc31ed5afa3c818
ms.sourcegitcommit: 73043fe1ac5d60b67e33b44053c0a7733b98bc3d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/23/2017
---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Ejecutar la imagen de contenedor de SQL Server 2017 con Docker

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tutorial rápido, usar Docker para extraer y ejecutar la imagen de contenedor 2017 de SQL Server, [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). A continuación, conecte con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

Esta imagen se compone de SQL Server que se ejecutan en Linux en función de Ubuntu 16.04. Se puede utilizar con el motor de Docker 1.8 + en Linux o en Docker para Mac y Windows.

> [!NOTE]
> Este tutorial se centra específicamente en usando el mssql-server -**linux** imagen. La imagen de Windows no está cubierta, pero puede obtener más información sobre la [mssql-server-windows-página para desarrolladores Docker Hub](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a id="requirements"></a> Prerequisites

- Motor de docker 1.8 + en cualquier admite la distribución de Linux o Docker para Mac y Windows. Para obtener más información, consulte [instalar Docker](https://docs.docker.com/engine/installation/).
- Mínimo de 2 GB de espacio en disco
- Mínimo de 2 GB de RAM
- [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

1. Extraiga la imagen de contenedor de SQL Server para Linux de 2017 de Docker Hub.

   ```bash
   sudo docker pull microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   El ejemplo anterior extrae la última imagen de contenedor de 2017 de SQL Server. Si desea extraer una imagen específica, agregue un coma y el nombre de etiqueta (por ejemplo, `microsoft/mssql-server-linux:2017-GA`). Para ver todas las imágenes disponibles, vea [la página del concentrador mssql-server-linux Docker](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Para ejecutar la imagen del contenedor con Docker, puede utilizar el siguiente comando desde un shell de bash (Linux/macOS) o la línea de comandos de PowerShell con privilegios elevados.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1401:1433 --name sql1 \
      -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1401:1433 --name sql1 `
      -d microsoft/mssql-server-linux:2017-latest
   ```

   > [!NOTE]
   > De forma predeterminada, esto crea un contenedor con la edición para desarrolladores de SQL Server 2017. El proceso para ejecutar las ediciones de producción en contenedores es ligeramente diferente. Para obtener más información, consulte [ejecutar producción imágenes del contenedor](sql-server-linux-configure-docker.md#production).

   En la tabla siguiente proporciona una descripción de los parámetros en la versión anterior `docker run` ejemplo:

   | Parámetro | Description |
   |-----|-----|
   | **-e ' ACCEPT_EULA = S '** |  Establecer el **ACCEPT_EULA** variable en cualquier valor para confirmar la aceptación de la [el contrato de licencia de usuario final](http://go.microsoft.com/fwlink/?LinkId=746388). Requiere configuración para la imagen de SQL Server. |
   | **-e ' MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>'** | Especifique su propia contraseña segura que es al menos 8 caracteres y se ajuste el [requisitos de contraseña de SQL Server](../relational-databases/security/password-policy.md). Requiere configuración para la imagen de SQL Server. |
   | **-p 1401:1433** | Asignar un puerto TCP en el entorno de host (el primer valor) con un puerto TCP en el contenedor (el segundo valor). En este ejemplo, SQL Server está escuchando en TCP 1433 en el contenedor y se expone al puerto, 1401, en el host. |
   | **--nombre sql1** | Especifique un nombre personalizado para el contenedor en lugar de uno generada aleatoriamente. Si ejecuta más de un contenedor, no se puede reutilizar este mismo nombre. |
   | **Microsoft/mssql-server-linux:2017-más reciente** | La imagen de contenedor de SQL Server para Linux de 2017. |

1. Para ver los contenedores de Docker, use el `docker ps` comando.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   Debería ver un resultado similar a la captura de pantalla siguiente:

   ![Resultado del comando de docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Si el **estado** columna muestra un estado de **una**, a continuación, se ejecuta SQL Server en el contenedor y escucha en el puerto especificado en el **puertos** columna. Si el **estado** columna para el contenedor se muestra en SQL Server **Exited**, consulte el [sección de la Guía de configuración de solución de problemas](sql-server-linux-configure-docker.md#troubleshooting).

El `-h` (nombre de host) parámetro también es útil, pero no se utiliza en este tutorial para simplificar el trabajo. Esto cambia el nombre interno del contenedor en un valor personalizado. Esto es el nombre, verá que se devuelven en la siguiente consulta de Transact-SQL:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Establecer `-h` y `--name` en el mismo valor, es una buena manera de identificar fácilmente el contenedor de destino.

## <a name="change-the-sa-password"></a>Cambiar la contraseña de SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Los pasos siguientes utilizan la herramienta de línea de comandos de SQL Server, **sqlcmd**, dentro del contenedor para conectarse a SQL Server.

1. Use la `docker exec -it` comando para iniciar un shell de bash interactivo dentro de su contenedor en ejecución. En el ejemplo siguiente `sql1` nombre especificado por el `--name` parámetro al crear el contenedor.

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. Una vez dentro del contenedor, conectar localmente con sqlcmd. Sqlcmd no está en la ruta de acceso de forma predeterminada, por lo que debe especificar la ruta de acceso completa.

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

1. Para salir de la línea de comandos interactiva del contenedor, escriba `exit`. El contenedor continúa ejecutándose después de salir del shell de bash interactivo.

## <a id="connectexternal"></a>Conectarse desde fuera del contenedor

También puede conectarse a la instancia de SQL Server en el equipo de Docker desde cualquier herramienta externa de Linux, Windows o Mac OS que admite las conexiones de SQL.

Los siguientes pasos se usa **sqlcmd** fuera de su contenedor para conectarse a SQL Server que se ejecutan en el contenedor. Estos pasos se supone que ya tiene las herramientas de línea de comandos de SQL Server instaladas fuera de su contenedor. Las mismas entidades que se aplican al usar otras herramientas, pero el proceso de conexión es único para cada herramienta.

1. Buscar la dirección IP para el equipo que hospeda el contenedor. En Linux, use **ifconfig** o **ip addr**. En Windows, utilice **ipconfig**.

1. Ejecute sqlcmd especificando la dirección IP y el puerto asignado al puerto 1433 en el contenedor. En este ejemplo, es el puerto 1401 en el equipo host.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. Ejecute comandos de Transact-SQL. Cuando termine, escriba `QUIT`.

Otras herramientas comunes para conectarse a SQL Server incluyen:

- [Código de Visual Studio](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) en Windows](sql-server-linux-develop-use-ssms.md)
- [Studio de operaciones de SQL Server (versión preliminar)](../sql-operations-studio/what-is.md)
- [MSSQL-cli (versión preliminar)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

## <a name="remove-your-container"></a>Quitar el contenedor

Si desea quitar el contenedor de SQL Server que se usan en este tutorial, ejecute los siguientes comandos:

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Detener y quitar un contenedor de forma permanente eliminan los datos de SQL Server en el contenedor. Si tiene que conservar los datos, [crear y copiar un archivo de copia de seguridad fuera del contenedor](tutorial-restore-backup-in-sql-server-container.md) o usar un [técnica de persistencia de datos de contenedor](sql-server-linux-configure-docker.md#persist).

## <a name="docker-demo"></a>Demostración de docker

Una vez que se ha intentado usar la imagen de contenedor de SQL Server para Docker, debe saber cómo Docker se usa para mejorar el desarrollo y las pruebas. El vídeo siguiente muestra cómo se puede utilizar Docker en un escenario de implementación y la integración continua.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>Pasos siguientes

Para obtener un tutorial sobre cómo restaurar archivos de copia de seguridad de base de datos en un contenedor, consulte [restaurar una base de datos de SQL Server en un contenedor Linux Docker](tutorial-restore-backup-in-sql-server-container.md). Para explorar otros escenarios, como la ejecución de varios contenedores, persistencia de los datos y solución de problemas, consulte [configurar SQL Server 2017 imágenes del contenedor en Docker](sql-server-linux-configure-docker.md).

Asimismo, consulte la [repositorio de GitHub de docker mssql](https://github.com/Microsoft/mssql-docker) para los recursos, comentarios y problemas conocidos.
