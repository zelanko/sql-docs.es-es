---
title: Migrar una base de datos de SQL Server de Windows a Linux | Documentos de Microsoft
description: "Este tutorial muestra cómo realizar la copia de seguridad de una base de datos de SQL Server en Windows y restaurarlo a una máquina de Linux que se ejecuta SQL Server 2017."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/16/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: a6d84942bfd13d672b3c59416cb64d2ae41ee10f
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migrar una base de datos de SQL Server de Windows para Linux con backup y restore

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Copia de seguridad de SQL Server y la característica de restauración es la manera recomendada para migrar una base de datos de SQL Server en Windows a SQL Server 2017 en Linux. En este tutorial le guiará a través de los pasos necesarios para mover una base de datos de Linux con copia de seguridad y restauración técnicas.

> [!div class="checklist"]
> * Crear un archivo de copia de seguridad en Windows con SSMS
> * Instalar un shell de Bash en Windows
> * Mover el archivo de copia de seguridad para Linux desde el shell de Bash
> * Restaurar el archivo de copia de seguridad en Linux con Transact-SQL
> * Ejecutar una consulta para comprobar la migración

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para completar este tutorial:

* Máquina de Windows con lo siguiente:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) instalado.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) instalado.
  * Base de datos de destino para migrar.

* Máquina Linux con instalado lo siguiente:
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), o [Ubuntu](quickstart-install-connect-ubuntu.md)) con las herramientas de línea de comandos.

## <a name="create-a-backup-on-windows"></a>Cree una copia de seguridad en Windows

Hay varias maneras de crear un archivo de copia de seguridad de una base de datos en Windows. Los pasos siguientes utilizan SQL Server Management Studio (SSMS).

1. Iniciar **SQL Server Management Studio** en su equipo de Windows.

1. En el cuadro de diálogo de conexión, escriba **localhost**.

1. En el Explorador de objetos, expanda **bases de datos**.

