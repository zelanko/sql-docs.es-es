---
title: Sys.dm_db_xtp_checkpoint_files (Transact-SQL) | Documentos de Microsoft
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cae0fb4ca29959382ac64307ea52851557d0174f
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdbxtpcheckpointfiles-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Muestra información sobre los archivos de puntos de comprobación, incluidos el tamaño de archivo, la ubicación física y el identificador de transacción.  
  
> **Nota:** para el punto de comprobación actual que no ha cerrado, la columna Estado de s`ys.dm_db_xtp_checkpoint_files` será UNDER CONSTRUCTION para los nuevos archivos. Un punto de comprobación se cierra automáticamente cuando no hay suficientes crecimiento del registro de transacciones desde el último punto de comprobación o si emite la `CHECKPOINT` comando ([punto de comprobación &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)).  
  
 Un grupo de archivos con optimización para memoria utiliza internamente archivos de solo anexar para almacenar las filas insertadas y eliminadas para tablas en memoria. Hay dos tipos de archivos: Un archivo de datos contiene filas insertadas, mientras que un archivo delta contiene referencias a las filas eliminadas. 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] es sustancialmente diferente de las versiones más recientes y se describe más abajo en el tema en [SQL Server 2014](#bkmk_2014).  
  
 Para obtener más información, consulte [crear y administrar el almacenamiento para los objetos con optimización para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
##  <a name="bkmk_2016"></a> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores  
 En la tabla siguiente se describe las columnas para `sys.dm_db_xtp_checkpoint_files`, empezando por **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**.  
  
|Nombre de columna|Tipo|Description|  
|-----------------|----------|-----------------|  
|container_id|**int**|Identificador del contenedor (representado como un archivo de tipo FILESTREAM en sys.database_files) del que forma parte el archivo de datos o delta. Combinaciones con file_id en [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|GUID del contenedor, que forma parte del archivo raíz, datos o delta. Combinaciones con file_guid en la tabla sys.database_files.|  
|checkpoint_file_id|**uniqueidentifier**|GUID del archivo de punto de comprobación.|  
|relative_file_path|**nvarchar(256)**|Ruta de acceso del archivo con respecto a contenedor a que está asignado.|  
|file_type|**smallint**|-1 para libre<br /><br /> 0 para el archivo de datos.<br /><br /> 1 para el archivo DELTA.<br /><br /> 2 para el archivo raíz<br /><br /> 3 para el archivo de datos de gran tamaño|  
|file_type_desc|**nvarchar(60)**|Archivos de libre, todo ello mantenerlos como libres están disponibles para la asignación. Archivos gratuitos pueden variar de tamaño según las necesidades previstas por el sistema. El tamaño máximo es 1GB.<br /><br /> DATOS - archivos de datos contienen filas que se han insertado en tablas optimizadas en memoria.<br /><br /> DELTA - archivos Delta contienen referencias a las filas de los archivos de datos que se han eliminado.<br /><br /> ROOT - archivos raíz contienen metadatos del sistema para los objetos compilados de forma nativa y con optimización para memoria.<br /><br /> DATOS de gran tamaño: grandes archivos de datos contienen valores insertados en (columnas varchar y varbinary (max), así como los segmentos de columna que forman parte de los índices de almacén de columnas en tablas optimizadas en memoria.|  
|internal_storage_slot|**int**|El índice del archivo en la matriz de almacenamiento interno. NULL para la raíz o de estado que no sea 1.|  
|checkpoint_pair_file_id|**uniqueidentifier**|Archivo de datos correspondientes o DELTA. NULL para la raíz.|  
|file_size_in_bytes|**bigint**|Tamaño del archivo en el disco.|  
|file_size_used_in_bytes|**bigint**|Para los pares de archivos de punto de comprobación que todavía se están llenando, esta columna se actualizará después del punto de comprobación siguiente.|  
|logical_row_count|**bigint**|Para los datos, el número de filas insertadas.<br /><br /> Para Delta, número de filas se elimina después de tener en cuenta las tabla de destino.<br /><br /> Para la raíz, es NULL.|  
|state|**smallint**|0 – PRECREATED<br /><br /> 1 - EN CONSTRUCCIÓN<br /><br /> 2 - ACTIVE<br /><br /> 3 – MERGE TARGET<br /><br /> 8: ESPERA DE TRUNCAMIENTO DEL REGISTRO|  
|state_desc|**nvarchar(60)**|PRECREATED: un número de archivos de punto de comprobación se preasignan para minimizar o eliminar cualquier espera para asignar nuevos archivos mientras se ejecutan las transacciones. Estos creados previamente archivos pueden variar de tamaño, según las necesidades estimadas de la carga de trabajo, pero no contienen ningún dato. Se trata de una sobrecarga de almacenamiento de bases de datos con un grupo de archivos.<br /><br /> EN construcción - estos archivos de punto de comprobación están elaborando, lo que significa que se van a rellenar basándose en los registros generados por la base de datos y aún no forman parte de un punto de control.<br /><br /> ACTIVE: contienen las filas insertadas y eliminadas de puntos de comprobación cerrados anteriores. Contienen el contenido de las tablas que lee el área en la memoria antes de aplicar la parte activa del registro de transacciones en el reinicio de la base de datos. Esperamos que el tamaño de estos archivos de punto de comprobación para ser aproximadamente 2 x del tamaño en memoria de tablas optimizadas en memoria, suponiendo que la operación de combinación se mantiene al nivel de la carga de trabajo transaccional.<br /><br /> TARGET MERGE: el destino de las operaciones de combinación - estos archivos de punto de comprobación almacenar las filas de datos consolidada de los archivos de origen que se identificaron mediante la directiva de combinación. Una vez instalada la mezcla, TARGET MERGE cambia al estado ACTIVE.<br /><br /> Esperando el TRUNCAMIENTO del registro: una vez que se ha instalado la mezcla y el CFP de destino de combinación es parte del punto de comprobación durable, la transición de archivos de punto de control de combinación origen en este estado. Archivos en este estado son necesarios para el correcto funcionamiento de la base de datos con la tabla optimizada en memoria.  Por ejemplo, para recuperarse de un punto de comprobación durable para ir a un momento anterior en el tiempo.|  
|lower_bound_tsn|**bigint**|Límite inferior de la transacción en el archivo; null si no está en estado (1, 3).|  
|upper_bound_tsn|**bigint**|Límite superior de la transacción en el archivo; null si no está en estado (1, 3).|  
|begin_checkpoint_id|**bigint**|Identificador del punto de control de inicio.|  
|end_checkpoint_id|**bigint**|Identificador del punto de comprobación final.|  
|last_updated_checkpoint_id|**bigint**|Id. del último punto de control que actualiza este archivo.|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar(60)**|0 = &GT; UNENCRTPTED<br /><br /> 1 = &GT; CIFRADA CON LA CLAVE 1<br /><br /> 2 = &GT; CIFRADA CON LA CLAVE 2. Válido únicamente para los archivos activos.|  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 En la tabla siguiente se describe las columnas para `sys.dm_db_xtp_checkpoint_files`, para **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**.  
  
|Nombre de columna|Tipo|Description|  
|-----------------|----------|-----------------|  
|container_id|**int**|Identificador del contenedor (representado como un archivo de tipo FILESTREAM en sys.database_files) del que forma parte el archivo de datos o delta. Combinaciones con file_id en [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|GUID del contenedor del que forma parte el archivo de datos o delta.|  
|checkpoint_file_id|**GUID**|Identificador del archivo de datos o delta.|  
|relative_file_path|**nvarchar(256)**|Ruta de acceso al archivo de datos o delta, con respecto a la ubicación del contenedor.|  
|file_type|**tinyint**|0 para el archivo de datos.<br /><br /> 1 para el archivo delta.<br /><br /> Es NULL si la columna state está establecida en 7.|  
|file_type_desc|**nvarchar(60)**|El tipo de archivo: DATA_FILE, DELTA_FILE o NULL si la columna de estado se establece en 7.|  
|internal_storage_slot|**int**|El índice del archivo en la matriz de almacenamiento interno. Es NULL si la columna state está establecida en 2 o 3.|  
|checkpoint_pair_file_id|**uniqueidentifier**|Archivo de datos o delta correspondiente.|  
|file_size_in_bytes|**bigint**|Tamaño del archivo que se usa. Es NULL si la columna state está establecida en 5, 6 o 7.|  
|file_size_used_in_bytes|**bigint**|Tamaño usado del archivo que se emplea. Es NULL si la columna state está establecida en 5, 6 o 7.<br /><br /> Para los pares de archivos de punto de comprobación que todavía se están llenando, esta columna se actualizará después del punto de comprobación siguiente.|  
|inserted_row_count|**bigint**|Número de filas del archivo de datos.|  
|deleted_row_count|**bigint**|Número de filas eliminadas del archivo delta.|  
|drop_table_deleted_row_count|**bigint**|Número de filas de los archivos de datos afectados por una operación de quitar tabla. Se aplica a los archivos de datos cuando la columna state es igual a 1.<br /><br /> Muestra los números de filas eliminadas de las tablas quitadas. Las estadísticas drop_table_deleted_row_count se compilan una vez que se completa la recolección de elementos no utilizados de memoria de las filas de las tablas quitadas y cuando se toma un punto de comprobación. Si reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de que las estadísticas de tablas quitadas se reflejen en esta columna, se actualizarán las estadísticas como parte de la recuperación. El proceso de recuperación no carga filas de tablas quitadas. Las estadísticas de tablas quitadas se compilan durante la fase de carga y se muestran en esta columna cuando se completa la recuperación.|  
|state|**int**|0 – PRECREATED<br /><br /> 1 – UNDER CONSTRUCTION<br /><br /> 2 - ACTIVE<br /><br /> 3 – MERGE TARGET<br /><br /> 4 – MERGED SOURCE<br /><br /> 5 – REQUIRED FOR BACKUP/HA<br /><br /> 6 – IN TRANSITION TO TOMBSTONE<br /><br /> 7 – TOMBSTONE|  
|state_desc|**nvarchar(60)**|PRECREATED: se mantiene preasignado un pequeño conjunto de pares de archivos de datos y delta, también conocidos como pares de archivos de punto de comprobación (CFP), para minimizar o eliminar cualquier espera para asignar nuevos archivos mientras se ejecutan las transacciones. Son de tamaño completo con un tamaño de archivo de datos de 128 MB y un tamaño de archivo delta de 8 MB pero no contienen ningún dato. El número de CFP se calcula como el número de procesadores o programadores lógicos (uno por núcleo, sin valor máximo) con un mínimo de 8. Se trata de una sobrecarga de almacenamiento fija en bases de datos con tablas optimizadas para memoria.<br /><br /> UNDER CONSTRUCTION: conjunto de CFP que almacenan las filas de datos recién insertadas y posiblemente eliminadas desde el último punto de comprobación.<br /><br /> ACTIVE: contienen las filas insertadas y eliminadas de puntos de comprobación cerrados anteriores. Estos CFP contienen todas las filas insertadas y eliminadas necesarias antes de aplicar la parte activa del registro de transacciones en el reinicio de la base de datos. El tamaño de estos CFP será aproximadamente el doble del tamaño en memoria de las tablas optimizadas para memoria, siempre y cuando la operación de combinación esté actualizada con la carga de trabajo transaccional.<br /><br /> TARGET MERGE: el CFP almacena las filas de datos consolidadas de los CFP identificados por la directiva de mezcla. Una vez instalada la mezcla, TARGET MERGE cambia al estado ACTIVE.<br /><br /> MERGED SOURCE: una vez instalada la operación de mezcla, los CFP de origen se marcan como MERGED SOURCE. Tenga en cuenta que el evaluador de la directiva de mezcla puede identificar varias mezclas pero un CFP solo puede participar en una operación de mezcla.<br /><br /> REQUIRED FOR BACKUP/HA: una vez instalada la mezcla y cuando el CFP con el estado MERGE TARGET forma parte del punto de comprobación durable, los CFP de origen de mezcla cambian a este estado. Los CFP que están en este estado son necesarios para el correcto funcionamiento de la base de datos con tablas optimizadas para memoria.  Por ejemplo, para recuperarse de un punto de comprobación durable para ir a un momento anterior en el tiempo. Un CFP se puede marcar para la recolección de elementos no utilizados una vez que el punto de truncamiento del registro sobrepasa los límites de su intervalo de transacción.<br /><br /> IN TRANSITION TO TOMBSTONE: el motor de OLTP en memoria no necesita estos CFP y se puede hacer su recolección de elementos no utilizados. Este estado indica que estos CFP están esperando que el subproceso de fondo haga la transición al estado siguiente, que es TOMBSTONE.<br /><br /> TOMBSTONE: estos CFP están esperando a que el recolector de elementos no utilizados de la secuencia de archivos recolecte sus elementos no utilizados. ([sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|El límite inferior de las transacciones contenidas en el archivo. Es NULL si la columna state no tiene el valor 2, 3 o 4.|  
|upper_bound_tsn|**bigint**|El límite superior de las transacciones contenidas en el archivo. Es NULL si la columna state no tiene el valor 2, 3 o 4.|  
|last_backup_page_count|**int**|Recuento de páginas lógicas que se determina en la última copia de seguridad. Se aplica cuando la columna state está establecida en 2, 3, 4 o 5. Es NULL si no se conoce el recuento de páginas.|  
|delta_watermark_tsn|**int**|Transacción del último punto de comprobación que escribió en este archivo delta. Es el límite para el archivo delta.|  
|last_checkpoint_recovery_lsn|**nvarchar(23)**|Número de secuencia de registro de recuperación del último punto de comprobación que todavía necesita el archivo.|  
|tombstone_operation_lsn|**nvarchar(23)**|El archivo se eliminará una vez que tombstone_operation_lsn esté detrás del número de secuencia de registro del truncamiento del registro.|  
|logical_deletion_log_block_id|**bigint**|Solo se aplica al estado 5.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso `VIEW DATABASE STATE` en el servidor.  
  
## <a name="use-cases"></a>Casos de uso  
 Puede calcular el almacenamiento utilizado por OLTP en memoria como sigue:  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
Para ver un desglose de utilización de recursos por tipo de archivos y el estado que se ejecute la siguiente consulta:
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de tablas optimizadas en memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
