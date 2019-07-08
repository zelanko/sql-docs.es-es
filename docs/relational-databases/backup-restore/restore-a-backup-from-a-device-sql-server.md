---
title: Restaurar una copia de seguridad desde un dispositivo (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], device restores
- backup devices [SQL Server], restoring from
- database restores [SQL Server], device restores
- devices [SQL Server]
ms.assetid: 6e139de7-7de2-4d18-9df0-beac31ba7ff1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b1582c10c8ae3aadf836fae2764988053f90e72b
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580398"
---
# <a name="restore-a-backup-from-a-device-sql-server"></a>Restaurar una copia de seguridad desde un dispositivo (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo restaurar una copia de seguridad desde un dispositivo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  Para obtener información sobre la copia de seguridad de SQL Server en el servicio de almacenamiento de blobs de Windows Azure, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para restaurar una copia de seguridad desde un dispositivo, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Si la base de datos que se va a restaurar no existe, el usuario debe tener permisos CREATE DATABASE para poder ejecutar RESTORE. Si la base de datos existe, los permisos RESTORE corresponden de forma predeterminada a los miembros de los roles fijos de servidor **sysadmin** y **dbcreator** , y al propietario (**dbo**) de la base de datos (para la opción FROM DATABASE_SNAPSHOT, la base de datos siempre existe).  
  
 Los permisos RESTORE se conceden a los roles en los que la información acerca de la pertenencia está siempre disponible para el servidor. Debido a que la pertenencia a un rol fijo de base de datos solo se puede comprobar cuando la base de datos es accesible y no está dañada, lo que no siempre ocurre cuando se ejecuta RESTORE, los miembros del rol fijo de base de datos **db_owner** no tienen permisos RESTORE.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-restore-a-backup-from-a-device"></a>Para restaurar una copia de seguridad desde un dispositivo  
  
1.  Tras conectarse a la instancia apropiada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol correspondiente.  
  
2.  Expanda **Bases de datos**y, en función de la base de datos, seleccione la base de datos de un usuario o expanda **Bases de datos del sistema** y seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, después, haga clic en **Restaurar**.  
  
4.  Haga clic en el tipo de operación de restauración que quiera (**Base de datos**, **Archivos y grupos de archivos**o **Registro de transacciones**). De este modo se abre el cuadro de diálogo de restauración correspondiente.  
  
5.  En la página **General** , en la sección **Origen de restauración** , haga clic en **Desde dispositivo**.  
  
6.  Haga clic en el botón Examinar del cuadro de texto **Desde dispositivo** , que abre el cuadro de diálogo **Especificar copia de seguridad** .  
  
7.  En el cuadro de texto **Medio para copia de seguridad** , seleccione **Dispositivo de copia de seguridad**y haga clic en el botón **Agregar** para abrir el cuadro de diálogo **Seleccionar dispositivo de copia de seguridad** .  
  
8.  En el cuadro de texto **Dispositivo de copia de seguridad** , seleccione el dispositivo que desee usar para la operación de restauración.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-restore-a-backup-from-a-device"></a>Para restaurar una copia de seguridad desde un dispositivo  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  En la instrucción [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) , especifique el dispositivo de copia de seguridad físico o lógico que se va a utilizar para la operación de copia de seguridad. En este ejemplo se realiza una restauración desde un archivo de disco con el nombre físico `Z:\SQLServerBackups\AdventureWorks2012.bak`.  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' ;  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [Restaurar una copia de seguridad de base de datos en el modelo de recuperación simple &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)   
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Restaurar una copia de seguridad diferencial de la base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)   
 [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
  
