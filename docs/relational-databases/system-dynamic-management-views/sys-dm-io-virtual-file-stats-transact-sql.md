---
title: Sys.dm_io_virtual_file_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_io_virtual_file_stats
- sys.dm_io_virtual_file_stats_TSQL
- sys.dm_io_virtual_file_stats
- dm_io_virtual_file_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_virtual_file_stats dynamic management function
ms.assetid: fa3e321f-6fe5-45ff-b397-02a0dd3d6b7d
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 971eeff843b43464541224343a937300bd22f280
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmiovirtualfilestats-transact-sql"></a>sys.dm_io_virtual_file_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Devuelve las estadísticas de E/S de los archivos de registro y datos. Esta vista de administración dinámica reemplaza el [fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md) función.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], use el nombre **sys.dm_pdw_nodes_io_virtual_file_stats**. 

## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database

sys.dm_io_virtual_file_stats (   
    { database_id | NULL },  
    { file_id | NULL }  
)  
```  

```  
-- Syntax for Azure SQL Data Warehouse

sys.dm_pdw_nodes_io_virtual_file_stats
```
  
## <a name="arguments"></a>Argumentos  


 *database_id* | ES NULL

 **SE APLICA A:** SQL Server (a partir de 2008), Azure SQL Database

 Identificador de la base de datos. *database_id* es de tipo int, no tiene ningún valor predeterminado. Las entradas válidas son el número de identificación de una base de datos o NULL. Cuando se especifica NULL, se devuelven todas las bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La función integrada [DB_ID](../../t-sql/functions/db-id-transact-sql.md) puede especificarse.  
  
*file_ID* | ES NULL

**SE APLICA A:** SQL Server (a partir de 2008), Azure SQL Database
 
Id. del archivo. *file_ID* es de tipo int, no tiene ningún valor predeterminado. Las entradas válidas son el número de identificación de un archivo o NULL. Cuando se especifica NULL, se devuelven todos los archivos de la base de datos.  
  
 La función integrada [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) se puede especificar y hace referencia a un archivo en la base de datos actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Nombre de base de datos.</br></br>Para almacenamiento de datos de SQL, este es el nombre de la base de datos que se almacenan en el nodo identificado por pdw_node_id. Cada nodo tiene una base de datos de tempdb con 13 archivos. Cada nodo tiene también una base de datos por la distribución, y cada base de datos de distribución tiene 5 archivos. Por ejemplo, si cada nodo contiene 4 distribuciones, los resultados muestran 20 archivos de base de datos de distribución por pdw_node_id. 
|**database_id**|**smallint**|Id. de base de datos.|  
|**file_id**|**smallint**|Id. de archivo.|  
|**sample_ms**|**bigint**|Número de milisegundos transcurridos desde que se inició el equipo. Esta columna se puede utilizar para comparar diferentes resultados de esta función.</br></br>El tipo de datos es **int** para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|**num_of_reads**|**bigint**|Número de operaciones de lectura realizadas en el archivo.|  
|**num_of_bytes_read**|**bigint**|Número total de bytes leídos en el archivo.|  
|**io_stall_read_ms**|**bigint**|Tiempo total, en milisegundos, que los usuarios han esperado para que se realicen las lecturas en el archivo.|  
|**num_of_writes**|**bigint**|Número de operaciones de escritura realizadas en este archivo.|  
|**num_of_bytes_written**|**bigint**|Número total de bytes escritos en el archivo.|  
|**io_stall_write_ms**|**bigint**|Tiempo total, en milisegundos, que los usuarios han esperado para que se completen las escrituras en el archivo.|  
|**io_stall**|**bigint**|Tiempo total, en milisegundos, que los usuarios han esperado para que se completen las operaciones de E/S en el archivo.|  
|**size_on_disk_bytes**|**bigint**|Número de bytes utilizados en el disco para este archivo. En el caso de archivos dispersos, este número es el número real de bytes en el disco utilizados para las instantáneas de base de datos.|  
|**file_handle**|**varbinary**|Identificador de archivo de Windows para este archivo.|  
|**io_stall_queued_read_ms**|**bigint**|**No se aplica a:**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)].<br /><br /> Latencia total de E/S introducida por el regulador de recursos de E/S para las lecturas. No admite valores NULL. Para obtener más información, consulte [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).|  
|**io_stall_queued_write_ms**|**bigint**|**No se aplica a:**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)].<br /><br />  Latencia total de E/S introducida por el regulador de recursos de E/S para las escrituras. No admite valores NULL.|
|**pdw_node_id**|**int**|**Se aplica a:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]</br></br>Identificador del nodo para la distribución.
 
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE. Para obtener más información, consulte [funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Ejemplos  

### <a name="a-return-statistics-for-a-log-file"></a>A. Devolver estadísticas de un archivo de registro

**Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure

 El ejemplo siguiente devuelve todas las estadísticas para el archivo de registro en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT * FROM sys.dm_io_virtual_file_stats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="b-return-statistics-for-file-in-tempdb"></a>B. Devolver estadísticas para el archivo en tempdb

**Se aplica a:** almacenamiento de datos SQL Azure

```sql
SELECT * FROM sys.dm_pdw_nodes_io_virtual_file_stats 
WHERE database_name = ‘tempdb’ AND file_id = 2;

```

## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [¿O relacionados con las funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

