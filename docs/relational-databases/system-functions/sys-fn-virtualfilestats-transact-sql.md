---
title: Sys. fn_virtualfilestats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aade9e02515e0d18e4edae188d72e5edafebbd3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68059185"
---
# <a name="sysfn_virtualfilestats-transact-sql"></a>sys.fn_virtualfilestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve las estadísticas de E/S de los archivos de las bases de datos, incluidos los archivos de registro. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta información también está disponible en la vista de administración dinámica [Sys. dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) .  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_virtualfilestats ( { database_id | NULL } , { file_id | NULL } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_id* | ACEPTA  
 Es el ID. de la base de datos. *database_id* es de **tipo int**y no tiene ningún valor predeterminado. Especifique NULL para devolver información de todas las bases de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *file_id* | ACEPTA  
 Identificador del archivo. *file_id* es de **tipo int**y no tiene ningún valor predeterminado. Especifique NULL para devolver información de todos los archivos de la base de datos.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**DbId**|**smallint**|Id. de la base de datos.|  
|**FileId**|**smallint**|Identificador de archivo.|  
|**Indicaciones**|**BIGINT**|Marca de tiempo de la base de datos en la que se obtuvieron los datos. **int** en versiones anteriores [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]a. |  
|**NumberReads**|**BIGINT**|Número de operaciones de lectura realizadas en el archivo.|  
|**BytesRead**|**BIGINT**|Número de bytes leídos emitidos en el archivo.|  
|**IoStallReadMS**|**BIGINT**|Tiempo total, en milisegundos, que los usuarios han esperado para que finalicen las E/S de lectura en el archivo.|  
|**NumberWrites**|**BIGINT**|Número de operaciones de escritura realizadas en el archivo.|  
|**BytesWritten**|**BIGINT**|Número de bytes escritos en el archivo.|  
|**IoStallWriteMS**|**BIGINT**|Tiempo total, en milisegundos, que los usuarios han esperado para que finalicen las E/S de escritura en el archivo.|  
|**IoStallMS**|**BIGINT**|Suma de **IoStallReadMS** y **IoStallWriteMS**.|  
|**FileHandle**|**BIGINT**|Valor del identificador de archivos.|  
|**BytesOnDisk**|**BIGINT**|Tamaño físico del archivo (recuento de bytes) en disco.<br /><br /> En el caso de los archivos de base de datos, este valor es el mismo que el **tamaño** en **Sys. database_files**, pero se expresa en bytes en lugar de en páginas.<br /><br /> En los archivos dispersos de instantáneas de base de datos, se trata del espacio que utiliza el sistema operativo para el archivo.|  
  
## <a name="remarks"></a>Observaciones  
 **fn_virtualfilestats** es una función con valores de tabla del sistema que proporciona información estadística, como el número total de operaciones de e/s realizadas en un archivo. Puede utilizarse esta función como ayuda para realizar un seguimiento del tiempo que los usuarios tienen que esperar para leer un archivo o escribir en él. La función también ayuda a identificar los archivos que tienen mucha actividad de E/S.  
  
## <a name="permissions"></a>Permisos  
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
 En el siguiente ejemplo se muestra información estadística del archivo de registro de la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. La función `DB_ID` del sistema se usa para especificar el parámetro *database_id* .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [DB_ID &#40;&#41;de Transact-SQL](../../t-sql/functions/db-id-transact-sql.md)   
 [FILE_IDEX &#40;Transact-SQL&#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
