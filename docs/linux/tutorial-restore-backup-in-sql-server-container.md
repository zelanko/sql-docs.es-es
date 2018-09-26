---
title: Restaurar una base de datos de SQL Server en Docker | Microsoft Docs
description: Este tutorial se muestra cómo restaura una copia de seguridad de base de datos de SQL Server en un nuevo contenedor de Docker de Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 9f435108414d60180d451bb874f098b15cb9b55f
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712407"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Restaurar una base de datos de SQL Server en un contenedor de Linux Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Este tutorial muestra cómo mover y restaurar un archivo de copia de seguridad de SQL Server en una imagen de contenedor de SQL Server 2017 para Linux que se ejecutan en Docker.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Este tutorial muestra cómo mover y restaurar un archivo de copia de seguridad de SQL Server en una imagen de contenedor de SQL Server de 2019 CTP 2.0 Linux que se ejecutan en Docker.

::: moniker-end

> [!div class="checklist"]
> * Extraer y ejecutar la imagen de contenedor más reciente de SQL Server para Linux.
> * Copie el archivo de base de datos de World Wide Importers en el contenedor.
> * Restaure la base de datos en el contenedor.
> * Ejecutar instrucciones Transact-SQL para ver y modificar la base de datos.
> * Copia de seguridad de la base de datos modificado.

## <a name="prerequisites"></a>Requisitos previos

* Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).
* Un mínimo de 2 GB de espacio en disco.
* Un mínimo de 2 GB de RAM.
* [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Abra un terminal de bash en Linux o Mac o en una sesión de PowerShell con privilegios elevados en Windows.

1. Extraiga la imagen de contenedor de SQL Server 2017 para Linux de Docker Hub.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > A lo largo de este tutorial, se proporcionan ejemplos de comandos de docker para el shell de bash (Linux/Mac) y PowerShell (Windows).

1. Para ejecutar la imagen de contenedor con Docker, puede usar el comando siguiente:

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   Este comando crea un contenedor de SQL Server 2017 con la edición Developer (valor predeterminado). Puerto de SQL Server **1433** se expone en el host como puerto **1401**. El elemento opcional `-v sql1data:/var/opt/mssql` parámetro crea un contenedor de volumen de datos denominado **sql1ddata**. Esto se usa para conservar los datos creados por SQL Server.

   > [!NOTE]
   > El proceso para ejecutar las ediciones de SQL Server de producción en contenedores es ligeramente diferente. Para obtener más información, vea [Run production container image](sql-server-linux-configure-docker.md#production) (Ejecutar imágenes de contenedor de producción). Si usa los mismos nombres de contenedor y los puertos, el resto de este tutorial sigue funcionando con contenedores de producción.

1. Para ver los contenedores de Docker, use el comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. Si la columna **ESTADO** muestra el estado **Activo**, esto indica que SQL Server se está ejecutando en el contenedor y que está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Abra un terminal de bash en Linux o Mac o en una sesión de PowerShell con privilegios elevados en Windows.

1. Extraiga la imagen de contenedor de SQL Server de 2019 CTP 2.0 Linux de Docker Hub.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   > [!TIP]
   > A lo largo de este tutorial, se proporcionan ejemplos de comandos de docker para el shell de bash (Linux/Mac) y PowerShell (Windows).

1. Para ejecutar la imagen de contenedor con Docker, puede usar el comando siguiente:

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   Este comando crea un contenedor de SQL Server de 2019 CTP 2.0 con la edición Developer (valor predeterminado). Puerto de SQL Server **1433** se expone en el host como puerto **1401**. El elemento opcional `-v sql1data:/var/opt/mssql` parámetro crea un contenedor de volumen de datos denominado **sql1ddata**. Esto se usa para conservar los datos creados por SQL Server.

1. Para ver los contenedores de Docker, use el comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. Si la columna **ESTADO** muestra el estado **Activo**, esto indica que SQL Server se está ejecutando en el contenedor y que está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>Cambiar la contraseña de SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>Copiar un archivo de copia de seguridad en el contenedor

Este tutorial se usa el [base de datos de ejemplo de Wide World Importers](../sample/world-wide-importers/wide-world-importers-documentation.md). Siga estos pasos para descargar y copiar el archivo de copia de seguridad de base de datos de Wide World Importers en el contenedor de SQL Server.

1. En primer lugar, use **la ejecución de docker** para crear una carpeta de copia de seguridad. El siguiente comando crea un **/var/opt/mssql/backup** directorio dentro del contenedor de SQL Server.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. A continuación, descargue el [WideWorldImporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) archivo en el equipo host. Los siguientes comandos navegue hasta el directorio principal o de usuario y se descarga el archivo de copia de seguridad como **wwi.bak**.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. Use **docker cp** para copiar el archivo de copia de seguridad en el contenedor en el **/var/opt/mssql/backup** directory.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>Restaurar la base de datos

El archivo de copia de seguridad ahora se encuentra dentro del contenedor. Antes de restaurar la copia de seguridad, es importante conocer los nombres de archivo lógico y los tipos de archivo dentro de la copia de seguridad. Los siguientes comandos de Transact-SQL inspeccionar la copia de seguridad y realizar la restauración con **sqlcmd** en el contenedor.

> [!TIP]
> Este tutorial se usa **sqlcmd** dentro del contenedor, dado que el contenedor viene con esta herramienta preinstalada. Sin embargo, también puede ejecutar instrucciones Transact-SQL con otro cliente herramientas fuera del contenedor, como [Visual Studio Code](sql-server-linux-develop-use-vscode.md) o [SQL Server Management Studio](sql-server-linux-manage-ssms.md). Para conectarse, use el puerto de host que se ha asignado al puerto 1433 en el contenedor. En este ejemplo, que es **localhost, 1401** en el equipo host y **Host_IP_Address, 1401** remotamente.

1. Ejecute **sqlcmd** dentro del contenedor a la lista de nombres de archivo lógico y rutas de acceso dentro de la copia de seguridad. Esto se realiza con el **RESTORE FILELISTONLY** instrucción Transact-SQL.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   Debería ver resultados similares al siguiente:

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. Llame a la **RESTORE DATABASE** comando para restaurar la base de datos dentro del contenedor. Especifique las rutas de acceso nuevo para cada uno de los archivos en el paso anterior.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   Debería ver resultados similares al siguiente:

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>Compruebe la base de datos restaurada

Ejecute la siguiente consulta para mostrar una lista de nombres de base de datos en el contenedor:

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

Debería ver **WideWorldImporters** en la lista de bases de datos.

## <a name="make-a-change"></a>Realice un cambio

Los pasos siguientes realizan un cambio en la base de datos.

1. Ejecutar una consulta para ver los elementos de la parte superior a 10 en el **Warehouse.StockItems** tabla.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   Debería ver una lista de nombres y los identificadores de elementos:

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. Actualizar la descripción del primer elemento con el siguiente **actualización** instrucción:

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   Debería ver resultados similares al siguiente texto:

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>Crear una nueva copia de seguridad

Una vez se haya restaurado la base de datos en un contenedor, también puede crear periódicamente copias de seguridad de base de datos dentro del contenedor en ejecución. Los pasos siguen un patrón similar a los pasos anteriores, pero en orden inverso.

1. Use la **BACKUP DATABASE** comando de Transact-SQL para crear una copia de seguridad de base de datos en el contenedor. Este tutorial crea un nuevo archivo de copia de seguridad, **wwi_2.bak**, en el que se han creado anteriormente **/var/opt/mssql/backup** directory.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   Debería ver resultados similares al siguiente:

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. A continuación, copie el archivo de copia de seguridad fuera del contenedor y en el equipo host.

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>Use los datos persistentes

Además de realizar copias de seguridad de base de datos para proteger los datos, también puede usar contenedores de volúmenes de datos. El principio de este tutorial crea el **sql1** contenedor con el `-v sql1data:/var/opt/mssql` parámetro. El **sql1data** contenedor de volúmenes de datos conserva la **/var/opt/mssql** incluso después de quita el contenedor de datos. Los pasos siguientes se quitan completamente el **sql1** contenedor y, a continuación, cree un nuevo contenedor, **sql2**, con los datos persistentes.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Detener el **sql1** contenedor.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Quitar el contenedor. Esto no elimina creado previamente **sql1data** contenedor de volúmenes de datos y los datos persistentes en él.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Crear un nuevo contenedor, **sql2**y volver a usar el **sql1data** contenedor de volúmenes de datos.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

1. La base de datos de Wide World Importers está ahora en el nuevo contenedor. Ejecutar una consulta para comprobar los cambios realizados en el anterior.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > La contraseña de SA no es la contraseña que especificó para el **sql2** contenedor, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos los datos de SQL Server se restauró desde **sql1**, incluidas la contraseña cambiada de anteriormente en el tutorial. De hecho, algunas opciones como este se omiten debido a la restauración de los datos en /var/opt/mssql. Por este motivo, la contraseña es `<YourNewStrong!Passw0rd>` como se muestra aquí.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Detener el **sql1** contenedor.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Quitar el contenedor. Esto no elimina creado previamente **sql1data** contenedor de volúmenes de datos y los datos persistentes en él.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Crear un nuevo contenedor, **sql2**y volver a usar el **sql1data** contenedor de volúmenes de datos.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
    ```

1. La base de datos de Wide World Importers está ahora en el nuevo contenedor. Ejecutar una consulta para comprobar los cambios realizados en el anterior.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > La contraseña de SA no es la contraseña que especificó para el **sql2** contenedor, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos los datos de SQL Server se restauró desde **sql1**, incluidas la contraseña cambiada de anteriormente en el tutorial. De hecho, algunas opciones como este se omiten debido a la restauración de los datos en /var/opt/mssql. Por este motivo, la contraseña es `<YourNewStrong!Passw0rd>` como se muestra aquí.

::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En este tutorial, aprendió a realizar una copia de seguridad de una base de datos en Windows y moverlo a un servidor de Linux que ejecuta SQL Server 2017. Ha aprendido a:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En este tutorial, aprendió a realizar una copia de seguridad de una base de datos en Windows y moverlo a un servidor de Linux que ejecuta SQL Server 2019 CTP 2.0. Ha aprendido a:

::: moniker-end

> [!div class="checklist"]
> * Crear imágenes de contenedor de Linux de SQL Server.
> * Copie las copias de seguridad de base de datos de SQL Server en un contenedor.
> * Ejecutar instrucciones Transact-SQL dentro del contenedor con **sqlcmd**.
> * Crear y extraer los archivos de copia de seguridad de un contenedor.
> * Usar contenedores de volúmenes de datos en Docker para conservar los datos de SQL Server.

A continuación, revisar otra configuración de Docker y escenarios de solución de problemas:

> [!div class="nextstepaction"]
>[Guía de configuración de SQL Server 2017 en Docker](sql-server-linux-configure-docker.md)
