---
title: sys.dm_os_buffer_descriptors (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_buffer_descriptors_TSQL
- dm_os_buffer_descriptors_TSQL
- sys.dm_os_buffer_descriptors
- dm_os_buffer_descriptors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_descriptors dynamic management view
ms.assetid: 012aab95-8888-4f35-9ea3-b5dff6e3f60f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c03bbdbe271500ecf417fe3b5c125304001a05e
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="sysdmosbufferdescriptors-transact-sql"></a>sys.dm_os_buffer_descriptors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de todas las páginas de datos que están actualmente en el grupo de búferes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La salida de esta vista se puede utilizar para determinar la distribución de páginas de la base de datos en el grupo de búferes según la base de datos, el objeto o el tipo. En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], esta vista de administración dinámica también devuelve información sobre las páginas de datos del archivo de la extensión del grupo de búferes. Para obtener más información, consulte [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md).  
  
 Cuando se lee una página de datos del disco, esta se copia en el grupo de búferes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se almacena en caché para volver a utilizarla. Cada página de datos almacenada en caché tiene un descriptor de búfer. Los descriptores de búfer únicamente identifican cada página de datos que está almacenada actualmente en memoria caché en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sys.dm_os_buffer_descriptors devuelve páginas en memoria caché para todas las bases de datos de usuario y de sistema. Esto incluye las páginas que están asociadas a la base de datos Resource.  
  
> **Nota:** para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_buffer_descriptors**.  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Identificador de la base de datos asociada con la página en el grupo de búferes. Acepta valores NULL.|  
|file_id|**int**|Identificador del archivo que almacena la imagen permanente de la página. Acepta valores NULL.|  
|page_id|**int**|Identificador de la página dentro del archivo. Acepta valores NULL.|  
|page_level|**int**|Nivel de índice de la página. Acepta valores NULL.|  
|allocation_unit_id|**bigint**|Identificador de la unidad de asignación de la página. Este valor se puede utilizar para combinar sys.allocation_units. Acepta valores NULL.|  
|page_type|**nvarchar(60)**|Tipo de la página, como: página de datos o página de índice. Acepta valores NULL.|  
|row_count|**int**|Número de filas de la página. Acepta valores NULL.|  
|free_space_in_bytes|**int**|Cantidad, en bytes, de espacio disponible en la página. Acepta valores NULL.|  
|is_modified|**bit**|1 = La página se ha modificado después de leerse en el disco. Acepta valores NULL.|  
|numa_node|**int**|Nodo de acceso no uniforme a memoria para el búfer. Acepta valores NULL.|  
|read_microsec|**bigint**|El tiempo real (en microsegundos) necesario para leer la página en el búfer. Este número se restablece cuando se reutiliza el búfer. Acepta valores NULL.|  
|is_in_bpool_extension|**bit**|1 = página se encuentra en la extensión del grupo de búferes. Acepta valores NULL.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.  
  
## <a name="remarks"></a>Comentarios  
 Sys.dm_os_buffer_descriptors devuelve páginas que están siendo utilizadas por la base de datos de recursos. Sys.dm_os_buffer_descriptors no devuelve información sobre páginas descartadas ni disponibles, ni sobre páginas con errores durante su lectura.  
  
|De|A|El|Relación|  
|----------|--------|--------|------------------|  
|sys.dm_os_buffer_descriptors|sys.databases|database_id|varios a uno|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.allocation_units|allocation_unit_id|varios a uno|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.database_files|file_id|varios a uno|  
|sys.dm_os_buffer_descriptors|sys.dm_os_buffer_pool_extension_configuration|file_id|varios a uno|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-cached-page-count-for-each-database"></a>A. Devolver el recuento de páginas almacenadas en caché de cada base de datos  
 En el ejemplo siguiente se devuelve el recuento de páginas cargadas para cada base de datos.  
  
```  
SELECT COUNT(*)AS cached_pages_count  
    ,CASE database_id   
        WHEN 32767 THEN 'ResourceDb'   
        ELSE db_name(database_id)   
        END AS database_name  
FROM sys.dm_os_buffer_descriptors  
GROUP BY DB_NAME(database_id) ,database_id  
ORDER BY cached_pages_count DESC;  
```  
  
### <a name="b-returning-cached-page-count-for-each-object-in-the-current-database"></a>B. Devolver el recuento de páginas almacenadas en caché para cada objeto de la base de datos actual  
 En el ejemplo siguiente se devuelve el recuento de páginas cargadas para cada objeto en la base de datos actual.  
  
```  
SELECT COUNT(*)AS cached_pages_count   
    ,name ,index_id   
FROM sys.dm_os_buffer_descriptors AS bd   
    INNER JOIN   
    (  
        SELECT object_name(object_id) AS name   
            ,index_id ,allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.hobt_id   
                    AND (au.type = 1 OR au.type = 3)  
        UNION ALL  
        SELECT object_name(object_id) AS name     
            ,index_id, allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.partition_id   
                    AND au.type = 2  
    ) AS obj   
        ON bd.allocation_unit_id = obj.allocation_unit_id  
WHERE database_id = DB_ID()  
GROUP BY name, index_id   
ORDER BY cached_pages_count DESC;  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Base de datos Resource](../../relational-databases/databases/resource-database.md)   
 [Sys.dm_os_buffer_pool_extension_configuration &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)  
  
  


