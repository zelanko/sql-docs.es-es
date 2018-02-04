---
title: backupfile (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84b26ca09b8cd537ed40f0af8844f3f0c7627c86
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="backupfile-transact-sql"></a>backupfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada archivo de datos o de registro de una base de datos. Las columnas describen la configuración del archivo en el momento en que se realizó la copia de seguridad. Si el archivo está incluido en la copia de seguridad está determinado por la **is_present** columna. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Número de identificación exclusivo del archivo que contiene el conjunto de copia de seguridad. References **backupset(backup_set_id)**.|  
|**first_family_number**|**tinyint**|Número de familia del primer medio que contiene este archivo de copia de seguridad. Puede ser NULL.|  
|**first_media_number**|**smallint**|Número de medio del primer medio que contiene este archivo de copia de seguridad. Puede ser NULL.|  
|**filegroup_name**|**nvarchar(128)**|Nombre del grupo de archivos que contiene un archivo de base de datos del que se ha realizado una copia de seguridad. Puede ser NULL.|  
|**page_size**|**int**|Tamaño de la página, en bytes.|  
|**file_number**|**numeric(10,0)**|Número de identificación de archivo único en una base de datos (corresponde a **sys.database_files**. **file_ID**).|  
|**backed_up_page_count**|**numeric(10,0)**|Número de páginas incluidas en la copia de seguridad. Puede ser NULL.|  
|**file_type**|**char(1)**|Archivo incluido en la copia de seguridad; uno de los siguientes:<br /><br /> D = Archivo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> L = Archivo de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> F = Catálogo de texto completo.<br /><br /> Puede ser NULL.|  
|**source_file_block_size**|**numeric(10,0)**|Dispositivo en el que se encontraba el archivo de datos o de registro original cuando se hizo la copia de seguridad del mismo. Puede ser NULL.|  
|**file_size**|**numeric(20,0)**|Longitud en bytes del archivo del que se hace una copia de seguridad. Puede ser NULL.|  
|**logical_name**|**nvarchar(128)**|Nombre lógico del archivo del que se hace una copia de seguridad. Puede ser NULL.|  
|**physical_drive**|**nvarchar(260)**|Unidad física o nombre de partición. Puede ser NULL.|  
|**physical_name**|**nvarchar(260)**|Resto del nombre de archivo físico (del sistema operativo). Puede ser NULL.|  
|**state**|**tinyint**|Estado del archivo, uno de los siguientes:<br /><br /> 0 = Con conexión <br /><br /> 1 = En restauración <br /><br /> 2 = En recuperación <br /><br /> 3 = Recuperación pendiente <br /><br /> 4 = Sospechoso <br /><br /> 6 = Sin conexión <br /><br /> 7 = Inactivo<br /><br /> 8 = QUITAR<br /><br /> Nota: El valor 5 se omite para que estos valores se corresponden con los valores de los Estados de base de datos.|  
|**state_desc**|**nvarchar(64)**|Descripción del estado del archivo, uno de los siguientes:<br /><br /> ONLINE RESTORING <br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING <br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**numeric(25,0)**|Número de secuencia de registro en el que se creó el archivo.|  
|**drop_lsn**|**numeric(25,0)**|Número de flujo de registro en el que se quitó el archivo. Puede ser NULL.<br /><br /> Si el archivo no se ha quitado, este valor es NULL.|  
|**file_guid**|**uniqueidentifier**|Identificador único del archivo.|  
|**read_only_lsn**|**numeric(25,0)**|Número de flujo de registro en el que el grupo de archivos que contiene el archivo cambió de lectura/escritura a solo lectura (el cambio más reciente). Puede ser NULL.|  
|**read_write_lsn**|**numeric(25,0)**|Número de secuencia de registro en el que el grupo de archivos que contiene el archivo cambió de solo lectura a lectura/escritura (el cambio más reciente). Puede ser NULL.|  
|**differential_base_lsn**|**numeric(25,0)**|LSN de base para copias de seguridad diferenciales. Una copia de seguridad diferencial incluye únicamente el número de extensiones de datos con una secuencia de registro igual o mayor que **differential_base_lsn**.<br /><br /> Para otros tipos de copia de seguridad, el valor es NULL.|  
|**differential_base_guid**|**uniqueidentifier**|Para una copia de seguridad diferencial, el identificador único de la copia de seguridad de datos más reciente que forma la base diferencial del archivo; si el valor es NULL, el archivo se incluyó en la copia de seguridad diferencial (pero se agregó después de que se creara la base).<br /><br /> Para otros tipos de copia de seguridad, el valor es NULL.|  
|**backup_size**|**numeric(20,0)**|Tamaño en bytes de la copia de seguridad de este archivo.|  
|**filegroup_guid**|**uniqueidentifier**|Id. del grupo de archivos. Para buscar información de grupo de archivos en la tabla backupfilegroup, utilice **filegroup_guid** con **backup_set_id**.|  
|**is_readonly**|**bit**|1 = El archivo es de solo lectura.|  
|**is_present**|**bit**|1 = El archivo está incluido en el conjunto de copia de seguridad.|  
  
## <a name="remarks"></a>Comentarios  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY rellena las columnas de la **backupmediaset** tabla con los valores apropiados del encabezado del conjunto de medios.  
  
 Para reducir el número de filas en esta tabla y en otras tablas de historial y de copia de seguridad, ejecute el [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad y restauración tablas &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tablas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
