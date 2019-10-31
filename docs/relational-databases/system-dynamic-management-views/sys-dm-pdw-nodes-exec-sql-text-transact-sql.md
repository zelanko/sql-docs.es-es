---
title: Sys. DM _ _pdw_nodes_exec_sql_text (Transact-SQL) | Microsoft Docs
description: Vista de administración dinámica que devuelve el texto del lote SQL que se identifica mediante el sql_handle especificado.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: fd886217b2fb2caf0fe3f32e88b7bf0215ece1a9
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145680"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>Sys. PDW _nodes_dm_exec_sql_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Devuelve el texto del lote SQL que se identifica mediante el *sql_handle*especificado. Esta función con valores de tabla reemplaza a la función del sistema **Fn_get_sql**.  
   
## <a name="table-returned"></a>Tabla devuelta  
|Nombre de columna|Data type|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|IDENTIFICADOR numérico único asociado al nodo.|
|**dbid**|**smallint**|IDENTIFICADOR de la base de datos.<br /><br /> En el caso de instrucciones SQL no planeadas y preparadas, el identificador de la base de datos donde se compilaron las instrucciones.|  
|**objectid**|**int**|Identificador del objeto.<br /><br /> Este valor es NULL para las instrucciones SQL ad hoc y preparadas.|  
|**number**|**smallint**|En un procedimiento almacenado numerado, esta columna devuelve el número del procedimiento almacenado. Para obtener más información, vea [Sys. &#40;NUMBERED_PROCEDURES Transact-&#41;SQL](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md).<br /><br /> Este valor es NULL para las instrucciones SQL ad hoc y preparadas.|  
|**cifra**|**bit**|1: el texto SQL está cifrado.<br /><br /> 0: el texto SQL no está cifrado.|  
|**varchar(max)**|**ssNoVersion**|Texto de la consulta de SQL.<br /><br /> Este valor es NULL para objetos cifrados.|  

## <a name="remarks"></a>Notas  
Se aplican los mismos comentarios en [Sys. DM _ _exec_sql_text](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql?view=sql-server-ver15) .  
  
## <a name="permissions"></a>Permissions  
 Requiere el rol de servidor **sysadmin** o el permiso `VIEW SERVER STATE` en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Vistas &#40;de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos de TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>Pasos siguientes
 Para obtener más sugerencias sobre desarrollo, vea [SQL Data Warehouse información general sobre desarrollo](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).