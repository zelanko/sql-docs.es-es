---
title: "Administrar y solucionar problemas de Stretch Database | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch Database, administrar"
  - "Stretch Database, solucionar problemas"
  - "administrar Stretch Database"
  - "solucionar problemas de Stretch Database"
ms.assetid: 6334db3e-9297-44df-8d53-211187a95520
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Administrar y solucionar problemas de Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para administrar y solucionar problemas de Stretch Database, use las herramientas y los métodos que se describen en este tema.  
## Administrar los datos locales  
  
###  <a name="LocalInfo"></a> Obtener información sobre las bases de datos y tablas locales habilitadas para Stretch Database  
 Abra las vistas de catálogo **sys.databases** y **sys.tables** para ver información sobre las bases de datos y las tablas de SQL Server habilitadas para Stretch. Para obtener más información, vea [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) y [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md).  
 
 Para ver el espacio que emplea una tabla habilitada para Stretch en SQL Server, ejecute la siguiente instrucción.
 
 ```tsql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'LOCAL_ONLY';
GO
 ```
   
## Administrar la migración de datos  
  
### Comprobar la función de filtro aplicada a una tabla  
 Abra la vista de catálogo **sys.remote_data_archive_tables** y compruebe el valor de la columna **filter_predicate** para identificar la función que usa Stretch Database para seleccionar las filas que se van a migrar. Si el valor es nulo, toda la tabla será apta para la migración. Para obtener más información, vea [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../Topic/sys.remote_data_archive_tables%20\(Transact-SQL\).md) y [Select rows to migrate by using a filter function](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md) (Seleccionar las filas que se van a migrar mediante una función de filtro).  
  
