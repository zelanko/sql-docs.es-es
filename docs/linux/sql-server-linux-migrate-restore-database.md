---
title: Migrar una base de datos de SQL Server de Windows para Linux | Microsoft Docs
description: Este tutorial muestra cómo realizar la copia de seguridad de una base de datos de SQL Server en Windows y restaurarla en una máquina Linux que ejecuta SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 7d31490369b1562db91820d0e47f5935b5b42911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713126"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migrar una base de datos de SQL Server de Windows para Linux mediante la copia de seguridad y restauración

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Copia de seguridad de SQL Server y la característica de restauración es la manera recomendada para migrar una base de datos de SQL Server en Windows para SQL Server en Linux. En este tutorial, guiará por los pasos necesarios para mover una base de datos para Linux con la copia de seguridad y restaurar técnicas.

> [!div class="checklist"]
> * Cree un archivo de copia de seguridad en Windows con SSMS
> * Instalar un shell de Bash en Windows
> * Mover el archivo de copia de seguridad para Linux desde el shell de Bash
> * Restaurar el archivo de copia de seguridad en Linux con Transact-SQL
> * Ejecutar una consulta para comprobar la migración

También puede crear un SQL Server grupo de disponibilidad AlwaysOn para migrar una base de datos de SQL Server de Windows a Linux. Consulte [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md).

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para completar este tutorial:

* Máquina de Windows con lo siguiente:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) instalado.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) instalado.
  * Base de datos de destino para migrar.

* Máquina de Linux con el software siguiente instalado:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), o [Ubuntu](quickstart-install-connect-ubuntu.md)) con las herramientas de línea de comandos.

## <a name="create-a-backup-on-windows"></a>Crear una copia de seguridad en Windows

Hay varias maneras de crear un archivo de copia de seguridad de una base de datos en Windows. Los pasos siguientes usan SQL Server Management Studio (SSMS).

1. Iniciar **SQL Server Management Studio** en el equipo de Windows.

1. En el cuadro de diálogo de conexión, escriba **localhost**.

1. En el Explorador de objetos, expanda **bases de datos**.

