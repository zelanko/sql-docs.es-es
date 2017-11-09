---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/17/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a16d4a7a10eb4f36d0ead2a19f8e37d251e417f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Muestra el número de filas, el espacio de disco reservado y el espacio en disco usado para una tabla específica o para todas las tablas de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
 [ *database_name* . [ *schema_name* ]. | *schema_name* . ] *table_name*  
 Uno, dos o tres partes de nombre de la tabla que se mostrará. Para dos o nombres de tabla de tres partes, el nombre deben incluirse entre comillas dobles (""). Uso de comillas alrededor de un nombre de tabla de una parte es opcional. Cuando no se especifica ningún nombre de tabla, se muestra la información de la base de datos actual.  
  
## <a name="permissions"></a>Permissions  
Requiere el permiso VIEW SERVER STATE.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Se trata de un conjunto de resultados para todas las tablas.
  
|Columna|Tipo de datos|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|Espacio total utilizado para la base de datos, en KB.|  
|data_space|bigint|Espacio utilizado para los datos, en KB.|  
|index_space|bigint|Espacio utilizado para los índices, en KB.|  
|unused_space|bigint|Espacio que forma parte del espacio reservado y no se usa, en KB.|  
|pdw_node_id|int|Nodo de proceso que se utiliza para los datos.|  
  
Se trata de un conjunto de resultados para una tabla.
  
|Columna|Tipo de datos|Description|Intervalo|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|Número de filas.||  
|reserved_space|bigint|Espacio total reservado para el objeto, en KB.||  
|data_space|bigint|Espacio utilizado para los datos, en KB.||  
|index_space|bigint|Espacio utilizado para los índices, en KB.||  
|unused_space|bigint|Espacio que forma parte del espacio reservado y no se usa, en KB.||  
|pdw_node_id|int|Nodo de proceso que se utiliza para el uso del espacio de informes.||  
|distribution_id|int|Distribución que se utiliza para el uso del espacio de informes.|El valor es -1 para las tablas replicadas.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. Sintaxis básica de DBCC PDW_SHOWSPACEUSED  
Los ejemplos siguientes se muestran varias formas para mostrar el número de filas, la reserva de espacio en disco y espacio en disco utilizado por la tabla FactInternetSales en la [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] base de datos.
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. Mostrar el espacio en disco utilizado por todas las tablas de la base de datos actual  
 En el ejemplo siguiente se muestra el espacio en disco reservado y las utilizan todas las tablas de usuario y las tablas del sistema en el [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] base de datos.  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>Vea también
[DBCC PDW_SHOWEXECUTIONPLAN &#40; Transact-SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40; Transact-SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  

