---
title: Sys. dm_io_pending_io_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 84bbf050161e6b66d10a1e7ce858459736248847
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827912"
---
# <a name="sysdm_io_pending_io_requests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila para cada solicitud de E/S pendiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para llamar a este método desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use el nombre **Sys. dm_pdw_nodes_io_pending_io_requests**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8**|Dirección de memoria de la solicitud de E/S. No admite valores NULL.|  
|**io_type**|**nvarchar(60)**|Tipo de solicitud de E/S pendiente. No admite valores NULL.|  
|**io_pending_ms_ticks**|**bigint**|Solo para uso interno. No admite valores NULL.| 
|**io_pending**|**int**|Indica si la solicitud de E/S sigue pendiente o Windows ya la ha completado. Una solicitud de E/S puede seguir pendiente incluso cuando Windows la ha completado; esto se debe a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aún no ha efectuado un cambio de contexto en el que se procesaría esta solicitud de E/S ni la ha quitado de esta lista. No admite valores NULL.|  
|**io_completion_routine_address**|**varbinary(8**|Función interna utilizada para llamar cuando se ha completado la solicitud de E/S. Acepta valores NULL.|  
|**io_user_data_address**|**varbinary(8**|Solo para uso interno. Acepta valores NULL.|  
|**scheduler_address**|**varbinary(8**|Programador en el que se ha emitido esta solicitud de E/S. La solicitud de E/S aparecerá en la lista de solicitudes de E/S pendientes del programador. Para obtener más información, vea [Sys. dm_os_schedulers &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). No admite valores NULL.|  
|**io_handle**|**varbinary(8**|Identificador del archivo que se utiliza en la solicitud de E/S. Acepta valores NULL.|  
|**io_offset**|**bigint**|Desplazamiento de la solicitud de E/S. No admite valores NULL.|  
|**io_handle_path**|**nvarchar(256)**| Ruta de acceso del archivo que se usa en la solicitud de e/s. Acepta valores NULL.|
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
  
## <a name="see-also"></a>Consulte también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I O funciones y vistas de administración dinámica relacionadas &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


