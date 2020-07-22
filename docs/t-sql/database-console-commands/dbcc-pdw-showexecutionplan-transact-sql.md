---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0895a01f3110c90172ab763ebd0991c259da985d
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484606"
---
# <a name="dbcc-pdw_showexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Muestra el plan de ejecución de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para una consulta que se ejecuta en un nodo de ejecución o un nodo de control determinado de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Úselo para solucionar problemas de rendimiento de consultas mientras se ejecutan las consultas en los nodos de ejecución y de control.
  
Una vez que se conozcan los problemas de rendimiento de las consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de SMP que se ejecutan en los nodos de ejecución, hay varias maneras de mejorar el rendimiento. Entre las diversas formas de mejorar el rendimiento de las consultas de los nodos de ejecución se incluye crear estadísticas de varias columnas, crear índices no agrupados o usar sugerencias de consulta.
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
Sintaxis de Azure SQL Data Warehouse:

```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Sintaxis para Almacenamiento de datos paralelos de Azure:
  
```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  

## <a name="arguments"></a>Argumentos  
 *distribution_id*  
 Identificador de la distribución que ejecuta el plan de consulta. Es un entero y no puede ser NULL. Se usa cuando el destino es [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 *pdw_node_id*  
 Identificador del nodo que ejecuta el plan de consulta. Es un entero y no puede ser NULL. Se usa cuando el destino es un dispositivo.  
  
 *spid*  
 Identificador de la sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecuta el plan de consulta. Es un entero y no puede ser NULL.  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso CONTROL en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
Requiere el permiso VIEW-SERVER-STATE en el dispositivo.
  
## <a name="examples-sssdw"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdw_showexecutionplan-basic-syntax"></a>A. Sintaxis básica de DBCC PDW_SHOWEXECUTIONPLAN  
 Cuando se ejecuta en una instancia de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], modifique la consulta anterior para seleccionar también el valor de distribution_id.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
Esto devolverá el spid de cada distribución que se ejecuta activamente. Si le interesa saber cuál es la distribución 1 que se ejecutaba en la sesión 375, debe ejecutar el comando siguiente.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-sspdw"></a>Ejemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdw_showexecutionplan-basic-syntax"></a>B. Sintaxis básica de DBCC PDW_SHOWEXECUTIONPLAN  
 Cuando una consulta se ejecuta durante mucho tiempo, significa que está ejecutando una operación de plan de consulta DMS o una operación de plan de consulta SQL.  
  
Si la consulta está ejecutando una operación de plan de consulta DMS, puede usar la consulta siguiente para recuperar una lista de los identificadores de nodo y de sesión para conocer los pasos que no se han completado.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
En función de los resultados de la consulta anterior, use los parámetros sql_spid y pdw_node_id para DBCC PDW_SHOWEXECUTIONPLAN. Por ejemplo, en el comando siguiente se muestra el plan de ejecución para pdw_node_id 201001 y sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Consulte también

- [DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
- [DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)
