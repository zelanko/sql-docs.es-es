---
title: Copia de seguridad y restaurar bases de datos de SQL Server en Linux | Documentos de Microsoft
description: Aprenda a copias de seguridad y restaurar bases de datos de SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 6bd05a89f0c06bc03de931b898be18f3cbea0c8c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Copia de seguridad y restauración de bases de datos SQL en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Puede realizar copias de seguridad de bases de datos de SQL Server de 2017 RC2 en Linux con las mismas herramientas como otras plataformas. En un servidor Linux, puede usar `sqlcmd` para conectarse a SQL Server y realizar copias de seguridad. En Windows, puede conectarse a SQL Server en Linux y realizar copias de seguridad con la interfaz de usuario. La funcionalidad de copia de seguridad es el mismo en las distintas plataformas. Por ejemplo, puede hacer una copia las bases de datos localmente, en unidades remotas o a [servicio de almacenamiento de blobs de Microsoft Azure](http://msdn.microsoft.com/library/dn435916.aspx). 

## <a name="backup-with-sqlcmd"></a>Copia de seguridad con sqlcmd

En el ejemplo siguiente `sqlcmd` se conecta a la instancia de SQL Server local y toma una completa de copia de seguridad de una base de datos de usuario denominada `demodb`.

```bash
sqlcmd -H localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
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

### <a name="backup-log-with-sqlcmd"></a>Registro de copia de seguridad con sqlcmd

En el ejemplo siguiente, `sqlcmd` se conecta a la instancia de SQL Server local y realiza copia de seguridad final del registro. Una vez completada la copia de seguridad del final del registro, la base de datos estará en estado de restauración. 

```bash
sqlcmd -H localhost -U SA -Q "BACKUP LOG [demodb] TO  DISK = N'var/opt/mssql/data/demodb_LogBackup_2016-11-14_18-09-53.bak' WITH NOFORMAT, NOINIT,  NAME = N'demodb_LogBackup_2016-11-14_18-09-53', NOSKIP, NOREWIND, NOUNLOAD,  NORECOVERY ,  STATS = 5"
```


## <a name="restore-with-sqlcmd"></a>Restaurar con sqlcmd

En el siguiente ejemplo `sqlcmd` se conecta a la instancia local de SQL Server y se restaura una base de datos.

```bash
sqlcmd -H localhost -U SA -Q "RESTORE DATABASE [demodb] FROM  DISK = N'var/opt/mssql/data/demodb.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE,  STATS = 5"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Copia de seguridad y restauración con SQL Server Management Studio (SSMS)

Puede usar SSMS desde un equipo de Windows para conectarse a una base de datos de Linux y realizar una copia de seguridad a través de la interfaz de usuario. 

>[!NOTE] 
> Utilice la versión más reciente de SSMS para conectarse a SQL Server. Para descargar e instalar la versión más reciente, consulte [descargar SSMS](http://msdn.microsoft.com/library/mt238290.aspx). 

Los pasos siguientes guían a través de una copia de seguridad con SSMS. 

1. Inicie SSMS y conéctese a su servidor en SQL Server de 2017 RC2 en Linux.

1. En el Explorador de objetos, haga doble clic en la base de datos, haga clic en **tareas**y, a continuación, haga clic en **realizar copias de seguridad...** .

1. En el **copia de seguridad de la base de datos** cuadro de diálogo, compruebe los parámetros y las opciones y haga clic en **Aceptar**.
 
SQL Server se completa la copia de seguridad de base de datos.

Para obtener más información, consulte [utilice SSMS para administrar SQL Server en Linux](sql-server-linux-manage-ssms.md).

### <a name="restore-with-sql-server-management-studio-ssms"></a>Restaurar con SQL Server Management Studio (SSMS) 

Los siguientes pasos le guiarán a través de restaurar una base de datos con SSMS.

1. En SSMS, haga clic en **bases de datos** y haga clic en **restaurar bases de datos...** . 

1. En **origen** haga clic en **dispositivo:** y, a continuación, haga clic en el botón de puntos suspensivos (...).

1. Busque el archivo de copia de seguridad de base de datos y haga clic en **Aceptar**. 

1. En **plan de restauraciones**, compruebe el archivo de copia de seguridad y la configuración. Haga clic en **Aceptar**. 

1. SQL Server restaura la base de datos. 

## <a name="see-also"></a>Vea también

* [Crear una copia de seguridad completa de la base de datos (SQL Server)](http://msdn.microsoft.com/library/ms187510.aspx)
* [Hacer copia de seguridad del registro de transacciones (SQL Server)](http://msdn.microsoft.com/library/ms179478.aspx)
* [BACKUP (Transact-SQL)](http://msdn.microsoft.com/library/ms186865.aspx)
* [Copia de seguridad en URL de SQL Server](http://msdn.microsoft.com/library/dn435916.aspx)

