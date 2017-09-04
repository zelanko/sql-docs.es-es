---
title: "Introducción a SQL Server 2017 en Docker | Documentos de Microsoft"
description: "Este tutorial de inicio rápido muestra cómo usar Docker para ejecutar la imagen de contenedor de 2017 de SQL Server. A continuación, crear y consultar una base de datos con sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.translationtype: MT
ms.sourcegitcommit: 303d3b74da3fe370d19b7602c0e11e67b63191e7
ms.openlocfilehash: 10623562f57ae1b4b571dd2e5b7dad56b81b8f8b
ms.contentlocale: es-es
ms.lasthandoff: 08/29/2017

---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Ejecutar la imagen de contenedor de SQL Server 2017 con Docker

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tutorial de inicio rápido, usar Docker para extraer y ejecutar la imagen de contenedor de SQL Server de 2017 RC2, [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). A continuación, conecte con **sqlcmd** para crear la primera base de datos y ejecutar consultas.

Esta imagen se compone de SQL Server que se ejecutan en Linux en función de Ubuntu 16.04. Se puede utilizar con el motor de Docker 1.8 + en Linux o en Docker para Mac y Windows.

> [!NOTE]
> Esta guía de inicio rápido se centra específicamente en medio de la imagen mssql-server-linux. La imagen de Windows no está cubierta, pero puede obtener más información sobre la [página de Docker Hub de windows del servidor mssql](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a id="requirements"></a> Requisitos previos

- Motor de docker 1.8 + en cualquier admite la distribución de Linux o Docker para Mac y Windows.
- Mínimo de 4 GB de espacio en disco
- Mínimo de 4 GB de RAM
- [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

> [!IMPORTANT]
> El valor predeterminado en Docker para Mac y Docker para Windows es 2 GB para la VM Moby, por lo que debe cambiarse a 4 GB. Si se ejecuta en Mac o Windows, use los procedimientos siguientes para aumentar la memoria.

### <a name="increase-docker-memory-to-4-gb-mac"></a>Aumente la memoria de Docker a 4 GB (Mac)

Los siguientes pasos aumentar la memoria para Docker para Mac a 4 GB.

1. Haga clic en el logotipo de Docker en la barra de estado superior.
1. Seleccione **preferencias**.
1. Mueva el indicador de memoria a 4 GB o más.
1. Haga clic en el **reiniciar** situado en el botón de la pantalla.

### <a name="increase-docker-memory-to-4-gb-windows"></a>Aumente la memoria de Docker a 4 GB (Windows)

Los siguientes pasos aumentar la memoria de Docker para Windows a 4 GB.

1. Haga doble clic en el icono de Docker desde la barra de tareas.
1. Haga clic en **configuración** en ese menú.
1. Haga clic en el **avanzadas** ficha.
1. Mueva el indicador de memoria a 4 GB o más.
1. Haga clic en el **aplicar** botón.

## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

1. Extraiga la imagen del contenedor de Docker Hub.

    ```bash
    docker pull microsoft/mssql-server-linux
    ```

    > [!TIP]
    > Para Linux, dependiendo de la configuración de usuario y del sistema, tendrá que incluir cada `docker` con `sudo`.

    > [!NOTE]
    > El comando anterior, extrae la última imagen de contenedor de SQL Server. Si desea extraer una imagen específica, agregue un coma y el nombre de etiqueta (por ejemplo, `microsoft/mssql-server-linux:rc1`). Para ver todas las imágenes disponibles, vea [la página del concentrador mssql-server-linux Docker](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Para ejecutar la imagen del contenedor con Docker, puede utilizar el siguiente comando desde un shell de bash (Linux/macOS):

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    Si usas Docker para Windows, utilice el siguiente comando desde un símbolo con privilegios elevados PowerShell:

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    > [!NOTE]
    > La única diferencia entre el ejemplo intensiva de errores (Linux/macOS) y el ejemplo de PowerShell (Windows) está entre comillas simples y comillas dobles alrededor de las variables de entorno. Se produce un error en el comando docker run si usas uno erróneo. En el resto de este tema, intensiva de errores y bloques de código de PowerShell se proporcionan por comodidad. Si hay solo un ejemplo, funciona en todas las plataformas, incluidos Windows.

    En la tabla siguiente proporciona una descripción de los parámetros en la versión anterior `docker run` ejemplo:

    | Parámetro | Description |
    |-----|-----|
    | **-e ' ACCEPT_EULA = S '** |  Establecer el **ACCEPT_EULA** variable en cualquier valor para confirmar la aceptación de la [el contrato de licencia de usuario final](http://go.microsoft.com/fwlink/?LinkId=746388). Requiere configuración para la imagen de SQL Server. |
    | **-e ' MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>'** | Especifique su propia contraseña segura que es al menos 8 caracteres y se ajuste [requisitos de contraseña de SQL Server](../relational-databases/security/password-policy.md). Requiere configuración para la imagen de SQL Server. |
    | **-e ' MSSQL_PID = Developer'** | Especifica la clave de producto o de edición. En este ejemplo, se usa la edición Developer libremente con licencia para las pruebas no sean de producción. Para otros valores, vea [configuración configurar SQL Server con las variables de entorno en Linux](sql-server-linux-configure-environment-variables.md). |
    | **--SYS_PTRACE de Agregar extremo** | Agrega la capacidad de Linux para realizar el seguimiento de un proceso. Esto permite a SQL Server generar volcados en una excepción. |
    | **-p 1401:1433** | Asignar un puerto TCP en el entorno de host (el primer valor) con un puerto TCP en el contenedor (el segundo valor). En este ejemplo, SQL Server está escuchando en TCP 1433 en el contenedor y se expone al puerto, 1401, en el host. |
    | **Microsoft/mssql-server-linux** | La imagen de contenedor de SQL Server para Linux. A menos que se especifique lo contrario, el valor predeterminado es el **más reciente** imagen. |

1. Para ver los contenedores de Docker, use el `docker ps` comando.

    ```bash
    docker ps -a
    ```

    Debería ver un resultado similar a la captura de pantalla siguiente:

    ![Resultado del comando de docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Si el **estado** columna muestra un estado de **una**, a continuación, se ejecuta SQL Server en el contenedor y escucha en el puerto especificado en el **puertos** columna. Si el **estado** columna para el contenedor se muestra en SQL Server **Exited**, consulte el [sección de la Guía de configuración de solución de problemas](sql-server-linux-configure-docker.md#troubleshooting).

Hay dos útil `docker run` opciones no utilizadas en el ejemplo anterior por motivos de simplicidad. El `-h` parámetro (nombre de host) cambia el nombre interno del contenedor en un valor personalizado. Esto es el nombre, verá que se devuelven en la siguiente consulta de Transact-SQL:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

También puede encontrar el `--name` parámetro útil para el nombre de su contenedor, en lugar de tener un nombre de contenedor generado. Establecer `-h` y `--name` en el mismo valor, es una buena manera de identificar fácilmente el contenedor de destino.

## <a name="change-the-sa-password"></a>Cambiar la contraseña de SA

La cuenta SA es un administrador del sistema en la instancia de SQL Server que se crea durante la instalación. Después de crear el contenedor de SQL Server, el `MSSQL_SA_PASSWORD` variable de entorno especificada es detectable mediante la ejecución de `echo $MSSQL_SA_PASSWORD` en el contenedor. Por motivos de seguridad, cambie la contraseña de SA.

1. Elija una contraseña segura que se usará para el usuario de SA.

1. Use `docker exec` para ejecutar **sqlcmd** para cambiar la contraseña mediante Transact-SQL. Reemplace `<Old Password>` y `<New Password>` con sus valores de contraseña.

> ```bash
> docker exec -it <Container ID> /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<Old Password>' -Q 'ALTER LOGIN SA WITH PASSWORD="<New Password>";'
> ```

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Los pasos siguientes utilizan la herramienta de línea de comandos de SQL Server, **sqlcmd**, dentro del contenedor para conectarse a SQL Server.

1. Use la `docker exec -it` comando para iniciar un shell de bash interactivo dentro de su contenedor en ejecución. En el ejemplo siguiente `e69e056c702d` es el identificador del contenedor.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > No siempre tendrá que especificar el identificador del contenedor todo. Solamente debe especificar suficientes caracteres para identificar de forma exclusiva. Por lo que en este ejemplo, es posible que sea suficiente para usar `e6` o `e69` en lugar del identificador completo.

1. Una vez dentro del contenedor, conectar localmente con sqlcmd. Sqlcmd no está en la ruta de acceso de forma predeterminada, por lo que debe especificar la ruta de acceso completa.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
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

## <a name="connect-from-outside-the-container"></a>Conectarse desde fuera del contenedor

También puede conectarse a la instancia de SQL Server en el equipo de Docker desde cualquier herramienta externa de Linux, Windows o Mac OS que admite las conexiones de SQL.

Los siguientes pasos se usa **sqlcmd** fuera de su contenedor para conectarse a SQL Server que se ejecutan en el contenedor. Estos pasos se supone que ya tiene las herramientas de línea de comandos de SQL Server instaladas fuera de su contenedor. Las mismas entidades que se aplican al usar otras herramientas, pero el proceso de conexión es único para cada herramienta.

1. Buscar la dirección IP para el equipo que hospeda el contenedor. En Linux, use **ifconfig** o **ip addr**. En Windows, utilice **ipconfig**.

1. Ejecute sqlcmd especificando la dirección IP y el puerto asignado al puerto 1433 en el contenedor. En este ejemplo, es el puerto 1401 en el equipo host.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
   ```

1. Ejecute comandos de Transact-SQL. Cuando termine, escriba `QUIT`.

Otras herramientas comunes para conectarse a SQL Server incluyen:

- [Código de Visual Studio](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) en Windows](sql-server-linux-develop-use-ssms.md)

## <a name="next-steps"></a>Pasos siguientes

Para explorar otros escenarios, como la ejecución de varios contenedores, persistencia de los datos y solución de problemas, consulte [configurar SQL Server 2017 imágenes del contenedor en Docker](sql-server-linux-configure-docker.md).

Asimismo, consulte la [repositorio de GitHub de docker mssql](https://github.com/Microsoft/mssql-docker) para los recursos, comentarios y problemas conocidos.

