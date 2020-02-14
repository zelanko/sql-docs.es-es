---
title: Copias de seguridad de solo copia | Microsoft Docs
ms.custom: ''
ms.date: 01/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 1d95c1982d5809288b64f34cd1f6328b4ee00e4c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76941041"
---
# <a name="copy-only-backups"></a>Copias de seguridad de solo copia
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Una *copia de seguridad de solo copia* es una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independiente de la secuencia de copias de seguridad convencionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Normalmente, la realización de una copia de seguridad cambia la base de datos y afecta a la forma de restaurar las copias de seguridad posteriores. Sin embargo, a veces es útil realizar una copia de seguridad con un fin específico sin afectar a los procedimientos generales para copias de seguridad y restauración de la base de datos. Las copias de seguridad de solo copia sirven para este propósito.
  
 Los tipos de copias de seguridad de solo copia son los siguientes:  
  
- Copias de seguridad completas de solo copia (todos los modelos de recuperación)  
  
     Una copia de seguridad de solo copia no puede servir como base diferencial ni copia de seguridad diferencial y no afecta a la base diferencial.  
  
     El proceso de restauración de una copia de seguridad completa de solo copia es el mismo que la restauración de cualquier otra copia de seguridad completa.  
  
- Copias de seguridad de registros de solo copia (solo modelo de recuperación completa y modelo de recuperación optimizado para cargas masivas de registros)  

     Una copia de seguridad de registros de solo copia mantiene el punto de archivo del registro existente y, por tanto, no afecta a la secuenciación de copias de seguridad de registros periódicas. Las copias de seguridad de registros de solo copia suelen ser innecesarias. En lugar de ello, puede crear una nueva copia de seguridad de registros rutinaria (con WITH NORECOVERY) y utilizarla junto con las copias de seguridad de registros anteriores que sean necesarias para la secuencia de restauración. Sin embargo, una copia de seguridad de registros de solo copia en ocasiones puede resultar útil para realizar una restauración en línea. Para obtener un ejemplo, vea [Ejemplo: Restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md).  

     El registro de transacciones nunca se trunca después de una copia de seguridad de solo copia.  
  
 Las copias de seguridad de solo copia se registran en la columna **is_copy_only** de la tabla [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) .  
 
 > [!IMPORTANT]  
> En Instancia administrada de Azure SQL Database no se puede crear una copia de seguridad de solo copia de una base de datos cifrada con [Cifrado de datos transparente (TDE) administrado por el servicio](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql?tabs=azure-portal#service-managed-transparent-data-encryption). El TDE administrado por el servicio usa la clave interna para el cifrado de datos, y esa clave no se puede exportar, por lo que no se puede restaurar la copia de seguridad en ningún otro lugar. Considere la posibilidad de usar [TDE administrado por el cliente](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql) en su lugar para poder crear copias de seguridad de solo copia de bases de datos cifradas, pero asegúrese de que la clave de cifrado esté disponible para su posterior restauración.
  
## <a name="to-create-a-copy-only-backup"></a>Para crear una copia de seguridad de solo copia  
 Para crear una copia de seguridad de solo copia, utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell.  

### <a name="examples"></a>Ejemplos  
###  <a name="SSMSProcedure"></a> A. Uso de SQL Server Management Studio  
En este ejemplo, una copia de seguridad de solo copia de la base de datos `Sales` se realizará en el disco en la ubicación de copias de seguridad predeterminada.

1. En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.

1. Expanda **Bases de datos**, haga clic con el botón derecho en `Sales`, seleccione **Tareas**y, luego, haga clic en **Copia de seguridad...**

1. En la página **General** de la sección **Origen** active la casilla **Copia de seguridad de solo copia** .

1. Haga clic en **OK**.

###  <a name="TsqlProcedure"></a>B. Usar Transact-SQL  
Este ejemplo crea una copia de seguridad de solo copia para la base de datos `Sales` utilizando el parámetro COPY_ONLY.  También se realiza una copia de seguridad de solo copia del registro de transacciones.

```sql
BACKUP DATABASE Sales
TO DISK = 'E:\BAK\Sales_Copy.bak'
WITH COPY_ONLY;

BACKUP LOG Sales
TO DISK = 'E:\BAK\Sales_LogCopy.trn'
WITH COPY_ONLY;
```
  
> [!NOTE]  
> COPY_ONLY no tiene ningún efecto cuando se especifica con la opción DIFFERENTIAL.  

  
###  <a name="PowerShellProcedure"></a>C. Usar PowerShell  
Este ejemplo crea una copia de seguridad de solo copia para la base de datos `Sales` utilizando el parámetro -CopyOnly.  
```powershell
Backup-SqlDatabase -ServerInstance 'SalesServer' -Database 'Sales' -BackupFile 'E:\BAK\Sales_Copy.bak' -CopyOnly
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para crear una copia de seguridad completa o de registros**  
  
- [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
- [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  

 **Para ver copias de seguridad de solo copia**  
  
- [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
- [Proveedor de SQL Server PowerShell Provider](../../relational-databases/scripting/sql-server-powershell-provider.md)  

## <a name="see-also"></a>Consulte también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [Copiar bases de datos con Copias de seguridad y restauración](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[Backup-SqlDatabase](/powershell/module/sqlserver/backup-sqldatabase)

  