###  <a name="Migration"></a> Comprobar el estado de la migración de datos  
 Seleccione **Tareas | Stretch | Monitor** en una base de datos de SQL Server Management Studio para supervisar la migración de datos en el monitor de Stretch Database. Para obtener más información, vea [Supervisión y solución de problemas de migración de datos &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
 También puede abrir la vista de administración dinámica **sys.dm_db_rda_migration_status** para ver el número de lotes y filas de datos que se han migrado.  
  
###  <a name="Firewall"></a> Solución de problemas de migración de datos  
 Para obtener sugerencias de solución de problemas, vea [Supervisión y solución de problemas de migración de datos &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
## Administrar los datos remotos  
  
###  <a name="RemoteInfo"></a> Obtener información sobre las bases de datos y tablas remotas que usa Stretch Database  
 Abra las vistas de catálogo **sys.remote_data_archive_databases** y **sys.remote_data_archive_tables** para ver la información de las bases de datos y las tablas remotas en las que se almacenan los datos migrados. Para obtener más información, vea [sys.remote_data_archive_databases &#40;Transact-SQL&#41;](../Topic/sys.remote_data_archive_databases%20\(Transact-SQL\).md) y [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../Topic/sys.remote_data_archive_tables%20\(Transact-SQL\).md).  
 
Para ver el espacio que emplea una tabla habilitada para Stretch en Azure, ejecute la siguiente instrucción.
 
 ```tsql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'REMOTE_ONLY';
GO
 ```

### Eliminar los datos migrados  
Si quiere eliminar los datos que ya se han migrado a Azure, siga los pasos descritos en [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md).  
  
## Administrar el esquema de tabla

### No cambie el esquema de la tabla remota  
 No cambie el esquema de una tabla remota de Azure que esté asociada a una tabla de SQL Server configurada para Stretch Database. En concreto, no modifique el nombre o el tipo de datos de una columna. La característica Stretch Database da por supuestas varias cosas sobre el esquema de la tabla remota en relación con el esquema de la tabla de SQL Server. Si cambia el esquema remoto, Stretch Database deja de funcionar para la tabla modificada.  

### Conciliar las columnas de tabla  
Si ha eliminado por error las columnas de la tabla remota, ejecute **sp_rda_reconcile_columns** para agregar columnas a la tabla remota que hay en la tabla de SQL Server habilitada para Stretch, pero no en la tabla remota. Para obtener más información, vea [sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md).  
  
  > [!IMPORTANT] Cuando **sp_rda_reconcile_columns** vuelve a crear las columnas que eliminó por error de la tabla remota, no restaura los datos que había antes en las columnas eliminadas.
  
**sp_rda_reconcile_columns** no elimina las columnas de la tabla remota que hay en la tabla remota, pero no en la tabla de SQL Server habilitada para Stretch. Si hay columnas en la tabla remota de Azure que ya no existen en la tabla de SQL Server habilitada para Stretch, estas columnas adicionales no impiden que Stretch Database funcione con normalidad. También puede quitar estas columnas adicionales de forma manual.  
 
## Administrar el rendimiento y los costos  
  
### Solucionar problemas del rendimiento de las consultas  
  Se espera que las consultas que incluyen tablas habilitadas para Stretch se realicen más lentamente que antes de que las tablas se habilitaran para Stretch. Si el rendimiento de las consultas se degrada considerablemente, compruebe si se debe a alguno de estos posibles problemas.  
  
-   ¿Se encuentra el servidor de Azure en una región geográfica diferente de la de SQL Server? Configure el servidor de Azure para que se encuentre en la misma región geográfica que SQL Server para reducir la latencia de red.  
  
-   Las condiciones de red podrían haberse degradado. Póngase en contacto con el administrador de red para obtener información sobre los problemas o las interrupciones recientes.  
  
### Aumentar el nivel de rendimiento de Azure para operaciones con uso intensivo de recursos, como la indexación  
 Al compilar, recompilar o reorganizar el índice de una tabla grande configurada para Stretch Database y se prevean numerosas consultas de los datos migrados en Azure durante este tiempo, considere la posibilidad de aumentar el nivel de rendimiento de la correspondiente base de datos remota de Azure mientras dure la operación. Para obtener más información sobre los niveles de rendimiento y los precios, vea [Precios de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### No se puede pausar el servicio de SQL Server Stretch Database en Azure  
 Asegúrese de seleccionar el nivel de rendimiento y el precio adecuados. Si aumenta temporalmente el nivel de rendimiento de una operación que consume muchos recursos, restáurelo al nivel anterior una vez finalizada la operación. Para obtener más información sobre los niveles de rendimiento y los precios, vea [Precios de SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
   
 ## Cambiar el ámbito de las consultas  
 De forma predeterminada, las consultas efectuadas en tablas habilitadas para Stretch devuelven datos locales y remotos. Puede cambiar el ámbito de todas las consultas efectuadas por todos los usuarios o de una sola consulta efectuada por un administrador.  
   
 ### Cambiar el ámbito de todas las consultas efectuadas por todos los usuarios  
 Para cambiar el ámbito de todas las consultas efectuadas por todos los usuarios, ejecute el procedimiento almacenado **sys.sp_rda_set_query_mode**. Puede reducir el ámbito para consultar únicamente los datos locales, deshabilitar todas las consultas o restaurar la configuración predeterminada. Para obtener más información, vea [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md).  
   
 ### <a name="queryHints"></a>Cambiar el ámbito de una sola consulta efectuada por un administrador  
 Para cambiar el ámbito de una sola consulta efectuada por un miembro del rol db_owner, agregue la sugerencia de consulta **WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = *valor*)** a la instrucción SELECT. La sugerencia de consulta REMOTE_DATA_ARCHIVE_OVERRIDE puede tener los siguientes valores:  
 -   **LOCAL_ONLY**. Solo se consultan los datos locales.  
   
 -   **REMOTE_ONLY**. Solo se consultan los datos remotos.  
   
 -   **STAGE_ONLY**. Solo se consultan los datos de la tabla en los que Stretch Database almacena provisionalmente las filas aptas para la migración y retiene las filas migradas durante el período especificado después de la migración. Esta sugerencia de consulta es la única manera de consultar la tabla de almacenamiento provisional.  
  
Por ejemplo, la siguiente consulta solo devuelve los resultados locales.  
  
 ```tsql  
USE <Stretch-enabled database name>;
GO
SELECT * FROM <Stretch_enabled table name> WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = LOCAL_ONLY) WHERE ... ;
GO
```  
   
 ## <a name="adminHints"></a>Efectuar actualizaciones y eliminaciones administrativas  
 De forma predeterminada, no se pueden actualizar o eliminar de una tabla habilitada para Stretch filas que son aptas para la migración ni filas que ya se han migrado. Cuando tiene que solucionar un problema, un miembro del rol db_owner puede ejecutar una operación UPDATE o DELETE agregando la sugerencia de consulta **WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = *valor*)** a la instrucción. La sugerencia de consulta REMOTE_DATA_ARCHIVE_OVERRIDE puede tener los siguientes valores:  
 -   **LOCAL_ONLY**. Solo se actualizan o eliminan los datos locales.  
   
 -   **REMOTE_ONLY**. Solo se actualizan o eliminan los datos remotos.  
   
 -   **STAGE_ONLY**. Solo se actualizan o eliminan los datos de la tabla en los que Stretch Database almacena provisionalmente las filas aptas para la migración y retiene las filas migradas durante el período especificado después de la migración.  
  
## Vea también  
 [Supervisión y solución de problemas de migración de datos &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)   
[Copia de seguridad de bases de datos habilitadas para Stretch (Stretch Database)](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
[Restore Stretch-enabled databases (Stretch Database) (Restauración de bases de datos habilitadas para Stretch (Stretch Database))](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
  