1. Haga clic en la base de datos de destino, seleccione **tareas**y, a continuación, haga clic en **copia de seguridad...** .

   ![Usar SSMS para crear un archivo de copia de seguridad](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. En el **copia de seguridad de base de datos** cuadro de diálogo, compruebe que **tipo de copia de seguridad** es **completa** y **copia de seguridad en** es **disco**. Tenga en cuenta el nombre y la ubicación del archivo. Por ejemplo, una base de datos denominada **YourDB** en SQL Server 2016 tiene una ruta de acceso de copia de seguridad predeterminada de `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`.

1. Haga clic en **Aceptar** realizar copias de seguridad de la base de datos.

> [!NOTE]
> Otra opción consiste en ejecutar una consulta de Transact-SQL para crear el archivo de copia de seguridad. El siguiente comando de Transact-SQL realiza las mismas acciones que los pasos anteriores para una base de datos denominada **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Instalar un shell de Bash en Windows

Para restaurar la base de datos, primero debe transferir el archivo de copia de seguridad de la máquina de Windows a la máquina de Linux de destino. En este tutorial, se mueva el archivo a Linux desde un shell de Bash (ventana de terminal) que se ejecutan en Windows.

1. Instalar un shell de Bash en la máquina de Windows que admita la **scp** (secure copy) y **ssh** comandos (inicio de sesión remoto). Se incluyen dos ejemplos:

   * El [subsistema Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * El Shell de Bash de Git ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Abra una sesión de Bash en Windows.

## <a id="scp"></a> Copie el archivo de copia de seguridad en Linux

1. En la sesión de Bash, navegue hasta el directorio que contiene el archivo de copia de seguridad. Por ejemplo:

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. Use la **scp** comando para transferir el archivo a la máquina de Linux de destino. Las siguientes transferencias de ejemplo **YourDB.bak** en el directorio principal de *user1* en el servidor Linux con la dirección IP *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![comando de SCP](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> Hay alternativas al uso de scp para transferir archivos. Una consiste en usar [Samba](https://help.ubuntu.com/community/Samba) para configurar un recurso compartido de red SMB entre Windows y Linux. Para ver un tutorial en Ubuntu, consulte [cómo crear un recurso compartido de red a través de Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Una vez establecida, puede acceder a él como un archivo de red comparten desde Windows, como  **\\ \\machinenameorip\\compartir**.

## <a name="move-the-backup-file-before-restoring"></a>Mueva el archivo de copia de seguridad antes de restaurar

En este momento, el archivo de copia de seguridad está en el servidor de Linux en su directorio particular de usuario. Antes de restaurar la base de datos a SQL Server, debe colocar la copia de seguridad en un subdirectorio de **/var/opt/mssql**.

1. En la misma sesión de Bash Windows conectarse remotamente a la máquina de destino de Linux con **ssh**. En el siguiente ejemplo se conecta a la máquina Linux **192.0.2.9** como usuario **user1**.

   ```bash
   ssh user1@192.0.2.9
   ```

   Ahora se ejecutan comandos en el servidor remoto de Linux.

1. ENTRAR en modo de superusuario.

   ```bash
   sudo su
   ```

1. Cree un nuevo directorio de copia de seguridad. El parámetro -p no hace nada si el directorio ya existe.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. Mueva el archivo de copia de seguridad a ese directorio. En el ejemplo siguiente, el archivo de copia de seguridad reside en el directorio principal de *user1*. Cambiar el comando para que coincida con el nombre de archivo y la ubicación del archivo de copia de seguridad.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. Salir del modo de superusuario.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Restaurar la base de datos en Linux

Para restaurar la copia de seguridad de base de datos, puede usar el **RESTORE DATABASE** comando Transact-SQL (TQL).

> [!NOTE]
> Los pasos siguientes usan la **sqlcmd** herramienta. Si no lo ha hecho instalar herramientas de SQL Server, vea [herramientas de línea de comandos de instalación de SQL Server en Linux](sql-server-linux-setup-tools.md).

1. En el mismo terminal, inicie **sqlcmd**. En el siguiente ejemplo se conecta a la instancia de SQL Server local con el **SA** usuario. Escriba la contraseña cuando se le solicite, o especifique la contraseña mediante la adición de la **-P** parámetro.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. En el `>1` símbolo del sistema, escriba lo siguiente **RESTORE DATABASE** comando, presione ENTRAR después de cada línea (no se puede copiar y pegar todo el comando de varias líneas a la vez). Reemplace todas las apariciones de `YourDB` con el nombre de la base de datos.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   Obtendrá un mensaje de que la base de datos se restauraron correctamente.

   `RESTORE DATABASE` puede devolver un error similar al ejemplo siguiente:

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   En este caso, la base de datos contiene archivos secundarios. Si estos archivos no se especifican en el `MOVE` cláusula de `RESTORE DATABASE`, el procedimiento de restauración intentará crearlos en la misma ruta que el servidor original. 

   Puede enumerar todos los archivos incluidos en la copia de seguridad:
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   Debería obtener una lista como la siguiente (enumerar solo las primeras dos columnas):
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   Puede usar esta lista para crear `MOVE` cláusulas para los archivos adicionales. En este ejemplo, el `RESTORE DATABASE` es:

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. Compruebe la restauración con una lista de todas las bases de datos en el servidor. Debe aparecer la base de datos restaurada.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. Ejecutar otras consultas en la base de datos migrada. El siguiente comando cambia el contexto para el **YourDB** selecciona las filas de una de sus tablas y base de datos.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. Cuando haya terminado con **sqlcmd**, tipo `exit`.

1. Cuando haya terminado trabajando en el servidor remoto **ssh** sesión, escriba `exit` nuevo.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprendió a realizar una copia de seguridad de una base de datos en Windows y moverlo a un servidor de Linux que ejecuta SQL Server. Ha aprendido a:
> [!div class="checklist"]
> * Usar SSMS y Transact-SQL para crear un archivo de copia de seguridad en Windows
> * Instalar un shell de Bash en Windows
> * Use **scp** para mover los archivos de copia de seguridad de Windows para Linux
> * Use **ssh** conectarse remotamente a la máquina Linux
> * Reubicar el archivo de copia de seguridad para preparar la restauración
> * Use **sqlcmd** para ejecutar comandos de Transact-SQL
> * Restaurar la copia de seguridad de base de datos con el **RESTORE DATABASE** comando 
> * Ejecute la consulta para comprobar la migración

A continuación, explorar otros escenarios de migración de SQL Server en Linux. 

> [!div class="nextstepaction"]
>[Migrar bases de datos a SQL Server en Linux](sql-server-linux-migrate-overview.md)
