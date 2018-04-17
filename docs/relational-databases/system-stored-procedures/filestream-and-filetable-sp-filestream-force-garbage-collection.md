---
title: sp_filestream_force_garbage_collection (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_filestream_force_garbage_collection
- sp_filestream_force_garbage_collection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILESTREAM [SQL Server]
- sp_filestream_force_garbage_collection
ms.assetid: 9d1efde6-8fa4-42ac-80e5-37456ffebd0b
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b567ffa4ac9b56074742999c602914ebe7d3934d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spfilestreamforcegarbagecollection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Fuerza la ejecución del recolector de elementos no utilizados de FILESTREAM eliminando los archivos FILESTREAM innecesarios.  
  
 Un contenedor de FILESTREAM no se puede quitar hasta que el recolector de elementos no utilizados ha limpiado todos los archivos eliminados que contiene. El recolector de elementos no utilizados de FILESTREAM se ejecuta automáticamente. Sin embargo, si necesita quitar un contenedor antes el recolector de elementos no utilizados ha ejecutado, puede usar sp_filestream_force_garbage_collection para ejecutar manualmente el recolector de elementos no utilizados.  
  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_filestream_force_garbage_collection  
    [ @dbname = ]  'database_name',  
    [ @filename = ] 'logical_file_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **@dbname** = *database_name***'**  
 Indica el nombre de la base de datos en la que se debe ejecutar el recolector de elementos no utilizados.  
  
> [!NOTE]  
>  *dbname* es **sysname**. Si no se especifica, se supone que es la base de datos actual.  
  
 **@filename** = *nombre_de_archivo_lógico*  
 Especifica el nombre lógico del contenedor de FILESTREAM en el que se va a ejecutar el recolector de elementos no utilizados. **@filename** es opcional. Si no se especifica ningún nombre de archivo lógico, el recolector de elementos no utilizados limpia todos los contenedores FILESTREAM en la base de datos especificada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
  
|||  
|-|-|  
|Value|Descripción|  
|0|Operación correcta|  
|1|Error de operación|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Value|Description|  
|-----------|-----------------|  
|*file_name*|Indica el nombre del contenedor de FILESTREAM|  
|*num_collected_items*|Indica el número de elementos de FILESTREAM (archivos o directorios) que el recolector de elementos eliminados ha eliminado en este contenedor.|  
|*num_marked_for_collection_items*|Indica el número de elementos de FILESTREAM (archivos o directorios) que se han marcado para la recolección de elementos no utilizados en este contenedor. Estos elementos que no se haya eliminado, pero podrían ser candidatas para su eliminación después de la fase de recopilación de elementos no utilizados.|  
|*num_unprocessed_items*|Indica el número de elementos de FILESTREAM (archivos o directorios) que se podían haber eliminado y no se procesaron para la recolección de elementos no utilizados en este contenedor de FILESTREAM. Los elementos pueden no haberse procesado por diversas razones, por ejemplo:<br /><br /> Archivos que se tienen que anclar porque no se ha tomado la copia de seguridad de registros o CHECKPOINT.<br /><br /> Archivos del modelo de recuperación FULL o BULK_LOGGED.<br /><br /> Hay una transacción activa de ejecución prolongada.<br /><br /> No se ha ejecutado el trabajo del lector de registro de replicación. Vea las notas del producto [almacenamiento de FILESTREAM en SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=209156) para obtener más información.|  
|*last_collected_xact_seqno*|Devuelve el último número de secuencia de registro (LSN) correspondiente hasta el que el recolector de elementos no utilizados ha recolectado archivos del contenedor de FILESTREAM especificado.|  
  
## <a name="remarks"></a>Comentarios  
 Ejecuta explícitamente la tarea del recolector de elementos no utilizados de FILESTREAM hasta su finalización en la base de datos solicitada (y el contenedor de FILESTREAM). El proceso de recolección de elementos no utilizados quita los archivos que ya no se necesitan. El tiempo necesario para completar esta operación depende del tamaño de los datos de FILESTREAM en la base de datos o el contenedor, así como de la cantidad de actividad DML que se ha producido recientemente en los datos de FILESTREAM. Si bien esta operación se puede ejecutar mientras la base de datos está en línea, el rendimiento de la base de datos puede verse afectado durante la ejecución como consecuencia de diversas actividades de I/O que el proceso de recolección de elementos no utilizados lleva a cabo.  
  
> [!NOTE]  
>  Se recomienda que esta operación solo se ejecute cuando sea necesario y fuera las horas de actividad normales.  
  
Solo se pueden ejecutar simultáneamente varias invocaciones de este procedimiento almacenado en contenedores o bases de datos independientes.  

Debido a las operaciones de la fase 2, el procedimiento almacenado se debe ejecutar dos veces para eliminar realmente los archivos Filestream subyacentes.  

Colección de elementos no utilizados (GC) se basa en el truncamiento del registro. Por lo tanto, si los archivos se han eliminado recientemente en una base de datos mediante el modelo de recuperación completa, son GC-ed solo después de que se realiza una copia de seguridad del registro de esas partes del registro de transacciones y la parte de registro se marca inactiva. En una base de datos mediante el modelo de recuperación Simple, se produce un truncamiento del registro después de un `CHECKPOINT` se emitió contra la base de datos.  


## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol de la base de datos db_owner.  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos se ejecuta el recolector de elementos no utilizados para contenedores de FILESTREAM de la base de datos `FSDB`.  
  
### <a name="a-specifying-no-container"></a>A. Sin especificar ningún contenedor  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB';  
```  
  
### <a name="b-specifying-a-container"></a>B. Especificando un contenedor  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB',
    @filename = N'FSContainer';  
```  
  
## <a name="see-also"></a>Vea también  
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[FileStream y vistas de administración dinámica de FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[FileStream y vistas de catálogo de FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
