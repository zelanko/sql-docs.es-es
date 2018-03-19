---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
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
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c564a6debb9c110cb41f8fc90a7cc1c0c5a01f7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Muestra el número de filas, el espacio en disco reservado y el espacio en disco usado para una tabla específica o para todas las tablas de una base de datos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ *database_name* . [ *schema_name* ] . | *schema_name* . ] *table_name*  
 Nombre de una, dos o tres partes de la tabla que se va a mostrar. En el caso de los nombres de tabla de dos o tres partes, el nombre debe incluirse entre comillas dobles (""). El uso de comillas en un nombre de tabla de una parte es opcional. Cuando no se especifica ningún nombre de tabla, se muestra la información de la base de datos actual.  
  
## <a name="permissions"></a>Permisos  
Requiere el permiso VIEW SERVER STATE.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Este es el conjunto de resultados de todas las tablas.
  
|columna|Tipo de datos|Description|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Espacio total usado para la base de datos, en KB.|  
|data_space|BIGINT|Espacio usado para los datos, en KB.|  
|index_space|BIGINT|Espacio usado para los índices, en KB.|  
|unused_space|BIGINT|Espacio que forma parte del espacio reservado y que no se usa, en KB.|  
|pdw_node_id|INT|Nodo de ejecución que se usa para los datos.|  
  
Este es el conjunto de resultados de una tabla.
  
|columna|Tipo de datos|Description|Intervalo|  
|------------|---------------|-----------------|-----------|  
|rows|BIGINT|Número de filas.||  
|reserved_space|BIGINT|Espacio total reservado para el objeto, en KB.||  
|data_space|BIGINT|Espacio usado para los datos, en KB.||  
|index_space|BIGINT|Espacio usado para los índices, en KB.||  
|unused_space|BIGINT|Espacio que forma parte del espacio reservado y que no se usa, en KB.||  
|pdw_node_id|INT|Nodo de ejecución que se usa para notificar el uso de espacio.||  
|distribution_id|INT|Distribución que se usa para notificar el uso de espacio.|El valor es -1 para las tablas replicadas.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. Sintaxis básica de DBCC PDW_SHOWSPACEUSED  
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
 ## <a name="see-also"></a>Vea también
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
