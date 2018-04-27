---
title: Restaurar una base de datos de SQL Server en Docker | Documentos de Microsoft
description: Este tutorial muestra cómo restaurar una copia de seguridad de base de datos de SQL Server en un nuevo contenedor de Linux Docker.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: ad11495a927d5ca37e15cb872a200a55beb93b35
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Restaurar una base de datos de SQL Server en un contenedor Linux Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial muestra cómo mover y restaurar un archivo de copia de seguridad de SQL Server en una imagen de contenedor de SQL Server de 2017 Linux con Docker.

> [!div class="checklist"]
> * Extraer y ejecutar la imagen de contenedor más reciente de SQL Server para Linux de 2017.
> * Copie el archivo de base de datos de World Wide Importers en el contenedor.
> * Restaure la base de datos en el contenedor.
> * Ejecutar instrucciones de Transact-SQL para ver y modificar la base de datos.
> * Copia de seguridad de la base de datos modificada.

## <a name="prerequisites"></a>Requisitos previos

* Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).
* Un mínimo de 2 GB de espacio en disco.
* Un mínimo de 2 GB de RAM.
* [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="pull-and-run-the-container-image"></a>Extraer y ejecutar la imagen de contenedor

1. Abra un terminal de bash en Linux/Mac o una sesión de PowerShell con privilegios elevados en Windows.

1. Extraiga la imagen de contenedor de SQL Server 2017 para Linux de Docker Hub.

    ```bash
    sudo docker pull microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker pull microsoft/mssql-server-linux:2017-latest
    ```

    > [!TIP]
    > A lo largo de este tutorial, se proporcionan ejemplos de comandos de docker para el shell de bash (Linux/Mac) y PowerShell (Windows).

1. Para ejecutar la imagen del contenedor con Docker, puede usar el comando siguiente:

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql1' -p 1401:1433 \
       -v sql1data:/var/opt/mssql \
       -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql1" -p 1401:1433 `
       -v sql1data:/var/opt/mssql `
       -d microsoft/mssql-server-linux:2017-latest
    ```

    Este comando crea un contenedor de 2017 de SQL Server con la edición Developer (valor predeterminado). Puerto de SQL Server **1433** se expone en el host como puerto **1401**. Opcional `-v sql1data:/var/opt/mssql` parámetro crea un contenedor de volumen de datos denominado **sql1ddata**. Esto se utiliza para conservar los datos creados por SQL Server.

   > [!NOTE]
   > El proceso para ejecutar las ediciones de SQL Server de producción en contenedores es ligeramente diferente. Para obtener más información, vea [Run production container image](sql-server-linux-configure-docker.md#production) (Ejecutar imágenes de contenedor de producción). Si utiliza los mismos nombres de contenedor y puertos, el resto de este tutorial sigue funcionando con contenedores de producción.

1. Para ver los contenedores de Docker, use el comando `docker ps`.

    ```bash
    sudo docker ps -a
    ```

    ```PowerShell
    docker ps -a
    ```
 
1. Si la columna **ESTADO** muestra el estado **Activo**, esto indica que SQL Server se está ejecutando en el contenedor y que está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

   ```
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        microsoft/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

## <a name="change-the-sa-password"></a>Cambiar la contraseña de SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>Copiar un archivo de copia de seguridad en el contenedor

Este tutorial se usa el [base de datos de ejemplo Wide World Importers](../sample/world-wide-importers/wide-world-importers-documentation.md). Siga estos pasos para descargar y copiar el archivo de copia de seguridad de base de datos de Wide World Importers en el contenedor de SQL Server.

1. En primer lugar, use **ejecución de docker** para crear una carpeta de copia de seguridad. El comando siguiente crea un **/var/opt/mssql/** directorio dentro del contenedor de SQL Server.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. A continuación, descargue el [WideWorldImporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) archivo en el equipo host. Los siguientes comandos navegue al directorio de inicio/usuarios y descarga el archivo de copia de seguridad como **wwi.bak**.

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

El archivo de copia de seguridad se encuentra dentro del contenedor. Antes de restaurar la copia de seguridad, es importante conocer los nombres de archivo lógico y tipos de archivo dentro de la copia de seguridad. Los siguientes comandos de Transact-SQL inspeccionar la copia de seguridad y realizar la restauración con **sqlcmd** en el contenedor.

> [!TIP]
> Este tutorial usa **sqlcmd** dentro del contenedor, dado que el contenedor viene con esta herramienta previamente instalada. Sin embargo, también puede ejecutar instrucciones Transact-SQL con otro cliente herramientas fuera del contenedor, como [código de Visual Studio](sql-server-linux-develop-use-vscode.md) o [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md). Para conectarse, use el puerto de host que se ha asignado al puerto 1433 en el contenedor. En este ejemplo, que es **localhost, 1401** en el equipo host y **Host_IP_Address, 1401** remotamente.

1. Ejecutar **sqlcmd** dentro del contenedor de lista de nombres de archivo lógicos y las rutas de acceso dentro de la copia de seguridad. Esto se realiza con el **RESTORE FILELISTONLY** instrucción Transact-SQL.

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

   Debería ver un resultado similar al siguiente:

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. Llame a la **RESTORE DATABASE** comando para restaurar la base de datos dentro del contenedor. Especificar rutas de acceso nuevo para cada uno de los archivos en el paso anterior.

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

   Debería ver un resultado similar al siguiente:

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

Ejecute la consulta siguiente para mostrar una lista de nombres de base de datos en el contenedor:

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

## <a name="make-a-change"></a>Realiza un cambio

Los siguientes pasos realiza un cambio en la base de datos.

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

   Debería ver una lista de identificadores de elemento y nombres de:

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

1. Actualizar la descripción del primer elemento con la siguiente **actualización** instrucción:

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

   Debería ver un resultado similar al siguiente texto:

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>Crear una nueva copia de seguridad

Una vez se haya restaurado la base de datos en un contenedor, que le interese crear periódicamente copias de seguridad de base de datos dentro del contenedor en ejecución. Los pasos siguen un patrón similar a los pasos anteriores, pero en orden inverso.

1. Use la **copia de seguridad de la base de datos** comando de Transact-SQL para crear una copia de seguridad de base de datos en el contenedor. Este tutorial crea un nuevo archivo de copia de seguridad, **wwi_2.bak**, en el que se han creado anteriormente **/var/opt/mssql/backup** directory.

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

   Debería ver un resultado similar al siguiente:

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

## <a name="use-the-persisted-data"></a>Utilice los datos persistentes

Además de realizar copias de seguridad de base de datos para proteger los datos, también puede utilizar los contenedores de volúmenes de datos. El principio de este tutorial crea el **sql1** contenedor con el `-v sql1data:/var/opt/mssql` parámetro. El **sql1data** contenedor de volúmenes de datos conserva la **/var/opt/mssql** datos incluso después de quita el contenedor. Los siguientes pasos quitan completamente el **sql1** contenedor y, a continuación, cree un nuevo contenedor, **sql2**, con los datos persistentes.

1. Detener el **sql1** contenedor.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Quitar el contenedor. Esto no elimina creado previamente **sql1data** contenedor de volúmenes de datos y los datos almacenados en ella.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Crear un nuevo contenedor, **sql2**, y volver a la **sql1data** contenedor de volúmenes de datos.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

1. La base de datos de Wide World Importers ahora está en el nuevo contenedor. Ejecutar una consulta para comprobar el cambio anterior realizado.

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
   > La contraseña de SA no es la contraseña que especificó para la **sql2** contenedor, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos los datos de SQL Server se restauró desde **sql1**, incluidas la contraseña cambiada de anteriormente en el tutorial. En efecto, se omiten algunas opciones así debido a la restauración de los datos en /var/opt/mssql. Por esta razón, la contraseña es `<YourNewStrong!Passw0rd>` tal y como se muestra aquí.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprendió a realizar la copia de seguridad de una base de datos en Windows y moverlo a un servidor de Linux que se ejecuta SQL Server 2017 RC2. También habrá aprendido cómo para:
> [!div class="checklist"]
> * Crear imágenes de contenedor de SQL Server para Linux de 2017.
> * Copie las copias de seguridad de base de datos de SQL Server en un contenedor.
> * Ejecutar instrucciones de Transact-SQL en el contenedor con **sqlcmd**.
> * Crear y extraer los archivos de copia de seguridad de un contenedor.
> * Utilizar contenedores de volúmenes de datos en Docker para conservar los datos de SQL Server.

A continuación, revise otra configuración de Docker y escenarios de solución de problemas:

> [!div class="nextstepaction"]
>[Guía de configuración de SQL Server 2017 en Docker](sql-server-linux-configure-docker.md)
