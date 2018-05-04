---
title: backupfilegroup (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backupfilegroup_TSQL
- backupfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], backupfilegroup system table
- backupfilegroup system table
ms.assetid: d26e8fbe-f5c5-4e10-b2bd-0d8e16ea21f9
caps.latest.revision: 53
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 610967323ce513cf20749e75945e4b6efe74e986
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada grupo de archivos de una base de datos en el momento de crear la copia de seguridad. **backupfilegroup** se almacena en la **msdb** base de datos.  
  
> [!NOTE]  
>  El **backupfilegroup** tabla muestra la configuración del grupo de archivos de la base de datos, no del conjunto de copia de seguridad. Para identificar si un archivo se incluye en el conjunto de copia de seguridad, use la **is_present** columna de la [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) tabla.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Conjunto de copia de seguridad que contiene este grupo de archivos.|  
|**Nombre**|**sysname**|Nombre del grupo de archivos.|  
|**filegroup_id**|**int**|Id. del grupo de archivos; único en la base de datos. Corresponde a **data_space_id** en **sys.filegroups**.|  
|**filegroup_guid**|**uniqueidentifier**|Identificador único global para el grupo de archivos. Puede ser NULL.|  
|**Tipo**|**char(2)**|Tipo de contenido, uno de los siguientes:<br /><br /> FG = Grupo de archivos "Rows"<br /><br /> SL = Grupo de archivos de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**type_desc**|**nvarchar(60)**|Descripción del tipo de función, una de:<br /><br /> ROWS_FILEGROUP <br /><br /> SQL_LOG_FILEGROUP |  
|**is_default**|**bit**|Grupo de archivos predeterminado, que se utiliza cuando no se ha especificado ningún otro en CREATE TABLE o CREATE INDEX.|  
|**is_readonly**|**bit**|1 = El grupo de archivos es de solo lectura.|  
|**log_filegroup_guid**|**uniqueidentifier**|Puede ser NULL.|  
  
## <a name="remarks"></a>Comentarios  
  
> [!IMPORTANT]  
>  El mismo nombre de grupo de archivos puede aparecer en diferentes bases de datos; no obstante, cada grupo de archivos tiene su propio GUID. Por lo tanto, **(backup_set_id, filegroup_guid)** es una clave única que identifica un grupo de archivos en **backupfilegroup**.  
  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY rellena las columnas de la **backupmediaset** tabla con los valores apropiados del encabezado del conjunto de medios.  
  
 Para reducir el número de filas en esta tabla y en otras tablas de historial y de copia de seguridad, ejecute el [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad y restaurar tablas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
