---
title: "Restauración de bases de datos habilitadas para Stretch (Stretch Database) | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2016
ms.prod: stretch-database
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cebc1f6d-d5ea-460d-ae60-d047d29c2723
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6f86b3d181ee105d3b7aaab7967ac9bada448b5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="restore-stretch-enabled-databases-stretch-database"></a>Restore Stretch-enabled databases (Restauración de bases de datos habilitadas para Stretch)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Restaure una copia de seguridad de una base de datos cuando sea necesario para recuperarse de muchos tipos de errores o desastres.
  
  Para obtener más información sobre la copia de seguridad, vea [Copia de seguridad y restauración de bases de datos habilitadas para Stretch](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md).

> [!TIP]
> La copia de seguridad es solo una parte de una completa solución de continuidad del negocio y alta disponibilidad. Para obtener más información sobre la alta disponibilidad, vea [Soluciones de alta disponibilidad](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).

## <a name="restore-your-sql-server-data"></a>Restaurar los datos de SQL Server
Para recuperarse de un error de hardware o de daños, restaure la base de datos de SQL Server con Stretch habilitado a partir de una copia de seguridad. Puede seguir recurriendo a los métodos de restauración de SQL Server que usa actualmente. Para obtener más información, vea [Información general sobre restauración y recuperación](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).

Después de restaurar la base de datos de SQL Server, hay que ejecutar el procedimiento almacenado **sys.sp_rda_reauthorize_db** para volver a establecer la conexión entre la base de datos de SQL Server con Stretch habilitado y la base de datos de Azure remota. Para obtener más información, vea [Restaurar la conexión entre la base de datos de SQL Server y la base de datos de Azure remota](#reconnect).

## <a name="restore-your-remote-azure-data"></a>Restaurar los datos de Azure remotos

### <a name="recover-a-live-azure-database"></a>Recuperar una base de datos de Azure dinámica
El servicio SQL Server Stretch Database de Azure crea instantáneas de todos los datos dinámicos al menos cada 8 horas, para lo cual usa instantáneas de Almacenamiento de Azure. Estas instantáneas se conservan durante 7 días. Esto permite restaurar los datos a uno de al menos cualquiera de los 21 puntos en el tiempo en los últimos 7 días, hasta el momento en el que se tomó la última instantánea.

Haga lo siguiente para restaurar una base de datos de Azure dinámica a un momento anterior en el tiempo por medio del Portal de Azure.

1. Inicie sesión en el [Portal de Azure][].
2. En el lado izquierdo de la pantalla, seleccione **EXAMINAR** y, después, seleccione **Bases de datos SQL**.
3. Vaya a la base de datos y selecciónela.
4. En la parte superior de la hoja de la base de datos, haga clic en **Restaurar**.
5. Indique un **Nombre de la base de datos**nuevo, seleccione un **Punto de restauración** y, después, haga clic en **Crear**.
6. Se iniciará el proceso de restauración de la base de datos, que puede supervisar con **NOTIFICACIONES**.

### <a name="recover-a-deleted-azure-database"></a>Recuperar una base de datos de Azure eliminada
El servicio SQL Server Stretch Database de Azure toma una instantánea de base de datos antes de que esta se elimine y la conserva durante 7 días. Transcurrido ese tiempo, dejará de conservar las instantáneas de base de datos dinámica. Esto le permite restaurar una base de datos al momento en el que se eliminó.

Haga lo siguiente para restaurar una base de datos de Azure eliminada al momento en que se eliminó por medio del Portal de Azure.

1. Inicie sesión en el [Portal de Azure][].
2. En el lado izquierdo de la pantalla, seleccione **EXAMINAR** y, después, seleccione **Servidores SQL**.
3. Vaya al servidor y selecciónelo.
4. Desplácese hacia abajo hasta Operaciones en la hoja del servidor y haga clic en el icono **Bases de datos eliminadas** .
5. Seleccione la base de datos eliminada que quiera restaurar.
5. Indique un **Nombre de la base de datos** nuevo y haga clic en **Crear**.
6. Se iniciará el proceso de restauración de la base de datos, que puede supervisar con **NOTIFICACIONES**.

## <a name="reconnect"></a>Restaurar la conexión entre la base de datos de SQL Server y la base de datos de Azure remota

1.  Si se va a conectar a una base de datos de Azure restaurada con un nombre diferente o en una región distinta, ejecute el procedimiento almacenado [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) para desconectarse de la base de datos de Azure anterior.  
  
2.  Ejecute el procedimiento almacenado [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectar la base de datos local con Stretch habilitado a la base de datos de Azure.  
  
    -   Escriba las credenciales de ámbito de base de datos existentes como un valor sysname o varchar (128). No use varchar(max). Puede buscar el nombre de la credencial en la vista **sys.database_scoped_credentials**.  
  
    -   Especifique si quiere hacer una copia de los datos remotos y conectarse a la copia (recomendado).  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    EXEC sp_rda_reauthorize_db
        @credential = N'<existing_database_scoped_credential_name>',
        @with_copy = 1 ;  
    GO  
    ```  
    
  ## <a name="see-also"></a>Vea también  
 [Copia de seguridad y restauración de bases de datos habilitadas para Stretch](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
 [Administrar y solucionar problemas de Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
 
 [Portal de Azure]: https://portal.azure.com/
 
