---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/16/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 461ee87f41692172b31125e36553c0eab0b09772
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Muestra el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] plan de ejecución de una consulta que se ejecute en un determinado [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodo o Control de proceso. Utilice esto para solucionar problemas de rendimiento de consultas mientras se ejecutan las consultas en los nodos de proceso y el nodo de Control.
  
Una vez que se entienden los problemas de rendimiento de consultas para SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las consultas se ejecutan en los nodos de proceso, hay varias maneras de mejorar el rendimiento. Posibles maneras de mejorar el rendimiento de las consultas de los nodos incluyen la creación de estadísticas de varias columnas, la creación de índices no clúster o usar sugerencias de consulta.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
Sintaxis para SQL Server:

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Almacenamiento de datos en paralelo Azure de sintaxis:
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *distribution_id*  
 Identificador de la distribución que se ejecuta el plan de consulta. Esto es un entero y no puede ser NULL. Usar cuando el destino es [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 *pdw_node_id*  
 Identificador del nodo que se está ejecutando el plan de consulta. Esto es un entero y no puede ser NULL. Se utiliza cuando el destino es un dispositivo.  
  
 *SPID*  
 Identificador de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sesión que se ejecuta el plan de consulta. Esto es un entero y no puede ser NULL.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
Requiere el permiso de servidor-estado de vista en el dispositivo.
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>Ejemplos:[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. Sintaxis básica de DBCC PDW_SHOWEXECUTIONPLAN  
 Cuando se ejecuta en un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] de la instancia, modifique la consulta anterior para seleccionar el distribution_id.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
Esto devolverá el spid de distribución que se ejecutan cada activamente. Si tuviera curiosidad sobre qué distribución 1 se estaba ejecutando en la sesión 375, ejecutaría el comando siguiente.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. Sintaxis básica de DBCC PDW_SHOWEXECUTIONPLAN  
 La consulta que se ejecuta demasiada es ya sea ejecutando un DMS consultar operación de plan o una operación de plan de consulta SQL.  
  
Si la consulta ejecuta una operación de plan de consulta DMS, puede utilizar la siguiente consulta para recuperar una lista de los identificadores de nodo e identificadores de sesión para conocer los pasos que no están completos.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
En función de los resultados de la consulta anterior, use la sql_spid y pdw_node_id como parámetros para DBCC PDW_SHOWEXEUCTIONPLAN. Por ejemplo, el siguiente comando muestra el plan de ejecución para pdw_node_id 201001 y sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Vea también
[DBCC PDW_SHOWPARTITIONSTATS &#40; Transact-SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)

