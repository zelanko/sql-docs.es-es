---
title: "Pausa y reanudación de la migración de datos (Stretch Database) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, pausing and resuming
- pausing Stretch Database
- resuming Stretch Database
ms.assetid: 65d6a990-b295-41b2-97f9-7b6bf3000e4d
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 0fef9c7f912cb824b3f1fcf8653a82fa99a35561
ms.openlocfilehash: a291fd543d572fc621e7b59e968e7ca69d79552e
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="pause-and-resume-data-migration-stretch-database"></a>Pausa y reanudación de la migración de datos (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para pausar o reanudar la migración de datos en Azure, seleccione **Stretch** para una tabla en SQL Server Management Studio y después seleccione **Pausar** para pausar la migración de datos o **Reanudar** para reanudar la migración de datos. También puede usar Transact-SQL para pausar o reanudar la migración de datos.  
  
 Pause la migración de datos en tablas individuales para solucionar problemas en el servidor local o para maximizar el ancho de banda de red disponible.  

## <a name="pause-data-migration"></a>Pausa de la migración de datos  
  
### <a name="use-sql-server-management-studio-to-pause-data-migration"></a>Use SQL Server Management Studio para pausar la migración de datos  
  
1.  En el Explorador de objetos de SQL Server Management Studio, seleccione la tabla habilitada para Stretch para la que desea pausar la migración de datos.  
  
2.  Haga clic con el botón derecho y seleccione **Stretch**; después, seleccione **Pausar**.  
  
### <a name="use-transact-sql-to-pause-data-migration"></a>Use Transact-SQL para pausar la migración de datos  
 Ejecute el siguiente comando.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>  
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = PAUSED ) ) ;  
GO 
```  
  
## <a name="resume-data-migration"></a>Reanudación de la migración de datos  
  
### <a name="use-sql-server-management-studio-to-resume-data-migration"></a>Use SQL Server Management Studio para reanudar la migración de datos  
  
1.  En el Explorador de objetos de SQL Server Management Studio, seleccione la tabla habilitada para Stretch para la que desea reanudar la migración de datos.  
  
2.  Haga clic con el botón derecho y seleccione **Stretch**; después, seleccione **Reanudar**.  
  
### <a name="use-transact-sql-to-resume-data-migration"></a>Use Transact-SQL para reanudar la migración de datos  
 Ejecute el siguiente comando.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>   
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = OUTBOUND ) ) ;  
 GO
```  

## <a name="check-whether-migration-is-active-or-paused"></a>Comprobar si la migración está activa o en pausa

### <a name="use-sql-server-management-studio-to-check-whether-migration-is-active-or-paused"></a>Usar SQL Server Management Studio para comprobar si la migración está activa o en pausa
En SQL Server Management Studio, abra **Supervisión de base de datos de Stretch** y compruebe el valor de la columna **Estado de migración** . Para obtener más información, vea [Supervisión y solución de problemas de migración de datos](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).

### <a name="use-transact-sql-to-check-whether-migration-is-active-or-paused"></a>Usar Transact-SQL para comprobar si la migración está activa o en pausa
Consulte la vista de catálogo **sys.remote_data_archive_tables** y compruebe el valor de la columna **is_migration_paused** . Para obtener más información, vea [sys.remote_data_archive_tables](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md).

## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[Supervisión y solución de problemas de migración de datos](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 
  

