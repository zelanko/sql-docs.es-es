---
title: Sys.dm_tran_commit_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 33cd6bb98fe17121a3903a82566dded929af6c8b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603774"
---
# <a name="change-tracking---sysdmtrancommittable"></a>Change Tracking - sys.dm_tran_commit_table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra una fila para cada transacción que se confirma para una tabla sometida al seguimiento de cambios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La vista de administración sys.dm_tran_commit_table, que se proporciona por compatibilidad, expone la información relacionada con la transacción que el seguimiento de cambios almacena en la tabla del sistema sys.syscommittab. En la tabla sys.syscommittab se proporciona una asignación persistente eficaz entre un identificador de transacción específico de la base de datos y el número de flujo de registro de confirmación (LSN) de la transacción y marca de tiempo de confirmación. Los datos que están almacenados en la tabla sys.syscommittab y que se exponen en esta vista de administración están sujetos a limpieza según el período de retención especificado cuando se configuró el seguimiento de cambios.  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_tran_commit_table**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|Número que se incrementa regularmente y que actúa como marca de tiempo específico de la base de datos para cada transacción confirmada.|  
|xdes_id|**bigint**|Identificador interno específico de la base de datos para la transacción.|  
|commit_lbn|**bigint**|Número del bloque de registros que contiene la entrada de registro de confirmación para la transacción.|  
|commit_csn|**bigint**|Número de secuencia de la confirmación específico de la instancia para la transacción.|  
|commit_time|**smalldatetime**|Hora en que se confirmó la transacción.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Acerca del seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


