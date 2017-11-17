---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Documentos de Microsoft
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
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9d1a4659deeab00589a09e66d885d7f7005f7a43
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Muestra el tamaño y el número de filas para cada partición de una tabla en una [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ *database_name* . [ *schema_name* ]. | *schema_name* . ] *table_name*  
 Uno, dos o tres partes de nombre de la tabla que se mostrará.  Para dos o nombres de tabla de tres partes, el nombre deben incluirse entre comillas dobles (""). Uso de comillas alrededor de un nombre de tabla de una parte es opcional.  
  
## <a name="permissions"></a>Permissions
Requiere **VIEW SERVER STATE** permiso.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Se trata de los resultados del comando DBCC PDW_SHOWPARTITIONSTATS.
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|partition_number|int|Número de partición.|  
|used_page_count|bigint|Número de páginas utilizadas para los datos.|  
|reserved_page_count|bigint|Número de páginas asignadas a la partición.|  
|row_count|bigint|Número de filas de la partición.|  
|pdw_node_id|int|Nodo de proceso para los datos.|  
|distribution_id|int|Identificador de la distribución de los datos.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. Ejemplos de sintaxis básica de DBCC PDW_SHOWPARTITIONSTATS  
Los ejemplos siguientes muestran el espacio utilizado y el número de filas por partición para la tabla FactInternetSales en la [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] base de datos.
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>Vea también
[DBCC PDW_SHOWEXECUTIONPLAN &#40; Transact-SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)  
  

