---
title: sys.dm_os_volume_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_volume_stats_TSQL
- dm_os_volume_stats
- sys.dm_os_volume_stats
- sys.dm_os_volume_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_volume_stats dynamic management function
ms.assetid: fa1c58ad-8487-42ad-956c-983f2229025f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 647c47f57e8f6eb7f756ec5a6263ae5d5059b674
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosvolumestats-transact-sql"></a>sys.dm_os_volume_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre el volumen (directorio) del sistema operativo en que están almacenados los archivos y bases de datos especificados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilice esta función de administración dinámica para comprobar los atributos de la unidad de disco física y obtener información sobre el espacio disponible en el directorio.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_os_volume_stats (database_id, file_id)  
```  
  
##  <a name="Arguments"></a> Argumentos  
 *database_id*  
 Identificador de la base de datos. *database_id* es **int**, no tiene ningún valor predeterminado. No puede ser NULL.  
  
 *file_id*  
 Id. del archivo. *file_ID* es **int**, no tiene ningún valor predeterminado. No puede ser NULL.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
||||  
|-|-|-|  
|**Columna**|**Tipo de datos**|**Description**|  
|**database_id**|**int**|Identificador de la base de datos. No puede ser null.|  
|**file_id**|**int**|Id. del archivo. No puede ser null.|  
|**volume_mount_point**|**nvarchar(512)**|Punto de montaje en el que el volumen tiene su raíz. Puede devolver una cadena vacía.|  
|**volume_id**|**nvarchar(512)**|Identificador del volumen del sistema operativo. Puede devolver una cadena vacía|  
|**logical_volume_name**|**nvarchar(512)**|Nombre lógico del volumen. Puede devolver una cadena vacía|  
|**file_system_type**|**nvarchar(512)**|Tipo de volumen de sistema de archivos (por ejemplo NTFS, FAT, RAW). Puede devolver una cadena vacía|  
|**total_bytes**|**bigint**|Tamaño total del volumen en bytes. No puede ser null.|  
|**available_bytes**|**bigint**|Espacio disponible del volumen. No puede ser null.|  
|**supports_compression**|**bit**|Indica si el volumen admite la compresión del sistema operativo. No puede ser null.|  
|**supports_alternate_streams**|**bit**|Indica si el volumen admite flujos alternativos. No puede ser null.|  
|**supports_sparse_files**|**bit**|Indica si el volumen admite archivos dispersos.  No puede ser null.|  
|**is_read_only**|**bit**|Indica si el volumen está marcado actualmente como de solo lectura. No puede ser null.|  
|**is_compressed**|**bit**|Indica si el volumen está comprimido actualmente. No puede ser null.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-return-total-space-and-available-space-for-all-database-files"></a>A. Devolver el espacio total y el espacio disponible de todos los archivos de base de datos  
 El ejemplo siguiente devuelve el espacio total y el espacio disponible (en bytes) de todos los archivos de base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT f.database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.master_files AS f  
CROSS APPLY sys.dm_os_volume_stats(f.database_id, f.file_id);  
```  
  
### <a name="b-return-total-space-and-available-space-for-the-current-database"></a>B. Devolver el espacio total y el espacio disponible de la base de datos actual  
 El ejemplo siguiente devuelve el espacio total y el espacio disponible (en bytes) de los archivos de base de datos de la base de datos actual.  
  
```  
SELECT database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.database_files AS f  
CROSS APPLY sys.dm_os_volume_stats(DB_ID(f.name), f.file_id);  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
