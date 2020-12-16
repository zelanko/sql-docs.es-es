---
description: DBCC PDW_SHOWSPACEUSED (Transact-SQL)
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL)
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: cfdec40a3f8bba1746963ee20070eac5efd0b430
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462526"
---
# <a name="dbcc-pdw_showspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Muestra el número de filas, el espacio en disco reservado y el espacio en disco usado para una tabla específica o para todas las tablas de una base de datos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis
  
```syntaxsql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>Argumentos

 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
Nombre de una, dos o tres partes de la tabla que se va a mostrar. En el caso de los nombres de tabla de dos o tres partes, el nombre debe incluirse entre comillas dobles (""). El uso de comillas en un nombre de tabla de una parte es opcional. Cuando no se especifica ningún nombre de tabla, se muestra la información de la base de datos actual.  
  
## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.
  
## <a name="result-sets"></a>Conjuntos de resultados

Este es el conjunto de resultados de todas las tablas.  Antes de crear una memoria caché para una tabla replicada de Synapse, el resultado de DBCC refleja el tamaño total de la tabla de round robin subyacente de cada distribución.  Una vez creada la memoria caché, el resultado refleja el tamaño total de las tablas de round robin y la memoria caché.   
  
|Columna|Tipo de datos|Descripción|  
|------------|---------------|-----------------|  
|reserved_space|bigint|Espacio total usado para la base de datos, en KB.|  
|data_space|bigint|Espacio usado para los datos, en KB.|  
|index_space|bigint|Espacio usado para los índices, en KB.|  
|unused_space|bigint|Espacio que forma parte del espacio reservado y que no se usa, en KB.|  
|pdw_node_id|int|Nodo de ejecución que se usa para los datos.|  
  
Este es el conjunto de resultados de una tabla.
  
|Columna|Tipo de datos|Descripción|Intervalo|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|Número de filas.||  
|reserved_space|bigint|Espacio total reservado para el objeto, en KB.||  
|data_space|bigint|Espacio usado para los datos, en KB.||  
|index_space|bigint|Espacio usado para los índices, en KB.||  
|unused_space|bigint|Espacio que forma parte del espacio reservado y que no se usa, en KB.||  
|pdw_node_id|int|Nodo de ejecución que se usa para notificar el uso de espacio.||  
|distribution_id|int|Distribución que se usa para notificar el uso de espacio.|En cuanto al almacenamiento de datos paralelos, su valor es -1 para las tablas replicadas.|  
  
## <a name="examples-sssdw-and-sspdw"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdw_showspaceused-basic-syntax"></a>A. Sintaxis básica de DBCC PDW_SHOWSPACEUSED  
En los ejemplos siguientes se muestran varias formas de mostrar el número de filas, el espacio en disco reservado y el espacio en disco usado por la tabla FactInternetSales en la base de datos [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. Mostrar el espacio en disco usado por todas las tablas de la base de datos actual  

 En el ejemplo siguiente se muestra el espacio en disco reservado y usado por todas las tablas de usuario y las tablas del sistema en la base de datos [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  

## <a name="see-also"></a>Consulte también

- [DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
- [DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)
