---
title: Sys.fn_virtualfilestats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_virtualfilestats_TSQL
- fn_virtualfilestats
dev_langs:
- TSQL
helpviewer_keywords:
- I/O [SQL Server], statistics
- fn_virtualfilestats function
- sys.fn_virtualfilestats function
- statistical information [SQL Server], I/O
ms.assetid: 96b28abb-b059-48db-be2b-d60fe127f6aa
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e49517833bb4869ae3eb72f078207e68caa09e98
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysfnvirtualfilestats-transact-sql"></a>sys.fn_virtualfilestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve las estadísticas de E/S de los archivos de las bases de datos, incluidos los archivos de registro. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta información también está disponible en la [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) vista de administración dinámica.  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_virtualfilestats ( { database_id | NULL } , { file_id | NULL } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_id* | ES NULL  
 Es el identificador de la base de datos. *database_id* es de tipo **int** y no tiene ningún valor predeterminado. Especifique NULL para devolver información de todas las bases de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *file_ID* | ES NULL  
 Identificador del archivo. *file_ID* es **int**, no tiene ningún valor predeterminado. Especifique NULL para devolver información de todos los archivos de la base de datos.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**DbId**|**smallint**|Id. de la base de datos.|  
|**FileId**|**smallint**|Identificador de archivo.|  
|**marca de tiempo**|**bigint**|Marca de tiempo de la base de datos en la que se obtuvieron los datos. **int** en las versiones anteriores [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. |  
|**NumberReads**|**bigint**|Número de operaciones de lectura realizadas en el archivo.|  
|**BytesRead**|**bigint**|Número de bytes leídos emitidos en el archivo.|  
|**IoStallReadMS**|**bigint**|Tiempo total, en milisegundos, que los usuarios han esperado para que finalicen las E/S de lectura en el archivo.|  
|**NumberWrites**|**bigint**|Número de operaciones de escritura realizadas en el archivo.|  
|**BytesWritten**|**bigint**|Número de bytes escritos en el archivo.|  
|**IoStallWriteMS**|**bigint**|Tiempo total, en milisegundos, que los usuarios han esperado para que finalicen las E/S de escritura en el archivo.|  
|**IoStallMS**|**bigint**|Suma de **IoStallReadMS** y **IoStallWriteMS**.|  
|**FileHandle**|**bigint**|Valor del identificador de archivos.|  
|**BytesOnDisk**|**bigint**|Tamaño físico del archivo (recuento de bytes) en disco.<br /><br /> Para archivos de base de datos, este es el mismo valor que **tamaño** en **sys.database_files**, pero se expresa en bytes, en lugar de páginas.<br /><br /> En los archivos dispersos de instantáneas de base de datos, se trata del espacio que utiliza el sistema operativo para el archivo.|  
  
## <a name="remarks"></a>Comentarios  
 **fn_virtualfilestats** es un función con valores de tabla que ofrece información estadística, como el número total de operaciones de E/s realizada en un archivo de sistema. Puede utilizarse esta función como ayuda para realizar un seguimiento del tiempo que los usuarios tienen que esperar para leer un archivo o escribir en él. La función también ayuda a identificar los archivos que tienen mucha actividad de E/S.  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-statistical-information-for-a-database"></a>A. Mostrar información estadística de una base de datos  
 En el siguiente ejemplo se muestra información estadística del archivo con Id. 1 de la base de datos con un Id. de `1`.  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(1, 1);  
GO  
```  
  
### <a name="b-displaying-statistical-information-for-a-named-database-and-file"></a>B. Mostrar información estadística de una base de datos y un archivo con nombre  
 En el siguiente ejemplo se muestra información estadística del archivo de registro de la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. La función del sistema `DB_ID` se utiliza para especificar el *database_id* parámetro.  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="c-displaying-statistical-information-for-all-databases-and-files"></a>C. Mostrar información estadística de todas las bases de datos y todos los archivos  
 En el siguiente ejemplo se muestra información estadística de todos los archivos de todas las bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(NULL,NULL);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)   
 [FILE_IDEX &#40;Transact-SQL&#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
