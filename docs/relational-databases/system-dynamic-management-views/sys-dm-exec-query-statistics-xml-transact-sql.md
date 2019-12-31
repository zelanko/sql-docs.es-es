---
title: Sys. dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 35f9cdfcc40d417a6aed19a3abe0e590061b2eb7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75256015"
---
# <a name="sysdm_exec_query_statistics_xml-transact-sql"></a>Sys. dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Devuelve el plan de ejecución de la consulta para las solicitudes en curso. Use esta DMV para recuperar SHOWPLAN XML con estadísticas transitorias. 

## <a name="syntax"></a>Sintaxis

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>Argumentos 
*session_id*  
 Es el identificador de sesión que ejecuta el lote que se va a buscar. *session_id* es **smallint**. *session_id* se pueden obtener de los siguientes objetos de administración dinámica:  
  
-   [Sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [Sys. dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [Sys. dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>Tabla devuelta

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|Id. de la sesión. No acepta valores NULL.|
|request_id|**Inter**|Id. de la solicitud. No acepta valores NULL.|
|sql_handle|**varbinary (64)**|Es un token que identifica de forma única el lote o el procedimiento almacenado del que forma parte la consulta. Acepta valores NULL.|
|plan_handle|**varbinary (64)**|Es un token que identifica de forma única un plan de ejecución de consulta para un lote que se está ejecutando actualmente. Acepta valores NULL.|
|query_plan|**Xml**|Contiene la representación del plan de presentación en tiempo de ejecución del plan de ejecución de consultas especificado con *plan_handle* que contienen estadísticas parciales. El plan de presentación está en formato XML. Se genera un plan para cada lote que contiene, por ejemplo, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] "ad hoc", llamadas a procedimientos almacenados y llamadas a funciones definidas por el usuario. Acepta valores NULL.|

## <a name="remarks"></a>Observaciones
Esta función del sistema está disponible a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] partir de SP1. Consulte KB [3190871](https://support.microsoft.com/help/3190871)

Esta función del sistema funciona en la infraestructura de generación de perfiles de estadísticas de ejecución de consultas **estándar** y **ligera** . Para obtener más información, consulte la [infraestructura de generación de perfiles de consulta](../../relational-databases/performance/query-profiling-infrastructure.md).  

En las siguientes condiciones, no se devuelve ningún resultado del plan de presentación en la columna **query_plan** de la tabla devuelta para **Sys. dm_exec_query_statistics_xml**:  
  
-   Si el plan de consulta que corresponde al *session_id* especificado ya no se está ejecutando, la columna de **query_plan** de la tabla devuelta es NULL. Por ejemplo, esta condición puede producirse si hay un retraso entre el momento en que se capturó el identificador del plan y el momento en que se usó con **Sys. dm_exec_query_statistics_xml**.  
    
Debido a una limitación en el número de niveles anidados permitidos en el tipo de datos **XML** , **Sys. dm_exec_query_statistics_xml** no puede devolver planes de consulta que cumplan o superen los 128 niveles de elementos anidados. En las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta condición impedía la devolución del plan de consulta y generaba el error 6335. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 y versiones posteriores, la columna **query_plan** devuelve NULL.   

## <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE` en el servidor.  

## <a name="examples"></a>Ejemplos  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>a. Examinar el plan de consulta activo y las estadísticas de ejecución de un lote en ejecución  
 En el ejemplo siguiente se consulta **Sys. dm_exec_requests** para encontrar la consulta interesante y `session_id` copiar su desde la salida.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 A continuación, para obtener el plan de consulta activo y las estadísticas de ejecución `session_id` , utilice el copiado con la función del sistema **Sys. dm_exec_query_statistics_xml**.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 O combinado para todas las solicitudes en ejecución.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>Véase también
  [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

