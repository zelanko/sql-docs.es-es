---
title: Copia de seguridad y restauración de bases de datos SQL en Linux
description: Obtenga información sobre cómo las copias de seguridad y restaurar bases de datos de SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: f3e27b283156bb23754a93161fc796e15baec7ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077692"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Copia de seguridad y restauración de bases de datos SQL en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Puede realizar copias de seguridad de bases de datos de SQL Server 2017 en Linux con las mismas herramientas que otras plataformas. En un servidor Linux, puede usar **sqlcmd** para conectarse a SQL Server y realizar copias de seguridad. Desde Windows, puede conectarse a SQL Server en Linux y realizar copias de seguridad con la interfaz de usuario. La funcionalidad de copia de seguridad es el mismo entre plataformas. Por ejemplo, puede hacer una copia las bases de datos localmente, en unidades remotas o a [servicio Microsoft Azure Blob storage](../relational-databases/backup-restore/sql-server-backup-to-url.md).

## <a name="backup-a-database"></a>Copia de seguridad de una base de datos

En el ejemplo siguiente **sqlcmd** se conecta a la instancia de SQL Server local y toma una completa de copia de seguridad de una base de datos de usuario denominada `demodb`.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

Al ejecutar el comando, SQL Server le solicitará una contraseña. Después de escribir la contraseña, el shell devolverá los resultados del progreso de copia de seguridad. Por ejemplo:

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>Copia de seguridad del registro de transacciones

Si la base de datos está en el modelo de recuperación completa, también puede hacer copias de seguridad de registro de transacciones para las opciones de restauración más granulares. En el ejemplo siguiente, **sqlcmd** se conecta a la instancia de SQL Server local y toma un registro de transacciones en copia de seguridad.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>Restaurar una base de datos

En el ejemplo siguiente **sqlcmd** se conecta a la instancia local de SQL Server y restaura la base de datos demodb. Tenga en cuenta que el `NORECOVERY` opción se utiliza para permitir las restauraciones de copias de seguridad de archivos de registro adicionales. Si no va a restaurar los archivos de registro adicionales, quite el `NORECOVERY` opción.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> Si accidentalmente usa NORECOVERY pero no tiene copias de seguridad de archivos de registro adicionales, ejecute el comando `RESTORE DATABASE demodb` sin parámetros adicionales. Esto finaliza la restauración y deja la base de datos operativa.

### <a name="restore-the-transaction-log"></a>Restaurar el registro de transacciones

El siguiente comando restaura la copia de seguridad de registro de transacciones anteriores.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Copia de seguridad y restauración con SQL Server Management Studio (SSMS)

Puede usar SSMS desde un equipo de Windows para conectarse a una base de datos de Linux y realizar una copia de seguridad a través de la interfaz de usuario.

>[!NOTE] 
> Use la versión más reciente de SSMS para conectarse a SQL Server. Para descargar e instalar la versión más reciente, consulte [descargar SSMS](../ssms/download-sql-server-management-studio-ssms.md). Para obtener más información sobre cómo usar SSMS, consulte [usar SSMS para administrar SQL Server en Linux](sql-server-linux-manage-ssms.md).

Los siguientes pasos guiarán a través de una copia de seguridad con SSMS. 

1. Inicie SSMS y conéctese a su servidor en SQL Server 2017 en Linux.

1. En el Explorador de objetos, haga doble clic en la base de datos, haga clic en **tareas**y, a continuación, haga clic en **copia de seguridad...** .

1. En el **copia de seguridad de base de datos** cuadro de diálogo, compruebe los parámetros y las opciones y haga clic en **Aceptar**.
 
SQL Server se completa la copia de seguridad de base de datos.

### <a name="restore-with-sql-server-management-studio-ssms"></a>Restaurar con SQL Server Management Studio (SSMS) 

Los siguientes pasos le guiarán a través de restaurar una base de datos con SSMS.

1. En SSMS, haga clic en **bases de datos** y haga clic en **restaurar bases de datos...** . 

1. En **origen** haga clic en **dispositivo:** y, a continuación, haga clic en el botón de puntos suspensivos (...).

1. Busque el archivo de copia de seguridad de base de datos y haga clic en **Aceptar**. 

1. En **plan de restauraciones**, compruebe el archivo de copia de seguridad y la configuración. Haga clic en **Aceptar**. 

1. SQL Server restaura la base de datos. 

## <a name="see-also"></a>Vea también

* [Crear una copia de seguridad completa de la base de datos (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [Realizar una copia de seguridad de un registro de transacciones (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [Copia de seguridad en URL de SQL Server](../relational-databases/backup-restore/sql-server-backup-to-url.md)
