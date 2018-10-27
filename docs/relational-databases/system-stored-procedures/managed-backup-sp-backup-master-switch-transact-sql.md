---
title: managed_backup.sp_backup_master_switch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_ backup_master_switch
- smart_admin.sp_backup_master_switch
- sp_ backup_master_switch_TSQL
- smart_admin.sp_backup_master_switch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_ backup_master_switch
- smart_admin.sp_backup_master_switch
ms.assetid: 1ed2b2b2-c897-41cc-bed5-1c6bc47b9dd2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a575a83d0e41dfb39dae33040d367188c4ce2200
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099676"
---
# <a name="managedbackupspbackupmasterswitch-transact-sql"></a>managed_backup.sp_backup_master_switch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Pausa o reanuda la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Utilice este procedimiento almacenado para pausar temporalmente la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] y reanudarla después. Esto garantiza que toda la configuración permanece y se conserva cuando las operaciones se reanudan. Cuando se pausa la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], el período de retención no se aplica. Esto significa que no hay ninguna comprobación para determinar si los archivos deben eliminarse del almacenamiento o si hay archivos de copia de seguridad dañados o se ha interrumpido la cadena de registros.  
  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
EXEC managed_backup.sp_backup_master_switch   
                     [@new_state = ] { 0 | 1}  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @state  
 Establezca el estado de la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. El @state parámetro es **bits**. Cuando se establece en el valor 0, las operaciones se pausan y, cuando se establece en el valor 1, la operación se reanuda.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
 Describe problemas de seguridad relacionados con la instrucción. Permisos de inclusión como subsección (título H3). Considere incluir otras subsecciones para el encadenamiento de la propiedad y auditoría, si procede.  
  
### <a name="permissions"></a>Permisos  
 Requiere la pertenencia a **db_backupoperator** rol, la base de datos con **ALTER ANY CREDENTIAL** permisos, y **EXECUTE** permisos **sp_delete_ backuphistory**procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente se puede utilizar para pausar la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en la instancia que se ejecuta en:  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
 El ejemplo siguiente se puede utilizar para reanudar la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=1;  
Go  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
