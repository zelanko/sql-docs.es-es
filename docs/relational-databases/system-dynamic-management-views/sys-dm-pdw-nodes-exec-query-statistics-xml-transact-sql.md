---
title: sys.dm_pdw_nodes_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
description: Vista de administración dinámica que devuelve el plan de ejecución de consultas para las solicitudes en curso. Use esta DMV para recuperar SHOWPLAN XML con estadísticas transitorias.
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
ms.openlocfilehash: 790431cd6effe4d1b3d21db46325782e05419e4f
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834188"
---
# <a name="dm_pdw_nodes_exec_query_statistics_xml-transact-sql"></a>dm_pdw_nodes_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Devuelve el plan de ejecución de la consulta para las solicitudes en curso. Use esta DMV para recuperar SHOWPLAN XML con estadísticas transitorias.

## <a name="table-returned"></a>Tabla devuelta

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|
|node_id|**int**|IDENTIFICADOR numérico único asociado al nodo.|
|session_id|**smallint**|Id. de la sesión. No acepta valores NULL.|
|request_id|**int**|Id. de la solicitud. No acepta valores NULL.|
|sql_handle|**varbinary (64)**|Es un token que identifica de forma única el lote o el procedimiento almacenado del que forma parte la consulta. Acepta valores NULL.|
|plan_handle|**varbinary (64)**|Es un token que identifica de forma única un plan de ejecución de consulta para un lote que se está ejecutando actualmente. Acepta valores NULL.|
|query_plan|**xml**|Contiene la representación del plan de presentación en tiempo de ejecución del plan de ejecución de consultas especificado con *plan_handle* que contienen estadísticas parciales. El plan de presentación está en formato XML. Se genera un plan para cada lote que contiene, por ejemplo, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] "ad hoc", llamadas a procedimientos almacenados y llamadas a funciones definidas por el usuario. Acepta valores NULL.|

## <a name="remarks"></a>Observaciones
Se aplican los mismos comentarios en [Sys.dm_exec_query_statistics_xml](./sys-dm-exec-query-statistics-xml-transact-sql.md?view=sql-server-ver15) .   

## <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE` en el servidor.  

## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>Pasos siguientes
 Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).