1. Haga clic en la base de datos de destino, seleccione **tareas**y, a continuación, haga clic en **realizar copias de seguridad...** .

   ![Usar SSMS para crear un archivo de copia de seguridad](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. En el **copia de seguridad de la base de datos** cuadro de diálogo, compruebe que **tipo de copia de seguridad** es **completa** y **copia de seguridad en** es **disco**. Anote el nombre y la ubicación del archivo. Por ejemplo, una base de datos denominada **YourDB** en SQL Server 2016 tiene una ruta de acceso de copia de seguridad predeterminada de `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`.

1. Haga clic en **Aceptar** para hacer copia de seguridad de la base de datos.

> [!NOTE]
> Otra opción es ejecutar una consulta de Transact-SQL para crear el archivo de copia de seguridad. El siguiente comando de Transact-SQL realiza las mismas acciones que los pasos anteriores para una base de datos denominada **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Instalar un shell de Bash en Windows

Para restaurar la base de datos, primero debe transferir el archivo de copia de seguridad de la máquina de Windows en el equipo de Linux de destino. En este tutorial, se mueve el archivo Linux desde un shell de Bash (ventana de terminal) con Windows.

1. Instalar un shell de Bash en su equipo de Windows que admite la **scp** (secure copia) y **ssh** comandos (inicio de sesión remoto). Dos ejemplos:

   * El [subsistema de Windows para Linux](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * El Shell de Bash Git ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Abra una sesión de Bash en Windows.

## <a id="scp"></a>Copie el archivo de copia de seguridad en Linux

1. En la sesión intensiva de errores, desplácese al directorio que contiene el archivo de copia de seguridad. Por ejemplo:

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. Use la **scp** comando para transferir el archivo en el equipo de Linux de destino. Las transferencias de ejemplo siguiente **YourDB.bak** al directorio particular de *user1* en el servidor Linux con una dirección IP de *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![comando de SCP](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> Hay alternativas al uso de scp para transferencia de archivos. Una consiste en usar [Samba](https://help.ubuntu.com/community/Samba) para configurar un recurso compartido de red SMB entre Windows y Linux. Para ver un tutorial en Ubuntu, consulte [cómo crear un recurso compartido de red a través de Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Una vez establecida, puede tener acceso a él como un archivo de red comparten en Windows, como  **\\ \\machinenameorip\\compartir**.

## <a name="move-the-backup-file-before-restoring"></a>Mueva el archivo de copia de seguridad antes de restaurar

En este punto, el archivo de copia de seguridad está en el servidor de Linux en el directorio particular de sus usuarios. Antes de restaurar la base de datos a SQL Server, debe colocar la copia de seguridad en un subdirectorio de **/var/opt/mssql**.

1. En la misma sesión de Windows Bash conectarse de forma remota a su equipo de Linux de destino con **ssh**. En el siguiente ejemplo se conecta a la máquina Linux **192.0.2.9** como usuario **user1**.

   ```bash
   ssh user1@192.0.2.9
   ```

   Ahora se ejecuta comandos en el servidor remoto de Linux.

1. ENTRAR en el modo de superusuario.

   ```bash
   sudo su
   ```

1. Crear un nuevo directorio de copia de seguridad. El parámetro -p no hace nada si el directorio ya existe.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. Mueva el archivo de copia de seguridad a ese directorio. En el ejemplo siguiente, el archivo de copia de seguridad reside en el directorio particular de *user1*. Cambie el comando para que coincida con el nombre de archivo y la ubicación del archivo de copia de seguridad.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. Salir del modo de superusuario.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Restaurar la base de datos en Linux

Para restaurar la copia de seguridad de base de datos, puede usar el **RESTORE DATABASE** comando de Transact-SQL (TQL).

> [!NOTE]
> Los siguientes pasos se usa la **sqlcmd** herramienta. Si no lo ha hecho instalar herramientas de SQL Server, vea [herramientas de línea de comandos de instalación de SQL Server en Linux](sql-server-linux-setup-tools.md).

1. En el mismo terminal, inicie **sqlcmd**. En el siguiente ejemplo se conecta a la instancia de SQL Server local con la **SA** usuario. Escriba la contraseña cuando se le solicite, o especifique la contraseña mediante la adición de la **-P** parámetro.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. En el `>1` símbolo del sistema, escriba lo siguiente **RESTORE DATABASE** comando, al presionar ENTRAR después de cada línea (no puede copiar y pegar todo el comando de varias líneas a la vez). Reemplace todas las apariciones de `YourDB` por el nombre de la base de datos.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   Debe obtener un mensaje de que la base de datos se restauró correctamente.

1. Enumera todas las bases de datos en el servidor para comprobar la restauración. Debe aparecer en la base de datos restaurada.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. Ejecutar otras consultas en la base de datos migrada. El siguiente comando cambia el contexto para el **YourDB** la base de datos y selecciona las filas de una de sus tablas.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. Cuando haya terminado con **sqlcmd**, tipo `exit`.

1. Cuando haya terminado trabajando en el servidor remoto **ssh** sesión, escriba `exit` nuevo.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprendió a realizar la copia de seguridad de una base de datos en Windows y moverlo a un servidor de Linux que se ejecuta SQL Server 2017. También habrá aprendido cómo para:
> [!div class="checklist"]
> * Usar SSMS y Transact-SQL para crear un archivo de copia de seguridad en Windows
> * Instalar un shell de Bash en Windows
> * Use **scp** para mover archivos de copia de seguridad de Windows para Linux
> * Use **ssh** conectarse remotamente a la máquina de Linux
> * Reubicar el archivo de copia de seguridad para preparar la restauración
> * Use **sqlcmd** para ejecutar comandos de Transact-SQL
> * Restaurar la copia de seguridad de base de datos con la **RESTORE DATABASE** comando 

A continuación, explorar otros escenarios de migración de SQL Server en Linux. 

> [!div class="nextstepaction"]
>[Migrar bases de datos a SQL Server en Linux](sql-server-linux-migrate-overview.md)

