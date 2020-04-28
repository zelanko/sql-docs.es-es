---
title: Sys. dm_pdw_nodes_exec_text_query_plan (Transact-SQL) | Microsoft Docs
description: Vista de administración dinámica que devuelve el plan de presentación en formato de texto para un lote de TSQL o para una instrucción concreta dentro del lote.
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
ms.openlocfilehash: 45f26c9569950c2450318abf546a838632e06f20
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73145670"
---
# <a name="sysdm_pdw_nodes_exec_text_query_plan--transact-sql"></a>Sys. dm_pdw_nodes_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Devuelve el plan de presentación en formato de texto para un lote [!INCLUDE[tsql](../../includes/tsql-md.md)] o para una instrucción concreta dentro del mismo.

## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pdw_node_ID**|**int**|IDENTIFICADOR numérico único asociado al nodo.|
|**DBID**|**smallint**|Identificador de la base de datos de contexto que estaba activa al compilarse la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondiente a este plan. En el caso de instrucciones SQL ad hoc y preparadas, identificador de la base de datos en que se compilaron las instrucciones.<br /><br /> Esta columna acepta valores NULL.|  
|**objectId**|**int**|Identificador del objeto (por ejemplo, procedimiento almacenado o función definida por el usuario) de este plan de consulta. Para lotes "ad hoc" y preparados, esta columna es **null**.<br /><br /> Esta columna acepta valores NULL.|  
|**número**|**smallint**|Entero de procedimiento almacenado numerado. Para lotes "ad hoc" y preparados, esta columna es **null**.<br /><br /> Esta columna acepta valores NULL.| 
|**cifra**|**bit**|Indica si el procedimiento almacenado correspondiente está cifrado.<br /><br /> 0 = no cifrado<br /><br /> 1 = cifrado<br /><br /> La columna no acepta valores NULL.|  
|**query_plan**|**nvarchar(max)**|Contiene la representación del plan de presentación de tiempo de compilación del plan de ejecución de consultas especificado con *plan_handle*. El plan de presentación está en formato de texto. Se genera un plan para cada lote que contiene, por ejemplo, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] "ad hoc", llamadas a procedimientos almacenados y llamadas a funciones definidas por el usuario.<br /><br /> Esta columna acepta valores NULL.|  

## <a name="remarks"></a>Observaciones  
Se aplican los mismos comentarios en [Sys. dm_exec_text_query_plan](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql?view=sql-server-ver15) .  

## <a name="permissions"></a>Permisos  
 Requiere **sysadmin** el rol de servidor `VIEW SERVER STATE` sysadmin o el permiso en el servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>Pasos siguientes
 Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).