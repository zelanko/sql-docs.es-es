---
title: Migrar una base de datos de SQL Server de Windows a Linux | Documentos de Microsoft
description: "En este tema se muestra cómo realizar la copia de seguridad de una base de datos de SQL Server en Windows y restaurarlo a una máquina de Linux que se ejecuta SQL Server 2017 RC2."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 2e23ba46381b1fb80b8ac335f6d7630f02a222bb
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migrar una base de datos de SQL Server de Windows para Linux con backup y restore

Copia de seguridad de SQL Server y la característica de restauración es la manera recomendada para migrar una base de datos de SQL Server en Windows a SQL Server de 2017 RC2 en Linux. Este tema proporciona instrucciones paso a paso para esta técnica. En este tutorial, aprenderá a:

- Descargue el archivo de copia de seguridad de AdventureWorks en un equipo de Windows
- Transferir la copia de seguridad en el equipo Linux
- Restaurar la base de datos mediante comandos de Transact-SQL

> [!NOTE] 
> Este tutorial se supone que ha instalado [SQL Server 2017 RC2](sql-server-linux-setup.md) y [herramientas de SQL Server](sql-server-linux-setup-tools.md) en el servidor Linux de destino.

## <a name="download-the-adventureworks-database-backup"></a>Descargue la copia de seguridad de base de datos de AdventureWorks

Aunque puede usar los mismos pasos para restaurar cualquier base de datos, la base de datos de ejemplo de AdventureWorks proporciona un buen ejemplo. Se trata como un archivo de copia de seguridad de base de datos existente.

>[!NOTE] 
> Para restaurar una base de datos a SQL Server en Linux, debe realizarse la copia de seguridad de origen de SQL Server 2014 o SQL Server 2016. El número de compilación de SQL Server de la copia de seguridad no debe ser mayor que la restauración de número de compilación de SQL Server.  

1. En el equipo de Windows, vaya a [https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661) y descargue el **Adventure Works 2014 Full Database Backup.zip**.

   > [!TIP] 
   > Aunque este tutorial muestra la copia de seguridad y restauración entre Windows y Linux, también puede usar un explorador en Linux para descargar directamente en el ejemplo de AdventureWorks en su equipo Linux.

2. Abra el archivo zip y extraiga el archivo AdventureWorks2014.bak a una carpeta en su equipo.

## <a name="transfer-the-backup-file-to-linux"></a>Transfiera el archivo de copia de seguridad para Linux

Para restaurar la base de datos, primero debe transferir el archivo de copia de seguridad de la máquina de Windows en el equipo de Linux de destino.

1. Para Windows, instale un shell de Bash. Hay varias opciones, incluidas las siguientes:

   - Descargar un shell de Bash, de código abierto como [PuTTY](http://www.putty.org/).
   - O bien, en Windows 10, use la nueva [shell de Bash integrado (beta)](https://msdn.microsoft.com/en-us/commandline/wsl/about).
   - O bien, si trabaja con Git, use la [shell de Git Bash](https://git-scm.com/downloads).

2. Abra un shell de Bash (terminal) y navegue hasta el directorio que contiene **AdventureWorks2014.bak**.

3. Use la **scp** comando (copia seguro) para transferir el archivo en el equipo de Linux de destino. Las transferencias de ejemplo siguiente **AdventureWorks2014.bak** al directorio particular de *user1* en el servidor denominado *linuxserver1*.

   ```bash
   sudo scp AdventureWorks2014.bak user1@linuxserver1:./
   ```
   
   En el ejemplo anterior, podría proporcionar en su lugar la dirección IP en lugar del nombre de servidor.

Hay varias alternativas al uso del scp. Una consiste en usar [Samba](https://help.ubuntu.com/community/Samba) para configurar un recurso compartido de red SMB entre Windows y Linux. Para ver un tutorial en Ubuntu, consulte [cómo crear un recurso compartido de red a través de Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Una vez establecida, puede tener acceso a él como un archivo de red comparten en Windows, como  **\\ \\machinenameorip\\compartir**.

## <a name="move-the-backup-file"></a>Mueva el archivo de copia de seguridad

En este punto, el archivo de copia de seguridad está en el servidor Linux. Antes de restaurar la base de datos a SQL Server, debe colocar la copia de seguridad en un subdirectorio de **/var/opt/mssql**.

1. Abra un Terminal en el equipo de Linux de destino que contiene la copia de seguridad.

2. ENTRAR en el modo de superusuario.

   ```bash
   sudo su
   ```

3. Crear un nuevo directorio de copia de seguridad. El parámetro -p no hace nada si el directorio ya existe.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

4. Mueva el archivo de copia de seguridad a ese directorio. En el ejemplo siguiente, el archivo de copia de seguridad reside en el directorio particular de *user1*. Cambiar el comando para que coincida con la ubicación de **AdventureWorks2014.bak** en su equipo.

   ```bash
   mv /home/user1/AdventureWorks2014.bak /var/opt/mssql/backup/
   ```

5. Salir del modo de superusuario.

   ```bash
   exit
   ```

## <a name="restore-the-database-backup"></a>Restaurar la copia de seguridad de base de datos

Para restaurar la copia de seguridad, puede usar el comando de Transact-SQL de restauración de base de datos (TQL).

> [!NOTE] 
> Los pasos siguientes utilizan la herramienta sqlcmd. Si no lo ha hecho instalar herramientas de SQL Server, vea [instalar SQL Server en Linux](sql-server-linux-setup.md).

1. En el mismo terminal, inicie **sqlcmd**. En el siguiente ejemplo se conecta a la instancia de SQL Server local con la *SA* usuario. Escriba la contraseña cuando se le solicite o especifique la contraseña con el parámetro -P.

   ```bash
   sqlcmd -S localhost -U SA
   ```

2. Después de conectarse, escriba lo siguiente **Restaurar base de datos** comando, al presionar ENTRAR después de cada línea. El ejemplo siguiente restaura la **AdventureWorks2014.bak** de archivos desde el */var/opt/mssql/backup* directory.

   ```sql
   RESTORE DATABASE AdventureWorks
   FROM DISK = '/var/opt/mssql/backup/AdventureWorks2014.bak'
   WITH MOVE 'AdventureWorks2014_Data' TO '/var/opt/mssql/data/AdventureWorks2014_Data.mdf',
   MOVE 'AdventureWorks2014_Log' TO '/var/opt/mssql/data/AdventureWorks2014_Log.ldf'
   GO
   ```

   Debe obtener un mensaje de que la base de datos se restauró correctamente.

3. Comprobar la restauración, primero cambiar el contexto a la base de datos de AdventureWorks. 

   ```sql
   USE AdventureWorks
   GO
   ```

4. Ejecute la consulta siguiente que muestra los 10 productos en la **Production.Products** tabla.

   ```sql
   SELECT TOP 10 Name, ProductNumber FROM Production.Product ORDER BY Name
   GO
   ```

![Resultado de consulta Production.Products](./media/sql-server-linux-migrate-restore-database/sql-server-linux-adventureworks-query.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otras técnicas de migración y base de datos, vea [migrar bases de datos a SQL Server en Linux](sql-server-linux-migrate-overview.md). 

